> 부트캠프 5주차 2022년 11월 18일

## Pandas - (11/17 Pandas 이어서)

### ***🖍Workshop 1***

- 행 삭제
    
    ```python
    exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
                 '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}
    
    df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
    ```
    
    ```python
    # '서준'행 삭제
    result = df.drop('서준', axis='index') # drop 함수 : axis에 지정된 "축을" 삭제
    
    # '서준', '우현' 행 삭제
    result = df.drop(['서준', '우현'], axis='index') # drop 함수 : axis에 지정된 "축을" 삭제
    ```
    
- 열 삭제
    
    ```python
    exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
                 '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}
    
    df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
    ```
    
    ```python
    # '수학' 열 삭제
    df.drop('수학', axis=1) # axis=1 : column 을 삭제!
    
    # '수학', '영어' 열 삭제
    df.drop(['수학', '영어'], axis=1)
    ```
    
- 행 선택
    
    ```python
    exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
                 '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}
    
    df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
    ```
    
    ```python
    # '서준' 행 선택(라벨 색인, 정수 색인)
    df.loc['서준'] # 라벨 색인
    df.iloc[0] # 정수 색인
    
    # '서준', '우현' 행 선택 (라벨 색인, 정수 색인, 슬라이싱)
    df.loc[['서준', '우현']] # 라벨 색인
    df.iloc[[0, 1]] # 정수 색인
    
    # 혹은 아래와 같이
    df.loc['서준':'우현']
    df['서준':'우현'] # 행색인임에도 슬라이싱일 경우에는 loc를 넣지 않아도 됨
    
    df.iloc[0:2] # 정수 슬라이싱할 때는 마지막 범위(2)가 포함되지 않음에 주의
    ```
    
    참고 : 서준' 행으로 색인을 하면 1차원 Series 데이터가 나오는데,
    
    ['서준'] 행으로 색인을 하면 2차원 DataFrame 으로 결과가 나온다.
    
- 열 선택
    
    ```python
    exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
                 '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}
    
    df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
    ```
    
    ```python
    # '수학' 열 선택
    df['수학'] # df.수학
    
    # '음악', '체육' 열 선택
    df[['음악', '체육']]
    ```
    
- 원소 선택
    
    ```python
    exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
                 '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}
    
    df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
    ```
    
    ```python
    # '서준'의 '음악' 점수
    df.loc['서준', '음악']
    df.loc['서준']['음악']
    df.iloc[0, 2]
    df.iloc[0][2] 
    
    #'서준'의 '음악','체육' 점수
    df.loc['서준', ['음악', '체육']]
    df.loc['서준'][['음악', '체육']]
    df.iloc[0, [2, 3]]
    df.iloc[0][[2, 3]]
    
    #'서준','우현'의 '음악','체육' 점수
    df.loc[['서준', '우현'], ['음악', '체육']]
    df.loc[['서준', '우현']][['음악', '체육']]
    df.iloc[[0, 1], [2, 3]]
    ```
    
- 열 추가
    
    ```python
    exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
                 '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}
    
    df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
    ```
    
    ```python
    # '국어' 열 추가, 값은 80 점 지정
    df['국어'] = 80
    ```
    
- 행 추가
    
    ```python
    exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
                 '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}
    
    df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
    ```
    
    ```python
    # "본인 이름" 으로 행추가, 과목 점수도 지정
    df.loc['재영'] = [100, 100, 100, 100]
    ```
    
- 원소 값 변경
    
    ```python
    exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
                 '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}
    
    df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
    ```
    
    ```python
    # '서준'의 '체육' 점수를 80 점으로 변경(라벨 색인, 정수 색인)
    df.loc['서준']['체육'] = 80 # df.loc['서준', '체육']
    
    # '서준'의 '음악','체육' 점수 변경
    df.iloc[0, [2, 3]]= 100, 100
    ```
    
- 행, 열 바꾸기
    
    ```python
    exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
                 '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}
    
    df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
    ```
    
    ```python
    df.T # df.transpose() 도 가능하다
    ```
    
