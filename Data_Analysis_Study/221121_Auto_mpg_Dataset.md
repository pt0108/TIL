> 부트캠프 6주차 2022년 11월 21일


## Pandas 실습 - Auto mpg Dataset

**자동차 연비 데이터셋**

- [UCI Machine Learning Repository](http://archive.ics.uci.edu/ml/index.php)의 [Auto MPG Data Set](https://archive.ics.uci.edu/ml/datasets/auto+mpg)에서 다운로드
- [Kaggle](https://www.kaggle.com/)의 [Auto-mpg dataset](https://www.kaggle.com/uciml/autompg-dataset)에서 다운로드

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
```

### 1. 데이터 탐색

**1.1 데이터 적재**

```python
df = pd.read_csv('./datasets/auto-mpg.csv', header=None)
```

**1.2 데이터 일부 확인**

```python
df.head()
```

![image](https://user-images.githubusercontent.com/106129152/203181982-94b8b1e3-4ecf-49a6-b9ed-b78f4bdb0dea.png)

```
mpg: continuous
cylinders: multi-valued discrete
displacement: continuous
horsepower: continuous
weight: continuous
acceleration: continuous
model year: multi-valued discrete
origin: multi-valued discrete
car name: string (unique for each instance)
```

**1.3 열 이름 지정**

```python
df.columns = ['mpg', 'cylinders', 'displacement', 'horsepower', 'weight', 'acceleration', 'model year', 'origin', 'name']
```

- mpg : 연비
- cylinders : 실린더수
- displacement : 배기량
- horsepower: 출력
- weight : 차중
- acceleration : 가속능력
- model year : 출시년도
- origin : 제조국 1(USA), 2(EU), 3(JPN)
- name : 모델명

**1.4 데이터 형상 확인**

```python
df.shape
# (398, 9)
```

**1.5 데이터 요약정보 확인(데이터 타입, 누락정보)**

```python
df.info()
# <class 'pandas.core.frame.DataFrame'>
# RangeIndex: 398 entries, 0 to 397
# Data columns (total 9 columns):
#  #   Column        Non-Null Count  Dtype  
# ---  ------        --------------  -----  
#  0   mpg           398 non-null    float64
#  1   cylinders     398 non-null    int64  
#  2   displacement  398 non-null    float64
#  3   horsepower    398 non-null    object 
#  4   weight        398 non-null    float64
#  5   acceleration  398 non-null    float64
#  6   model year    398 non-null    int64  
#  7   origin        398 non-null    int64  
#  8   name          398 non-null    object 
# dtypes: float64(4), int64(3), object(2)
# memory usage: 28.1+ KB
```

**1.6 데이터 자료형 확인**

```python
df.dtypes
# mpg             float64
# cylinders         int64
# displacement    float64
# horsepower       object
# weight          float64
# acceleration    float64
# model year        int64
# origin            int64
# name             object
# dtype: object
```

**1.7 Series(horsepower열)의 자료형 확인**

```python
df['horsepower'].dtypes # O : Object
# dtype('O')

df['horsepower'].isin(['?']).sum()
# 6
```

horsepower는 숫자 데이터인데  object 형으로 반환된 이유

→ 6개의 '?' 때문에 Object 형으로 반환

**1.8 제조국(origin) 특성의 데이터 분포(건수)확인하기**

• 1(USA), 2(EU), 3(JPN)

```python
df['origin'].value_counts()
# 1    249
# 3     79
# 2     70
# Name: origin, dtype: int64
```

**1.9 제조국(origin) 특성을 histogram으로 표현하기**

```python
df['origin'].plot(kind='hist')
```

![image](https://user-images.githubusercontent.com/106129152/203182027-5002ccce-e671-4ad6-912d-16169c590606.png)

**1.10 country 컬럼 추가하기**

제조국 1, 2, 3을 각각 "USA", "Europe", "Japan"으로 대체한 값을 새로운 컬럼(country)에 적용하기

```python
df['country'] = df['origin'].replace([1, 2, 3], ['USA', 'Europe', 'Japan'])
df.tail()
```

![image](https://user-images.githubusercontent.com/106129152/203182051-0898ff8a-0c97-4555-86c9-5884b6ad74cd.png)
coutry 특성으로 groupby하여 "국가당 몇건"의 샘플이 있는지 확인하기

```python
df.groupby('country').size() # df['country'].value_counts() 와 동일
# country
# Europe     70
# Japan      79
# USA       249
# dtype: int64
```

위에서 구한 국가당 레코드수를 파이차트 그리기

```python
country = df.groupby('country').size()
country.plot(kind='pie', autopct="%.1f%%")
```

![image](https://user-images.githubusercontent.com/106129152/203182064-08912736-51ed-41bf-bbdc-21a0c5b1895e.png)

**1.11 국가별(country) mpg 값의 분포를 boxplot으로 확인하기**

Q. mpg의 중간값이 가장 낮은 국가는?

```python
# 참고 : seaborn에서
# 범주형 데이터 값에 따른 수치형 데이터 값이 어떠한지 나타내는 그래프
# - 막대 그래프(barplot)
# - 박스 플롯(boxplot) -> 상자수염도
# - 포인트 플롯(pointplot)

# 제조국(범주형 데이터)에 따른 연비(수치형)를 확인
sns.boxplot(data=df, x='country', y='mpg')
```

![image](https://user-images.githubusercontent.com/106129152/203182078-e2a633f5-b00e-469e-8b51-d02cbe0ecc15.png)

**1.12 통계 정보 확인**

```python
df.describe()
```

![image](https://user-images.githubusercontent.com/106129152/203182101-8f01ae51-1ad9-4c6b-a9c7-7fc59ba06e85.png)

**1.13 특성들 간의 상관관계 구하기**

상관계수 매트릭스 : df.corr() 이용

```python
df_corr = df.corr()
df_corr
```

![image](https://user-images.githubusercontent.com/106129152/203182119-0a2eff8d-1275-4066-8e28-5fbfa0bbc2e6.png)

(시각화 1) 상관계수 산점도로 시각화 하기 : pd.plotting.scatter_matrix()

```python
obj = pd.plotting.scatter_matrix(df, figsize=(24, 16))
```

![image](https://user-images.githubusercontent.com/106129152/203182133-3d470256-1181-40c8-9380-856f137c7bee.png)

(시각화 2) 상관계수 히트맵으로 시각화하기

```python
# 히트맵은 seaborn에만 있음
sns.heatmap(df_corr, annot=True, fmt='.2f', cmap='Reds')
```

![image](https://user-images.githubusercontent.com/106129152/203182142-4a0a0b94-18c4-4163-8656-43ab692fc15d.png)

[컬러맵 정보](https://matplotlib.org/stable/tutorials/colors/colormaps.html)

Q. 타깃(mpg)와의 상관계수가 가장 높은 특성은?

A. weight(차중)가 mpg와 음의 상관관계가 높다.

weight 특성과, mpg(타깃) 의 상관관계 및 산점도

```python
df[['weight', 'mpg']].corr()
```

![image](https://user-images.githubusercontent.com/106129152/203182170-5c68394a-1552-4e2f-88c5-8274bdffb575.png)

```python
df.plot(kind='scatter', x='weight', y='mpg', alpha=0.5)
```

![image](https://user-images.githubusercontent.com/106129152/203182188-4839f7ae-0ba7-4a67-af56-6ffb2bbeed46.png)

### 2. 데이터 처리

**2.1 누락데이터 처리하기**

• horsepower 열의 ('?')를 np.nan으로 변경

```python
# 기존 '?'의 개수
df['horsepower'].isin(['?']).sum()
# 6

df['horsepower'].replace('?', np.nan, inplace=True)

df['horsepower'].isin(['?']).sum()
# 0
```

• 누락 데이터 삭제하기(행삭제)

```python
df.dropna(axis=0, inplace=True)

df['horsepower'].isnull().sum()
# 0
```

• horsepower 컬럼의 데이터 타입을 실수형으로 변환

```python
df['horsepower'] = df['horsepower'].astype('float64')
df.describe() # horsepower 컬럼이 실수형으로 변환되어 추가된 것을 확인
```

![image](https://user-images.githubusercontent.com/106129152/203182210-65251d07-b3f8-4487-be81-7f47786c4ebf.png)

**2.2 데이터 구간 분할**

- horsepower 컬럼에 대해 3개의 구간으로 나누어 범주화 하기
- 예) 저출력, 보통출력, 고출력

```python
df['hp_cats'] = pd.cut(df['horsepower'], 3, labels=['저출력', '보통출력', '고출력'])
df['hp_cats']
# 0      보통출력
# 1      보통출력
# 2      보통출력
# 3      보통출력
# 4      보통출력
#        ... 
# 393     저출력
# 394     저출력
# 395     저출력
# 396     저출력
# 397     저출력
# Name: hp_cats, Length: 392, dtype: category
# Categories (3, object): ['저출력' < '보통출력' < '고출력']

df['hp_cats'].value_counts()
# 저출력     257
# 보통출력    103
# 고출력      32
# Name: hp_cats, dtype: int64
```

**2.3 더미 변수**

• 범주화된 horwerpower 컬럼을 더미변수화 하기

```python
horsepower_dummies = pd.get_dummies(df['hp_cats'])
horsepower_dummies
```

![image](https://user-images.githubusercontent.com/106129152/203182230-5da9fd78-b4ee-437c-9957-1a33bcc59dd2.png)

**2.4 불필요한 컬럼 삭제**

• horsepower, hp_cat, name 컬럼 삭제

```python
df.drop(['horsepower', 'hp_cats', 'name'], axis=1, inplace=True)
```

mysql에서 배웠던 것처럼, concat()으로 데이터를 이어붙일 수도 있다.

```python
df = pd.concat([df, horsepower_dummies], axis=1)
df.head()
```

![image](https://user-images.githubusercontent.com/106129152/203182246-88a44c78-d96b-4dcb-ae51-22c5ae171c92.png)

**2.5 중복 데이터 확인**

```python
df.duplicated().sum()
# 0
```
