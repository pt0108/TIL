> 부트캠프 6주차 2022년 11월 24일

## 실습 - Wine Quality Data Set

### Data 개요

**적포도주 및 백포도주 샘플들의 물리화학적 특성 및 품질 등급**

- UCI 머신러닝 저장소에 공개 : [dataset](https://archive.ics.uci.edu/ml/datasets/Wine+Quality)
- 포르투갈 "Vinho Verde" 와인의 레드 및 화이트 변종 샘플에 대한 정보를 제공
- 각 와인 샘플은 와인 전문가에 의해 품질 평가를 받았고 화학적 테스트를 거쳤음
- 개인 정보 보호 및 물류 문제로 인해 포도 유형, 와인 브랜드, 와인 판매 가격 등에 대한 데이터가 없음
    
    ```
       Input variables (based on physicochemical tests):
       1 - fixed acidity (고정된 산도)
       2 - volatile acidity (휘발성 산도)
       3 - citric acid (구연산)
       4 - residual sugar (잔여 설탕)
       5 - chlorides (염화물)
       6 - free sulfur dioxide (유리 이산화황)
       7 - total sulfur dioxide (총 이산화황)
       8 - density (밀도)
       9 - pH (산도)
       10 - sulphates (황산염)
       11 - alcohol (알코올)
    
       Output variable (based on sensory data):
       12 - quality (품질) (score between 0 and 10)
    ```
    

### Step 1 : 질문하기 (Ask questions)

데이터가 주어진 상태에서 질문을 할 수도 있고, 질문에 답할 수 있는 데이터를 수집할 수도 있다.

**질문 예시**

- 와인의 품질을 예측하는 데 가장 중요한 화학적 특성은 무엇일까?
- 어떤 유형(white, red)의 와인이 더 좋은 평가를 받을까?
- 알코올 도수가 높은 와인이 더 좋은 평가를 받을까?
- 더 달콤한 와인이 더 나은 평가를 받을까?
- 어느 정도의 산도가 와인 품질에 영향을 미칠까?

### Step 2 : 데이터 랭글링 (Wrangle data)

- 데이터 랭글링 : 원자료(raw data)를 보다 쉽게 접근하고 분석할 수 있도록 데이터를 정리하고 통합하는 과정 (참고. 위키피디아)
- 세부적으로는 데이터의 수집(gather), 평가(assess), 정제(clean) 작업으로 나눌 수 있다.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

****2.1 수집(gather)****

```python
df_red = pd.read_csv('./datasets/winequality-red.csv', sep=';')
df_white = pd.read_csv('./datasets/winequality-white.csv', sep=';')
```

```python
df_red.head()
```

![image](https://user-images.githubusercontent.com/106129152/203901991-5be8e4b6-06f6-45b1-9f50-59f991a72d88.png)

```python
df_white.head()
```

![image](https://user-images.githubusercontent.com/106129152/203902001-8f4bc235-a9b4-48b9-9f02-65aa92572c96.png)

****2.2 평가(assess)****

**샘플의 개수**, **컬럼의 개수**

```python
df_red.shape, df_white.shape
# ((1359, 12), (3961, 12))
```

**누락 데이터 확인**

```python
df_red.info()
# <class 'pandas.core.frame.DataFrame'>
# Int64Index: 1359 entries, 0 to 1598
# Data columns (total 12 columns):
#  #   Column                Non-Null Count  Dtype  
# ---  ------                --------------  -----  
#  0   fixed acidity         1359 non-null   float64
#  1   volatile acidity      1359 non-null   float64
#  2   citric acid           1359 non-null   float64
#  3   residual sugar        1359 non-null   float64
#  4   chlorides             1359 non-null   float64
#  5   free sulfur dioxide   1359 non-null   float64
#  6   total sulfur dioxide  1359 non-null   float64
#  7   density               1359 non-null   float64
#  8   pH                    1359 non-null   float64
#  9   sulphates             1359 non-null   float64
#  10  alcohol               1359 non-null   float64
#  11  quality               1359 non-null   int64  
# dtypes: float64(11), int64(1)
# memory usage: 138.0 KB

df_white.info()
# <class 'pandas.core.frame.DataFrame'>
# Int64Index: 3961 entries, 0 to 4897
# Data columns (total 12 columns):
#  #   Column                Non-Null Count  Dtype  
# ---  ------                --------------  -----  
#  0   fixed acidity         3961 non-null   float64
#  1   volatile acidity      3961 non-null   float64
#  2   citric acid           3961 non-null   float64
#  3   residual sugar        3961 non-null   float64
#  4   chlorides             3961 non-null   float64
#  5   free sulfur dioxide   3961 non-null   float64
#  6   total sulfur dioxide  3961 non-null   float64
#  7   density               3961 non-null   float64
#  8   pH                    3961 non-null   float64
#  9   sulphates             3961 non-null   float64
#  10  alcohol               3961 non-null   float64
#  11  quality               3961 non-null   int64  
# dtypes: float64(11), int64(1)
# memory usage: 402.3 KB
```

**중복 데이터 확인**

```python
df_red.duplicated().sum()
# 240

df_white.duplicated().sum()
# 937
```

**quality 컬럼(특성)의 고유값과 개수**

```python
df_red['quality'].unique(), df_red['quality'].nunique()
# (array([5, 6, 7, 4, 8, 3], dtype=int64), 6)

df_white['quality'].unique(), df_white['quality'].nunique()
# (array([6, 5, 7, 8, 4, 3, 9], dtype=int64), 7)
```

unique()는 고유한 값을 출력, nunique()는 고유한 값의 수를 출력

**통계 정보 확인**

가독성을 높이기 위해, 

인덱스를 컬럼으로, 컬럼을 인덱스로 변경해주는 .T를 사용해서 확인

```python
df_red.describe().T
```

![image](https://user-images.githubusercontent.com/106129152/203902031-dbe843e4-979e-4c38-ba41-30207fa79390.png)

```python
df_white.describe().T
```

![image](https://user-images.githubusercontent.com/106129152/203902040-e2636f19-35c8-4cb1-8199-7fb693c6555c.png)

****2.3 정제(clean)****

**중복데이터 삭제**

```python
df_red.drop_duplicates(inplace = True)
df_white.drop_duplicates(inplace = True)
```

**두 데이터 프레임 합치기**

```python
# 각각 red와 white 와인임을 알 수 있는 color 컬럼 추가
df_red['color'] = 'red'
df_white['color'] = 'white'

# 데이터 프레임 합치기
wine_df = pd.concat([df_red, df_white], axis=0)
wine_df.tail()

wine_df.shape
# (5320, 13)
```

![image](https://user-images.githubusercontent.com/106129152/203902064-766080f5-500a-414f-b2a0-f4eeda9dfe96.png)

### Step 3 : 데이터 탐색 (Exploratory Data Analysis)

데이터의 패턴을 찾고, 관계를 시각화 하는 작업 등으로 통해 데이터에 대한 직관을 극대화 한다.

****3.1 새로 결합된 데이터 프레임으로 histogram 그리기****

- fixed acidity, total sulfur dioxide, pH, alcohol
    
    ```python
    hist_col = ['fixed acidity', 'total sulfur dioxide', 'pH', 'alcohol']
    h = wine_df[hist_col].hist(bins=20, figsize=(18, 10))
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/203902107-8f28eceb-c165-44fc-961c-fd670632779b.png)
    

Q. 특성 중 오른쪽으로 꼬리가 긴 분포(right skewed distribution)는 어떤것인가?

A. fixed acidity, alcohol

****3.2 새로 결합된 데이터 프레임으로 산점도 그리기****

- quality와 아래의 특성들간의 상관관계 파악하기
- volatile acidity, residual sugar, pH, alcohol
    
    ```python
    scatter_col = ['volatile acidity', 'residual sugar', 'pH', 'alcohol']
    obj = pd.plotting.scatter_matrix(wine_df[scatter_col], figsize=(16, 10))
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/203902148-b3cc8a52-cb61-4cd2-98b7-397201085f06.png)
    
    ```python
    scatter_col = ['volatile acidity', 'residual sugar', 'pH', 'alcohol', 'quality']
    
    figrue, axes = plt.subplots(nrows=1, ncols=len(scatter_col)-1, figsize=(22, 4))
    
    for index, column in enumerate(scatter_col[:-1]):
        sns.regplot(data=wine_df[scatter_col], x=column, y='quality', ax=axes[index] )
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/203902166-12202b09-7133-416c-8fd4-17aaaf2e4c7d.png)
    
    ```python
    wine_df[scatter_col].corr()
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/203902183-8c7f0f49-89de-4501-bd99-012f05debd81.png)
    
    Q. 품질에 긍정적인 영향을 미칠 가능성이 높은 특성은 어떤 것인가?
    
    A. alcohol
    

### Step 4 : 결론 도출 또는 예측 (Draw conclusions or make predictions)

****4.1 어떤 유형(white, red)의 와인이 더 좋은 평가를 받을까?****

```python
wine_df.groupby('color').mean()['quality']
# color
# red      5.623252
# white    5.854835
# Name: quality, dtype: float64

sns.barplot(data=wine_df, x='color', y='quality')
```

![image](https://user-images.githubusercontent.com/106129152/203902200-37468abb-a4cf-40ff-b694-8b0b0214df5f.png)

→ white wine의 quality 평균값이 더 높음

****4.2 어느 정도의 산도가 와인 품질에 영향을 미칠까?****

- 산도를 4등분하여 (low, medium, medium_high, high ) 어느 단계의 quality의 평균값이 높은지 확인하기
    
    ```python
    wine_df['pH'].describe()
    # count    5320.000000
    # mean        3.224664
    # std         0.160379
    # min         2.720000
    # 25%         3.110000
    # 50%         3.210000
    # 75%         3.330000
    # max         4.010000
    # Name: pH, dtype: float64
    
    # 데이터 구간 분할
    bins = [2.72, 3.11, 3.21, 3.33, 4.01]
    labels = ['high', 'medium_high', 'medium', 'low']
    wine_df['acidity_levels'] = pd.cut(wine_df['pH'], bins=bins, labels =labels)
    
    wine_df['acidity_levels'].value_counts()
    # medium         1391
    # high           1331
    # medium_high    1330
    # low            1267
    # Name: acidity_levels, dtype: int64
    
    sns.barplot(data=wine_df, x='acidity_levels', y='quality')
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/203902220-4e66f8e1-383c-4b70-b22f-296d52a2f370.png)
    
    → medium 단계의 평균값이 가장 높음
    

****4.3 더 달콤한 와인이 더 나은 평가를 받을까?****

```python
median_sugar = wine_df['residual sugar'].median()
low_sugar = wine_df[wine_df['residual sugar'] < median_sugar]
high_sugar = wine_df[wine_df['residual sugar'] >= median_sugar]

low_sugar['quality'].mean()
# 5.78316032295271

high_sugar['quality'].mean()
# 5.807649871276205

wine_df['sugar_level'] = pd.qcut(wine_df['residual sugar'], 2, labels=['low_sugar', 'high_sugar'])
wine_df.groupby('sugar_level').mean()['quality']
# sugar_level
# low_sugar     5.789513
# high_sugar    5.801887
# Name: quality, dtype: float64

sns.barplot(data=wine_df, x='sugar_level', y='quality')
```

![image](https://user-images.githubusercontent.com/106129152/203902234-828554a6-173d-4cd3-8aa4-e92835748f56.png)

→ 더 달콤한 와인의 quality 평균값이 조금 더 높음

****4.4 알코올 도수가 높은 와인이 더 좋은 평가를 받을까?****

```python
median_alcohol = wine_df['alcohol'].median()
low_alcohol = wine_df[wine_df['alcohol'] < median_alcohol]
high_alcohol = wine_df[wine_df['alcohol'] >= median_alcohol]

low_alcohol['quality'].mean()
# 5.439202148062908

high_alcohol['quality'].mean()
# 6.138223368964246

wine_df["alcohol_level"] = pd.qcut(wine_df['alcohol'], 2, labels=['low_alcohol', 'high_alcohol'])
sns.barplot(data=wine_df, x='alcohol_level', y='quality')
```

![image](https://user-images.githubusercontent.com/106129152/203902243-bb3e0c9c-a87d-41ff-be44-d8113b5e2810.png)

→ 알콜 도수가 높은 와인의 quality 평균값이 더 높음

### Step 5 : 결과 공유 (Communicate the results)

보고서, 이메일, 블로그 등 다양한 방법을 통해 발견한 통찰들을 공유할 수 있다.