- 특정 열을 행 인덱스로 설정
    
    ```python
    exam_data = {'이름' : [ '서준', '우현', '인아'],
                 '수학' : [ 90, 80, 70],
                 '영어' : [ 98, 89, 95],
                 '음악' : [ 85, 95, 100],
                 '체육' : [ 100, 90, 90]}
    df = pd.DataFrame(exam_data)
    ```
    
    ```python
    df.set_index(['이름'], inplace=True)
    
    df.reindex(['인아', '서준', '우현', '재영'])
    
    df.reset_index()
    ```
    

### ***🖍Workshop 2***

- 데이터 프레임 객체에서 색인 연습
    
    ```python
    data = {'state': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada'],
            'year': [2000, 2001, 2002, 2001, 2002],
            'pop': [1.5, 1.7, 3.6, 2.4, 2.9]}
    frame2 = pd.DataFrame(data, columns=['year', 'state', 'pop', 'debt'],
                          index=['one', 'two', 'three', 'four', 'five'])
    frame2
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/202634249-e94565aa-0252-482d-b1e0-067fbc927068.png)
    
    ![image](https://user-images.githubusercontent.com/106129152/202634271-12bd0851-6e93-4a95-a7c1-9e2e9da046a8.png)
    
    ```python
    #1
    frame2['state'] # frame2.state
    # one        Ohio
    # two        Ohio
    # three      Ohio
    # four     Nevada
    # five     Nevada
    # Name: state, dtype: object
    ```
    
    ```python
    #2
    frame2[['state', 'pop','debt']] # frame2.loc[:, 'state':'debt']
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/202634293-6a5b667a-fc49-4028-8bf9-96c3691eb072.png)
    
    ```python
    #3
    frame2.loc['two'] # frame2.iloc[1]
    # year     2001
    # state    Ohio
    # pop       1.7
    # debt      NaN
    # Name: two, dtype: object
    ```
    
    ```python
    #4
    frame2.loc['two':'four'] # frame2.iloc[1:4] # frame2['two':'four']
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/202634322-7707ee70-cd52-4046-a726-561d674538f9.png)
    
    ```python
    #5
    frame2.loc['three':'four', 'pop':'debt'] # frame2.iloc[2:4, 2:4]
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/202634379-65f006c4-5c9d-4a7c-bdc1-415f4b90ca27.png)
    
    ```python
    #6
    frame2[['pop', 'debt', 'state']]
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/202634406-a2f7dd01-b9e4-479f-b69e-4edacf1f406a.png)
    
    ```python
    #7
    frame2.loc[['three', 'four', 'two']] # frame2.iloc[[2, 3, 1]]
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/202634430-e4ee8301-297c-4fc5-b7d7-0b3883bd297c.png)
    

### 3. 산술 연산과 데이터 정렬

아래와 같이 Series끼리 연산이 가능하다.

```python
s1 = pd.Series([7.3, -2.5, 3.4, 1.5], index=['a', 'c', 'd', 'e'])
s2 = pd.Series([-2.1, 3.6, -1.5, 4, 3.1], index = ['a', 'c', 'e', 'f', 'g'])

s1
# a    7.3
# c   -2.5
# d    3.4
# e    1.5
# dtype: float64

s2
# a   -2.1
# c    3.6
# e   -1.5
# f    4.0
# g    3.1
# dtype: float64

s1 + s2
# a    5.2
# c    1.1
# d    NaN
# e    0.0
# f    NaN
# g    NaN
# dtype: float64
```

DataFrame끼리의 연산도 가능하다.

```python
df1 = pd.DataFrame(np.arange(12).reshape(3, 4), columns = list('abcd'))
df2 = pd.DataFrame(np.arange(20).reshape(4, 5), columns = list('abcde'))
df2.loc[1, 'b'] = np.nan
```

```python
df1
```

