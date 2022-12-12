> 부트캠프 6주차 2022년 11월 22일

## Pandas 실습 - Titanic Dataset

### **타이타닉 데이터셋 도전**

- 승객의 나이, 성별, 승객 등급, 승선 위치 같은 속성을 기반으로 하여 승객의 생존 여부를 예측하는 것이 목표
- [캐글](https://www.kaggle.com/)의 [타이타닉 챌린지](https://www.kaggle.com/c/titanic)에서 `train.csv`와 `test.csv`를 다운로드
- 두 파일을 각각 datasets 디렉토리에 titanic_train.csv titanic_test.csv로 저장

### 1. 데이터 탐색

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

**1.1 데이터 적재**

```python
titanic = pd.read_csv('./datasets/titanic_test.csv')
```

**1.2 titanic_df 살펴보기**

```python
titanic.head()
```

![image](https://user-images.githubusercontent.com/106129152/203244729-5a90aa60-6eba-42c8-9f48-d40011a00e4b.png)

- **Survived**: 타깃. 0은 생존하지 못한 것이고 1은 생존을 의미
- **Pclass**: 승객 등급. 1, 2, 3등석.
- **Name**, **Sex**, **Age**: 이름 그대로의 의미
- **SibSp**: 함께 탑승한 형제, 배우자의 수
- **Parch**: 함께 탑승한 자녀, 부모의 수
- **Ticket**: 티켓 아이디
- **Fare**: 티켓 요금 (파운드)
- **Cabin**: 객실 번호
- **Embarked**: 승객이 탑승한 곳. C(Cherbourg), Q(Queenstown), S(Southampton)

**1.3 누락 데이터 살펴보기**

```python
titanic.info()
# <class 'pandas.core.frame.DataFrame'>
# RangeIndex: 891 entries, 0 to 890
# Data columns (total 12 columns):
#  #   Column       Non-Null Count  Dtype  
# ---  ------       --------------  -----  
#  0   PassengerId  891 non-null    int64  
#  1   Survived     891 non-null    int64  
#  2   Pclass       891 non-null    int64  
#  3   Name         891 non-null    object 
#  4   Sex          891 non-null    object 
#  5   Age          714 non-null    float64
#  6   SibSp        891 non-null    int64  
#  7   Parch        891 non-null    int64  
#  8   Ticket       891 non-null    object 
#  9   Fare         891 non-null    float64
#  10  Cabin        204 non-null    object 
#  11  Embarked     889 non-null    object 
# dtypes: float64(2), int64(5), object(5)
# memory usage: 83.7+ KB
```

**1.4 통계치 살펴보기**

```python
titanic.describe()
```

![image](https://user-images.githubusercontent.com/106129152/203244784-b804ed6c-2ce7-4346-9295-4fb7ed1028a8.png)

참고로 count 값은 null인 값을 제외한 결과이다.

**1.5 Survived 컬럼 값의 빈도수 확인**

```python
titanic['Survived'].value_counts()
# 0    549
# 1    342
# Name: Survived, dtype: int64
```

**1.6 범주형(카테고리) 특성들의 빈도수 확인**

- **Pclass**, **Sex**, **Embarked**
- **Embarked** 특성은 승객이 탑승한 곳 : C=Cherbourg, Q=Queenstown, S=Southampton.

```python
titanic['Pclass'].value_counts()
# 3    491
# 1    216
# 2    184
# Name: Pclass, dtype: int64

titanic['Sex'].value_counts()
# male      577
# female    314
# Name: Sex, dtype: int64

titanic['Embarked'].value_counts(dropna=False)
# S      644
# C      168
# Q       77
# NaN      2
# Name: Embarked, dtype: int64

```

**1.7 Name과 Age 열을 Age 순으로 정렬해서 보기**

```python
titanic[['Name', 'Age']].sort_values(by='Age')
```

![image](https://user-images.githubusercontent.com/106129152/203244834-c9ec1c3f-7cce-435e-a2f5-4e7de0522d75.png)

**1.8 나이(Age)가 60 이상인 사람들의 Name과 Age 확인해보기**

```python
titanic.loc[titanic['Age'] >= 60, ['Name', 'Age']]
```

![image](https://user-images.githubusercontent.com/106129152/203244868-b3d6439f-54a0-49a2-8554-9b152ac92838.png)

**1.9 나이(Age)가 60 이상이고 1등석에 탔으며, 여성인 탑승자 확인해보기**

```python
titanic.loc[(titanic['Age'] >= 60)&(titanic['Pclass'] == 1)&(titanic['Sex'] == 'female'), ['Name', 'Survived', 'Age', 'Sex']]
```

![image](https://user-images.githubusercontent.com/106129152/203244896-32237b47-e0b3-4644-b943-bf8314c0f815.png)

**1.10 요금(Fare)의 최댓값 최솟값 확인해보기**

```python
titanic['Fare'].max()
# 512.3292

titanic['Fare'].min()
# 0.0
```

**1.11 등급(Pcalss) 그룹별 생존률 확인해보기**

→ [Pandas groupby](https://teddylee777.github.io/pandas/pandas-groupby)

```python
titanic.groupby('Pclass').mean()['Survived']
# Pclass
# 1    0.629630
# 2    0.472826
# 3    0.242363
# Name: Survived, dtype: float64
```

아래와 같은 방법도 동일한 결과를 얻을 수 있다.

```python
titanic.groupby('Pclass').agg({'Survived':'mean'})
```

![image](https://user-images.githubusercontent.com/106129152/203244923-c222ae6b-6965-4cfd-b191-6e4d4f41cafa.png)

문제와는 별개로, 

아래 방법으로 생존 여부 확인이 가능하다. (사망자와 생존자의 수)

```python
titanic.groupby(['Pclass', 'Survived']).size()
# Pclass  Survived
# 1       0            80
#         1           136
# 2       0            97
#         1            87
# 3       0           372
#         1           119
# dtype: int64
```

### 2. 데이터 전처리 (누락 데이터 처리, 범주화 등)

**2.1 Cabin 열 : 전체 삭제하기**

```python
titanic.drop('Cabin', axis='columns') # 열을 삭제
```

아래와 같은 방법도 사용할 수 있다.

```python
titanic.dropna(thresh=600, axis='columns') # not null인 값이 600건 이상인 것은 삭제 대상에서 제외
```

**2.2 Embarked 열 : 누락 데이터를 승선도시 최고 빈도수 값으로 대체하기**

```python
# 누락 데이터의 건수 확인
titanic['Embarked'].isnull().sum()
# 2

sr = titanic['Embarked'].value_counts(dropna=False)
sr
# S      644
# C      168
# Q       77
# NaN      2
# Name: Embarked, dtype: int64
```

```python
# numpy : 가장 큰 값의 index를 구하는 함수 argmax
# pandas : 가장 큰 값의 index를 구하는 함수 idxmax

most_freq = sr.idxmax()

titanic['Embarked'].fillna(most_freq)
# 0      S
# 1      C
# 2      S
# 3      S
# 4      S
#       ..
# 886    S
# 887    S
# 888    S
# 889    C
# 890    Q
# Name: Embarked, Length: 891, dtype: object
```

**2.3 Age 열 : 중간값으로 대체하기**

```python
median_age = titanic['Age'].median() # 28.0

titanic['Age'].fillna(median_age, inplace=True)
```

**2.4 Age 열 : 범주로 나눠보기**

- 0~18세
- 18~25세
- 25~35세
- 35~60세
- 60~80세

```python
bins = [0, 18, 25, 35, 60, 80]
group_names = ['Childeren', 'Youth', 'YoungAdult', 'MiddleAge', 'Senior']

age_cats = pd.cut(titanic['Age'], bins, labels = group_names)
age_cats
# 0           Youth
# 1       MiddleAge
# 2      YoungAdult
# 3      YoungAdult
# 4      YoungAdult
#           ...    
# 886    YoungAdult
# 887         Youth
# 888    YoungAdult
# 889    YoungAdult
# 890    YoungAdult
# Name: Age, Length: 891, dtype: category
# Categories (5, object): ['Childeren' < 'Youth' < 'YoungAdult' < 'MiddleAge' < 'Senior']
```

age_cats를 컬럼에 추가해보자.

```python
titanic['AgeCat'] = age_cats
titanic.head()
```

![image](https://user-images.githubusercontent.com/106129152/203244996-77c6539b-cfda-4450-9755-a8680c0b704f.png)

이 AgeCat(범주형 데이터)으로 수치형 데이터를 확인할 수 있다.

```python
# 히스토그램으로 연령대 분포 확인하기
titanic['Age'].hist(bins=15)
```

![image](https://user-images.githubusercontent.com/106129152/203245020-aa1ef4e5-a1b6-474c-a450-dd68a5c2da76.png)

```python
# 연령대에 따른 생존률
sns.barplot(data=titanic, x='AgeCat', y='Survived', ci=None)
```

![image](https://user-images.githubusercontent.com/106129152/203245040-4c898628-992a-4b99-a84e-532583b38728.png)

```python
# 연령대에 따른 요금
sns.barplot(data=titanic, x='AgeCat', y='Fare', ci=None)
```

![image](https://user-images.githubusercontent.com/106129152/203245070-c15fa524-4ae8-4755-b840-446afc8ca096.png)

• 범주 데이터를 dummy 변수로 바꿔보기 (One-Hot Encoding)

```python
# Pclass, Embarked, Sex

Pclass_dummies = pd.get_dummies(titanic['Pclass'], prefix='Pclass')
Embarked_dummies = pd.get_dummies(titanic['Embarked'], prefix='Embarked')
Sex_dummies = pd.get_dummies(titanic['Sex'], prefix='Sex')

# 이어 붙이기
pd.concat([titanic, Pclass_dummies, Embarked_dummies, Sex_dummies], axis=1)
```

**2.5 중복 데이터 확인**

```python
titanic.duplicated().sum()
# 0
```