![image](https://user-images.githubusercontent.com/106129152/202634486-d774d1db-63a2-4972-95d4-f75fb1d8f04d.png)

```python
df2
```

![image](https://user-images.githubusercontent.com/106129152/202634501-66c1015b-24a6-453d-afa0-8b7bd67819fb.png)

그냥 `df1 + df2` 로도 연산이 가능하지만, 

아래처럼 값이 없는 원소들에게 값을 정해줄 수도 있다.

```python
df1.add(df2, fill_value=0) # 값이 없는 원소들은 0으로 지정을 한 뒤에 add
```

![image](https://user-images.githubusercontent.com/106129152/202634529-c898f7a1-0105-49c8-9025-6e734063c15f.png)

그리고, Series와 DataFrame과의 연산도 가능하다!

```python
frame = pd.DataFrame(np.arange(12.).reshape((4, 3)),
            columns = list('bde'),
            index = ['Utah', 'Ohio', 'Texas', 'Oregon'])

series = frame.iloc[0]
```

```python
frame
```

![image](https://user-images.githubusercontent.com/106129152/202634553-d413d032-0b6e-49e6-add7-4214f783e824.png)

```python
series
# b    0.0
# d    1.0
# e    2.0
# Name: Utah, dtype: float64
```

```python
frame - series # 2차원 - 1차원
```

![image](https://user-images.githubusercontent.com/106129152/202634571-a0700883-d9a8-4c13-8176-6948a4d0cfa5.png)

### 4. 함수 적용과 매핑

```python
frame = pd.DataFrame(np.arange(12).reshape(4,3), columns= list('bde'),
                     index = ["Utah", "Ohio", "Texas", "Oregon"])
frame
```

![image](https://user-images.githubusercontent.com/106129152/202634645-f18e14de-ed11-4292-9c17-f766aa5964dd.png)

```python
# 컬럼별 합계
frame.sum() # pandas에서는 numpy와 다르게 axis=0이 기본값으로 지정
# b    18
# d    22
# e    26
# dtype: int64

# 행별 합계
frame.sum(axis=1) # frame.sum(axis='columns')
# Utah       3
# Ohio      12
# Texas     21
# Oregon    30
# dtype: int64

# 컬럼별 합계
np.sum(frame) # axis=0(행축)을 따라서 합이 계산
# b    18
# d    22
# e    26
# dtype: int64

# 행별 합계
np.sum(frame, axis=1)
# Utah       3
# Ohio      12
# Texas     21
# Oregon    30
# dtype: int64
```

```python
frame.mean()
# b    4.5
# d    5.5
# e    6.5
# dtype: float64

frame.min(axis=0)
# b    0
# d    1
# e    2
# dtype: int32

frame.max(axis=0)
# b     9
# d    10
# e    11
# dtype: int32
```

```python
frame.max(axis=0) - frame.min(axis=0)
# b    9
# d    9
# e    9
# dtype: int32

# 위의 코드를 나만의 함수로 만들어서 적용 (동일한 결과axis=0 이 생략)
def range_f(x): # x는 frame을 행축으로 색인한 series
    return x.max() - x.min()
frame.apply(range_f, axis=0) # axis=0 이 생략

# b    9
# d    9
# e    9
# dtype: int64
```

applymap은 전체 원소에 입력한 함수를 적용한다.

```python
def fmt(x):
    return '%.2f'%x # 소숫점 두자리만 표현

frame.applymap(fmt)
# 람다 함수로 쓰면
# frame.applymap(lambda x: '%.2f'%x)
```

![image](https://user-images.githubusercontent.com/106129152/202634683-1a3b185b-b7a6-4e69-a46f-b19559dc84bf.png)

참고할 사항으로는, 

시리즈 데이터에는 applymap이 적용 불가하기 때문에 map을 사용하면 된다.

```python
frame['b'].map(fmt) # 대신 map을 사용하면 가능
# Utah      0.00
# Ohio      3.00
# Texas     6.00
# Oregon    9.00
# Name: b, dtype: object
```

***🖍Workshop***

```python
import seaborn as sns # seaborn : 시각화 모듈
titanic = sns.load_dataset('titanic') # 데이터를 DataFrame으로 반환
```

```python
# 데이터 훑어보기
titanic.head()
```

![image](https://user-images.githubusercontent.com/106129152/202634709-1419366b-7615-4052-a0b8-793ae324ccf1.png)

- 두 열(age, fare)만 색인해서 DataFrame으로 만들기
    
    ```python
    df = pd.DataFrame(titanic[['age','fare']])
    df
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/202634722-8a2961a9-55c6-47e3-80b4-d677fcff3ff2.png)
    
- 각 열의 최댓값과 최솟값 구하기
    
    ```python
    df.max()
    # age      80.0000
    # fare    512.3292
    # dtype: float64
    
    df.min()
    # age     0.42
    # fare    0.00
    # dtype: float64
    ```
    
- 각 열의 최댓값과 최솟값의 차이 구하기(apply 함수 이용)
    
    ```python
    df.apply(lambda x:x.max() - x.min())
    # age      79.5800
    # fare    512.3292
    # dtype: float64
    ```
    
- 모든 원소의 포맷을 소수점 두자리로 맞추기
    
    ```python
    df.applymap(lambda x: '%.2f'%x)
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/202634743-1873d80b-8334-450c-bf56-95347003ecb1.png)
    
- 누락된 값(NaN)이 있는지 Bool값으로 확인하기
    
    ```python
    df.isnull()
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/202634761-cb4d3e7c-cd17-4c47-bde1-a3fe828e22a6.png)
    

### 5. 정렬

```python
obj = pd.Series(np.arange(4), index=['d', 'a', 'b', 'c'])
obj
# d    0
# a    1
# b    2
# c    3
# dtype: int32

obj.sort_index() # 인덱스를 기준으로 정렬
# a    1
# b    2
# c    3
# d    0
# dtype: int32

obj.sort_values() # 값을 기준으로 정렬
# d    0
# a    1
# b    2
# c    3
# dtype: int32
```

```python
frame = pd.DataFrame(np.arange(8).reshape(2, 4),
                    index = ['three', 'one'],
                    columns = ['d', 'a', 'b', 'c'])
frame
```

![image](https://user-images.githubusercontent.com/106129152/202634813-858f360b-438a-45dc-b6d6-293788ec5dff.png)

```python
frame.sort_index(axis=0) # index 자체를 정렬
```

![image](https://user-images.githubusercontent.com/106129152/202634836-6dffa9ea-e793-48ad-8c6f-89477028aed1.png)

```python
frame.sort_index(axis=1) # column 자체를 정렬
```

![image](https://user-images.githubusercontent.com/106129152/202634891-2a9d38a5-476f-44d4-8060-e8be8c7b6958.png)

```python
frame = pd.DataFrame({'b':[4, 7, -3, 2], 'c':[0, 1, 0, 1]})
frame
```

![image](https://user-images.githubusercontent.com/106129152/202635018-87d8858c-599b-4629-86b6-9eeb3a3562f8.png)

```python
frame.sort_values(by='c', axis=0, ascending=False) # 내림차순 정렬
```

![image](https://user-images.githubusercontent.com/106129152/202635053-5ca53b4d-49c7-40e2-8e39-175dc81bfba3.png)

```python
frame.sort_values(by=['c', 'b'], axis=0) # 계층적으로 정렬
```

![image](https://user-images.githubusercontent.com/106129152/202635072-45d86dea-c464-444f-88bc-11ce4c798f73.png)


### 6. 중복 색인

```python
obj = pd.Series(np.arange(5), index=['a', 'a', 'b', 'b', 'c'])
obj
# a    0
# a    1
# b    2
# b    3
# c    4
# dtype: int32
```

```python
obj.index
# Index(['a', 'a', 'b', 'b', 'c'], dtype='object')

obj.index.is_unique # 인덱스에 중복값이 있기 때문에 False가 나옴
# False

obj['a']
# a    0
# a    1
# dtype: int32

obj['b']
# b    2
# b    3
# dtype: int32
```

```python
df = pd.DataFrame(np.random.randn(4, 3), index=['a', 'a', 'b', 'b'])
df
```

![image](https://user-images.githubusercontent.com/106129152/202635117-d9772ee0-11fe-4ab9-927e-8113ac7b0aa5.png)

```python
df.loc['b']
```

![image](https://user-images.githubusercontent.com/106129152/202635141-52c73ea0-8b82-4ca4-afb3-4eae82915eae.png)

### 7. 기술 통계 계산과 요약

```python
df = pd.DataFrame([[1.4, np.nan], [7.1, -4.5],
                   [np.nan, np.nan], [0.75, -1.3]],
                  index=['a', 'b', 'c', 'd'],
                  columns=['one', 'two'])
df
```

![image](https://user-images.githubusercontent.com/106129152/202635179-fa9c3575-2a63-49ea-a5d9-98e578e21f04.png)

```python
df.sum() # axis=0 기본값
# one    9.25
# two   -5.80
# dtype: float64

df.sum(axis=0, skipna=True) # skipna=True 기본값
# one    9.25
# two   -5.80
# dtype: float64

df.sum(axis=1, skipna=False) # skipna=False 로 설정하면 결측값을 건너뛰지 않음
# a     NaN
# b    2.60
# c     NaN
# d   -0.55
# dtype: float64
```

Numpy : 최댓값과 최솟값의 위치를 구할 때 argmax(), argmin()

Pandas : 최댓값과 최솟값의 위치를 구할 때 idxmax(), idxmin()

```python
df.idxmax() # 행축을 따라서 최댓값의 index
# one    b
# two    d
# dtype: object
```

```python
df.cumsum() # 행축을 따라서 누적합
```

![image](https://user-images.githubusercontent.com/106129152/202635287-088e554e-f524-4b79-baa1-1f15742ac2fd.png)

```python
df.describe() # 값이 숫자만 있는 경우
```

![image](https://user-images.githubusercontent.com/106129152/202635306-1112c0c9-19e4-4e12-a44d-7d200ae1f53e.png)

```python
obj = pd.Series(['a', 'a', 'b', 'c'] * 4)
obj
# 0     a
# 1     a
# 2     b
# 3     c
# 4     a
# 5     a
# 6     b
# 7     c
# 8     a
# 9     a
# 10    b
# 11    c
# 12    a
# 13    a
# 14    b
# 15    c
# dtype: object

obj.describe() # top : 제일 많이 나온 값, freq : 제일 많이 나온 값의 횟수
# count     16
# unique     3
# top        a
# freq       8
# dtype: object
```

describe는 include=’all’로 설정하면 모든 열이 데이터 출력에 포함된다.

→ [describe() 메서드](https://kongdols-room.tistory.com/172) 

## **기술 통계**

기술 통계는 수집한 데이터를 수치나 표, 그래프 등으로 정리하여 

데이터 전체가 나타내는 경향이나 성질을 파악하는 방법이다.

어떤 집단을 구성하는 것의 특성을 수치로 표현한 값 : **변량**

변량의 관측값이나 측정값을 모은 것 : **데이터**

[Numpy 기술 통계](https://datascienceschool.net/01%20python/03.04%20%EA%B8%B0%EC%88%A0%20%ED%86%B5%EA%B3%84.html)

[기술 통계란?](https://computer-science-student.tistory.com/167)

**질적 데이터 (범주형 데이터)** : 셀 수 없는 변량으로 이루어진 데이터

**양적 데이터** : 이산형 데이터와 연속형 데이터로 나뉨. 

- **이산형 데이터** : ****띄엄띄엄 떨어진 값을 갖는 데이터
- **연속형 데이터** : 연속하는 값을 갖는 데이터

**분포** : 데이터가 흩어진 정도

→ 대푯값(다섯수요약), 상자수염도, 분산, 표준편차와 같은 통계량이 있음

**도수분포표** : 데이터가 흩어진 정도를 파악

**히스토그램** : 데이터분포를 직관적으로 이해하기 쉽도록 막대그래프로 나타낸 그림

**데이터의 대푯값 :** 

평균값 (mean)

중앙값 (median)

최빈값 (mode) *- 가장 개수가 많은 값*

**사분위수** : 데이터 전체를 큰 순서로 나열했을 때 4등분하는 세 수

→ 작은 순서대로 1사분위수, 2사분위수(=데이터 전체의 중앙값), 3사분위수

일단 이정도로 간략한 용어정리만 하고 차차 배워가면서 알아가기로 하자😊
