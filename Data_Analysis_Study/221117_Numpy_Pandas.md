> 부트캠프 5주차 2022년 11월 17일

## **Numpy - 그 외 기능들**

### ****3.1 배열 전치****

```python
arr = np.arange(15).reshape(3, 5) # 3행 5열의 행렬이 준비
arr
# array([[ 0,  1,  2,  3,  4],
#        [ 5,  6,  7,  8,  9],
#        [10, 11, 12, 13, 14]])
```

위와 같이 3행 5열의 행렬을 준비했다. 

여기에 Numpy의 **T** 속성을 사용하면 *전치(Transpose) 변환*을 할 수 있다.

[이 링크](https://newprivatemarine.tistory.com/80)를 참고하면 전치연산과 전치행렬에 대해 이해할 수 있다.

```python
arr.T # 5행 3열로 바뀜 (전치행렬)
# array([[ 0,  5, 10],
#        [ 1,  6, 11],
#        [ 2,  7, 12],
#        [ 3,  8, 13],
#        [ 4,  9, 14]])
```

```python
arr * arr # 개별 원소의 곱셈
# array([[  0,   1,   4,   9,  16],
#        [ 25,  36,  49,  64,  81],
#        [100, 121, 144, 169, 196]])

# 행렬의 곱셈
# arr @ arr 연산은 가능하지 않음 (@은 행렬의 곱셈)
# (3, 5) @ (3, 5)

# arr @ arr.T 연산은 가능
# (3, 5) @ (5, 3) = (3, 3)

arr @ arr.T
# array([[ 30,  80, 130],
#        [ 80, 255, 430],
#        [130, 430, 730]])

np.dot(arr, arr.T) # .dot() : 행렬 내적 (dot product)
# array([[ 30,  80, 130],
#        [ 80, 255, 430],
#        [130, 430, 730]])
```

[여기](https://namu.wiki/w/%ED%96%89%EB%A0%AC%EA%B3%B1)를 보면 행렬곱에 대해 상당히 자세한 설명이 되어있다.

위 링크의 개요만 이해해도 된다! 

### ****3.2 배열 연산과 조건절 표현하기****

```python
# 파이썬
x_list = [1, 2, 3, 4]
y_list = [5, 6, 7, 8]
cond_list = [True, True, False, False]

result = []
for x, y, c in zip(x_list, y_list, cond_list): # 4번 순회
    if c:
        result.append(x)
    else:
        result.append(y)
result
# [1, 2, 7, 8]
```

```python
# 넘파이
x_arr = np.array([1, 2, 3, 4])
y_arr = np.array([5, 6, 7, 8])
cond_arr = np.array([True, True, False, False])

# np.where(조건, 조건이 참일 때, 조건이 거짓일 때)
result = np.where(cond_arr, x_arr, y_arr) 
result # x_arr의 True 값과 y_arr의 False값이 나옴
# array([1, 2, 7, 8])
```

보이는 것과 같이, 파이썬만으로 값을 구하려면 반복문을 사용해야 하지만 

넘파이를 사용하면 한 줄로 해결이 된다.

```python
arr = np.arange(16).reshape((4,4))
arr
# array([[ 0,  1,  2,  3],
#        [ 4,  5,  6,  7],
#        [ 8,  9, 10, 11],
#        [12, 13, 14, 15]])
```

arr이라는 4행 4열의 행렬을 준비했다.

그리고 아래와 같은 연산이 가능하다.

```python
arr > 10
# array([[False, False, False, False],
#        [False, False, False, False],
#        [False, False, False,  True],
#        [ True,  True,  True,  True]])

cond = arr > 10
result = np.where(cond, 1, -1)
result # arr이 10보다 작으면 1, 10보다 크면 -1로
# array([[-1, -1, -1, -1],
#        [-1, -1, -1, -1],
#        [-1, -1, -1,  1],
#        [ 1,  1,  1,  1]])
```

```python
arr < 10
# array([[ True,  True,  True,  True],
#        [ True,  True,  True,  True],
#        [ True,  True, False, False],
#        [False, False, False, False]])

cond = arr < 10
result = np.where(cond, -1, arr)
result # arr가 10보다 작으면 -1, 10보다 크면 그대로
# array([[-1, -1, -1, -1],
#        [-1, -1, -1, -1],
#        [-1, -1, 10, 11],
#        [12, 13, 14, 15]])
```

### ****3.3 수학 통계 메서드****

![image](https://user-images.githubusercontent.com/106129152/202394870-61ea3c81-9a8b-4e50-a8e9-114dea8ac358.png)

```python
arr = np.arange(20).reshape((5, 4))
arr
# array([[ 0,  1,  2,  3],
#        [ 4,  5,  6,  7],
#        [ 8,  9, 10, 11],
#        [12, 13, 14, 15],
#        [16, 17, 18, 19]])
```

5행 4열의 arr을 준비하고, 위의 메서드를 사용해보자.

```python
np.sum(arr) # arr.sum() 과 동일
# 190

np.sum(arr, 0) # arr.sum(0) 과 동일, 0번축(행축)을 따라서 합산
# array([40, 45, 50, 55])

np.sum(arr, 1) # 1번축(열축)을 따라서 합산
# array([ 6, 22, 38, 54, 70])

np.mean(arr, 0) # arr.mean(0)
# array([ 8.,  9., 10., 11.])

arr.min(0)
# array([0, 1, 2, 3])

arr.min(1)
# array([ 0,  4,  8, 12, 16])

arr.cumsum(0) # 누적합
# array([[ 0,  1,  2,  3],
#        [ 4,  6,  8, 10],
#        [12, 15, 18, 21],
#        [24, 28, 32, 36],
#        [40, 45, 50, 55]])

arr.cumprod(1) # 누적곱
# array([[    0,     0,     0,     0],
#        [    4,    20,   120,   840],
#        [    8,    72,   720,  7920],
#        [   12,   156,  2184, 32760],
#        [   16,   272,  4896, 93024]])
```

### ****3.4 불리언 배열 메서드****

```python
bool_arr = np.array([True, False, True])
bool_arr
# array([ True, False,  True])

bool_arr.all() # 모두 True 여야 True
# False

bool_arr.any() # 하나라도 True면 True
# True
```

```python
arr = np.arange(16).reshape((2, 8))
arr
# array([[ 0,  1,  2,  3,  4,  5,  6,  7],
#        [ 8,  9, 10, 11, 12, 13, 14, 15]])

bool_arr2 = arr < 8
bool_arr2
# array([[ True,  True,  True,  True,  True,  True,  True,  True],
#        [False, False, False, False, False, False, False, False]])

bool_arr2.all(1)
# array([ True, False])

bool_arr2.any(0)
# array([ True,  True,  True,  True,  True,  True,  True,  True])
```

### ****3.5 정렬****

```python
arr = np.random.randn(3, 4) # numpy에서 제공하는 표준정규분포를 따르는 무작위수를 지정한 사이즈로 만들어줌
arr
# array([[-0.85372035,  0.31349008,  0.32138989, -0.199782  ],
#        [ 0.68252071, -0.36220123, -1.83367006, -2.1748366 ],
#        [-1.3460748 , -1.59569023, -0.71832656, -0.05398212]])

np.sort(arr, 1) # arr에 반영되지 않음
# array([[-0.85372035, -0.199782  ,  0.31349008,  0.32138989],
#        [-2.1748366 , -1.83367006, -0.36220123,  0.68252071],
#        [-1.59569023, -1.3460748 , -0.71832656, -0.05398212]])

arr.sort(1) # arr에 반영됨
arr
# array([[-0.85372035, -0.199782  ,  0.31349008,  0.32138989],
#        [-2.1748366 , -1.83367006, -0.36220123,  0.68252071],
#        [-1.59569023, -1.3460748 , -0.71832656, -0.05398212]])
```

### ****3.6 집합 관련 함수****

```python
# 파이썬의 리스트
fruits_list = ["strawbery", "strawbery", "pear", "apple"] 
fruits_list
# ['strawbery', 'strawbery', 'pear', 'apple']

set(fruits_list) # 파이썬의 집합
# {'apple', 'pear', 'strawbery'}

# 넘파이
fruits_array = np.array(["strawbery", "strawbery", "pear", "apple"])
fruits_array
# array(['strawbery', 'strawbery', 'pear', 'apple'], dtype='<U9')

np.unique(fruits_array)
# array(['apple', 'pear', 'strawbery'], dtype='<U9')
```

Numpy의 unique 함수를 사용하면 고유한 값들만 모아서 반환해준다.

### ****3.7 난수 생성****

![image](https://user-images.githubusercontent.com/106129152/202394936-2f0b1613-24d0-4492-87bd-d28f88cd5c82.png)

*참고 → [정규분포](https://ko.khanacademy.org/math/statistics-probability/modeling-distributions-of-data/normal-distributions-library/a/normal-distributions-review)*

- 정규 분포에서 표본을 추출
    
    ```python
    samples = np.random.normal(size=1000, loc=10, scale=1) # 사이즈, 평균, 표준편차
    
    samples.mean() # 평균값
    # 9.979490656744959
    
    samples.std() # 표준편차
    # 0.993948544014064
    ```
    
    더 와닿을 수 있게 matplotlib을 사용해서 눈으로 확인해보자.
    
    ```python
    import matplotlib.pyplot as plt
    plt.hist(samples)
    # 정규분포의 형태를 띄는 것을 볼 수 있다
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/202394991-0219373d-25d7-4eb1-a6d0-bd06e962bc31.png)
    
- 표준 정규 분포에서 표본을 추출
    
    ```python
    samples = np.random.randn(1000)
    
    samples.mean(), samples.std() # 평균 0, 표준편차 1
    # (0.022248374881031957, 1.0046080256825007)
    ```
    
- 최대, 최소 범위에서 난수 생성
    
    ```python
    # 주사위 던지기 (50회)
    for i in range(50):
        draw = np.random.randint(1, 7)
        print(draw, end=' ')
    
    # 1 1 2 2 4 4 4 1 1 6 2 2 6 3 3 4 1 6 5 6 3 5 6 4 6 4 2 3 2 1 1 2 1 6 4 1 6 3 2 1 5 4 2 3 3 1 6 3 5 6
    
    # 반복문 없이 주사위 던지기 50회 시뮬레이션
    np.random.randint(1, 7, 50)
    # array([5, 6, 6, 2, 2, 3, 2, 3, 4, 4, 6, 6, 1, 3, 3, 5, 3, 6, 3, 5, 6, 3,
    #        2, 5, 2, 2, 2, 1, 6, 5, 2, 6, 2, 6, 1, 1, 6, 6, 1, 3, 1, 1, 6, 1,
    #        4, 4, 4, 2, 3, 4])
    ```
    
    ```python
    arr = np.arange(16)
    p = np.random.permutation(arr) # permutation : 순열
    p.reshape(4, 4) # 4팀을 무작위로
    # array([[ 8,  3, 14,  7],
    #        [ 1,  0,  2,  5],
    #        [11,  4,  9, 13],
    #        [12,  6, 10, 15]])
    ```
    

### 🖍***Workshop***

**문제 1 ) 1~45개의 번호 중 무작위로 6개씩 생성되는 번호 세트를 총 10개 출력하기**

```python
for i in range(10):
    arr = np.arange(1, 46)
    draw = np.random.permutation(arr)
    print(draw[:6])

# [36 21 31  1 18 16]
# [13 15 32 20  8 42]
# [ 2 29 41 33 45 22]
# [35 33 19 37  3 38]
# [37 44 25 27 24  1]
# [14 22 21  3 45 33]
# [19 36 40 18 16 38]
# [31 40 36 24 38  2]
# [44  1 33 17  6 34]
# [14 11 27 38  7 24]
```

**문제 2 ) 계단 오르내리기**

- 동전을 던졌을 때 앞이 나오면 계단 1칸 올라가기
- 동전을 던졌을 때 뒤가 나오면 계단 1칸 내려가기
- 현재 위치 position
- 동전을 1000번 던졌을 때 위치의 히스토리: walk 리스트

*파이썬의 random 모듈 사용→*

```python
import random

position = 0 # 계단 1칸 오르게 되면 +1, 내려가게 되면 -1
steps = 1000

walk = [position] # [0, 1, 0, -1, -2, -3, -2, -1, -2...] 

step = 0
for i in range(steps):
    draw = random.randint(0, 1) 
    if draw == 1: # 동전의 앞
        step = 1
    else:
        step = -1
    position += step
    walk.append(position)
```

```python
walk[:20]
# [0, -1, 0, -1, 0, -1, 0, 1, 2, 3, 4, 5, 4, 3, 4, 3, 4, 5, 4, 5]

walk[-1]
# -34

plt.plot(walk)
```

![image](https://user-images.githubusercontent.com/106129152/202395074-8b320161-fef7-44ba-8626-5f2848fd121a.png)

*for문을 사용하지 않고 Numpy로 구현 →*

```
np.random.randint() : 동전의 앞뒤 결정
np.where() : 동전의 앞뒤 조건에 따른 step 결정
np.cumsum() : 현재 위치의 히스토리
```

```python
steps = 1000
draws = np.random.randint(0, 2, steps)

cond = draws > 0
step_arr = np.where(cond, 1, -1)
walk = step_arr.cumsum()

plt.plot(walk)
```

![image](https://user-images.githubusercontent.com/106129152/202395111-06b09e79-b49b-4868-ab38-4a717a1c3d16.png)

```python
walk.min(), walk.max()
# (-37, 13)

walk.argmin(), walk.argmax() # 최소값의 인덱스, 최대값의 인덱스
# (894, 296)
```

argmax()를 사용해서 아래와 같은 질문도 답할 수 있다.

결과는 289가 나왔다.

```python
# 처음 위치에서 10계단 이상 올라가는데 걸린 횟수

bool_arr = walk >= 10
np.argmax(bool_arr) # False는 0, True는 1 로 간주
                    # argmax() 최대값(1)이 최초로 등장한 index
                    # 처음 위치에서 10계단 이상 올라가는데 289번의 동전을 던짐
```

## Pandas

### ****Pandas 개요****

- pandas는 for문을 사용하지 않고 데이터를 처리한다거나 배열 기반의 함수를 제공하는 등 NumPy의 배열 기반 계산 스타일을 많이 차용
- pandas가 NumPy 스타일을 많이 차용했지만 가장 큰 차이점은 **pandas는 표 형식의 데이터나 다양한 형태의 데이터를 다루는 데 초점**을 맞춰 설계
- 그에 비해 NumPy는 단일 산술 배열 데이터를 다루는 데 특화
- 고수준의 자료구조를 제공하고 파이썬 생태계 내의 다른 분석 라이브러리 등과 함께 사용

*→ [판다스 사용법 알아보기](https://laboputer.github.io/machine-learning/2020/04/07/pandas-10minutes/)*

### 1. Pandas 자료구조

```python
import pandas as pd
import numpy as np
```

****1.1 Series**** *- 1차원 데이터*

Pandas의 Series는 1차원 데이터와 인덱스로 이루어져 있다.

인덱스에 아무런 값도 넣지 않으면 자동으로 0부터 할당된다.

```python
obj = pd.Series([4, 7, -5, 3])
obj
# 0    4
# 1    7
# 2   -5
# 3    3
# dtype: int64

obj.values
# array([ 4,  7, -5,  3], dtype=int64)

obj.index
# RangeIndex(start=0, stop=4, step=1)

type(obj)
# pandas.core.series.Series
```

이번에는 인덱스에 값을 넣어보자.

```python
obj2 = pd.Series([4, 7, -5, 3], index=['d', 'b', 'a', 'c'])
obj2
# d    4
# b    7
# a   -5
# c    3
# dtype: int64

obj2.values
# array([ 4,  7, -5,  3], dtype=int64)

obj2.index
# Index(['d', 'b', 'a', 'c'], dtype='object')
```

다양한 색인도 가능하다.

```python
obj2['d'] # 라벨 이름으로 색인
# 4

obj2[0] # 정수로 색인
# 4

obj2[[0, 1, 3]] # 팬시 색인 (정수)
# d    4
# b    7
# c    3
# dtype: int64

obj2[['d', 'b', 'c']] # 팬시 색인 (라벨)
# d    4
# b    7
# c    3
# dtype: int64

obj2 > 0
# d     True
# b     True
# a    False
# c     True
# dtype: bool

obj2[obj2 > 0] # 불리안 색인
# d    4
# b    7
# c    3
# dtype: int64
```

```python
obj2 * 2 # 브로드캐스팅
# d     8
# b    14
# a   -10
# c     6
# dtype: int64

np.exp(obj2) # 유니버설 함수
# d      54.598150
# b    1096.633158
# a       0.006738
# c      20.085537
# dtype: float64
```

딕셔너리, 리스트, 튜플 등을 시리즈로 변환할 수도 있다!

```python
sdata = {'Ohio':3500, 'Texas':71000, 'Oregon':16000, 'Utah':5000}
obj3 = pd.Series(sdata)
obj3
# Ohio       3500
# Texas     71000
# Oregon    16000
# Utah       5000
# dtype: int64

states = ['California', 'Ohio', 'Oregon', 'Texas']
obj4 = pd.Series(sdata, index=states)
obj4 # NaN : Not a Number
# California        NaN
# Ohio           3500.0
# Oregon        16000.0
# Texas         71000.0
# dtype: float64
```

Null 값을 찾는 것도 가능하다. 

Missing Data, 결측 데이터를 판다스에서는 NaN으료 표현한다.

```python
pd.isnull(obj4) # obj4.isnull()
# California     True
# Ohio          False
# Oregon        False
# Texas         False
# dtype: bool

pd.isnull(obj4).sum() # null인 항목의 합
# 1

pd.notnull(obj4)
# California    False
# Ohio           True
# Oregon         True
# Texas          True
# dtype: bool
```

시리즈의 이름이나, 인덱스의 이름을 정할 수도 있다.

```python
obj4.name = 'population'
obj4
# California        NaN
# Ohio           3500.0
# Oregon        16000.0
# Texas         71000.0
# Name: population, dtype: float64

obj4.index.name = 'state'
obj4
# state
# California        NaN
# Ohio           3500.0
# Oregon        16000.0
# Texas         71000.0
# Name: population, dtype: float64
```

```python
obj
# 0    4
# 1    7
# 2   -5
# 3    3
# dtype: int64

obj.index = ['Bob', 'Steve', 'Jeff', 'Ryan']
obj
# Bob      4
# Steve    7
# Jeff    -5
# Ryan     3
# dtype: int64
```

### 🖍***Workshop***

**문제 1 )** 딕셔너리 → 시리즈 변환 (index, values 출력)

```python
dict_data = {'a':1, 'b':2, 'c':3}

dictS = pd.Series(dict_data)
dictS.index, dictS.values
# (Index(['a', 'b', 'c'], dtype='object'), array([1, 2, 3], dtype=int64))
```

**문제 2 )** 리스트 → 시리즈 변환 (index, values 출력)

```python
list_data = ['2019-01-02', 3.14, 'ABC', 100, True]

listS = pd.Series(list_data)
listS.index, listS.values
# (RangeIndex(start=0, stop=5, step=1),
#  array(['2019-01-02', 3.14, 'ABC', 100, True], dtype=object))
```

**문제 3 )** 튜플 → 시리즈 변환 (index, values 출력)

```python
tuple_data = ('영인', '2010-05-01', '여', True)

tupleS = pd.Series(tuple_data)
tupleS.index, tupleS.values
# (RangeIndex(start=0, stop=4, step=1),
#  array(['영인', '2010-05-01', '여', True], dtype=object))
```

**문제 3-1 )** 튜플 → 시리즈 변환 (index 설정)

```python
tuple_data = ('영인', '2010-05-01', '여', True)
index_name = ['이름', '생년월일', '성별', '학생여부']

tupleS = pd.Series(tuple_data, index_name)
tupleS
# 이름              영인
# 생년월일    2010-05-01
# 성별               여
# 학생여부          True
# dtype: object

# 색인을 통해 '영인'값이 나오도록
tupleS['이름']
# '영인'
tupleS[0]
# '영인'

# 슬라이스 색인을 통해 '2010-05-01', '여' 값이 나오도록
tupleS[1:3]
# 생년월일    2010-05-01
# 성별               여
# dtype: object

tupleS['생년월일':'성별']
# 생년월일    2010-05-01
# 성별               여
# dtype: object
```

****1.2 DataFrame**** *- 2차원 데이터*

```python
data = {'state':['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'], 
        'year':[2000, 2001, 2002, 2001, 2002, 2003], 
        'pop':[1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}
frame = pd.DataFrame(data)
frame
```

![image](https://user-images.githubusercontent.com/106129152/202395241-a0e24f23-5016-4f94-888d-ff62631185cd.png)

```python
frame.index
# RangeIndex(start=0, stop=6, step=1)

frame.columns
# Index(['state', 'year', 'pop'], dtype='object')

frame.values
# array([['Ohio', 2000, 1.5],
#        ['Ohio', 2001, 1.7],
#        ['Ohio', 2002, 3.6],
#        ['Nevada', 2001, 2.4],
#        ['Nevada', 2002, 2.9],
#        ['Nevada', 2003, 3.2]], dtype=object)

type(frame)
# pandas.core.frame.DataFrame
```

```python
frame.head() # 전체 데이터 중 앞에서부터 5행만 보여줌
```

![image](https://user-images.githubusercontent.com/106129152/202395290-a0f054e6-9fe5-4c4c-b5cb-0c81dfa48654.png)

```python
frame.tail() # 전체 데이터 중 뒤에서부터 5행만 보여줌
```

![image](https://user-images.githubusercontent.com/106129152/202395342-8333ac56-e591-4c86-ad87-a23d7bdcffa2.png)

컬럼의 순서를 바꿔도 값이 변하지 않는다.

```python
pd.DataFrame(data, columns = ['year', 'state', 'pop'])
```

![image](https://user-images.githubusercontent.com/106129152/202395382-c1514457-50be-4989-85c8-ea9a9f2940a7.png)

값이 없는 컬럼을 추가하면 아래처럼 NaN으로 채워진 컬럼이 생긴다.

```python
pd.DataFrame(data, columns = ['year', 'state', 'pop', 'debt'])
```

![image](https://user-images.githubusercontent.com/106129152/202395433-eea55013-4f64-4b00-b62d-c9baaa2900c8.png)

이번에는 인덱스 값을 추가해보자.

```python
frame2 = pd.DataFrame(data, columns = ['year', 'state', 'pop', 'debt'],
                     index = ['one', 'two', 'three', 'four', 'five', 'six'])
```

![image](https://user-images.githubusercontent.com/106129152/202395474-adcea367-b65e-4425-9e55-aa91ed519219.png)

```python
frame2.columns
# Index(['year', 'state', 'pop', 'debt'], dtype='object')

frame2.index
# Index(['one', 'two', 'three', 'four', 'five', 'six'], dtype='object')
```

**(1) 열 색인**

```python
frame2['state'] # 2차원 데이터인 DataFrame을 색인하면 1차원 데이터인 Series
# one        Ohio
# two        Ohio
# three      Ohio
# four     Nevada
# five     Nevada
# six      Nevada
# Name: state, dtype: object
```

**(2) 행 색인**

```python
frame2.loc['one'] # 1차원 Series 데이터
# year     2000
# state    Ohio
# pop       1.5
# debt      NaN
# Name: one, dtype: object
```

```python
frame2.loc['one':'two'] # 슬라이싱을 통해서 행을 가져올 때는 loc를 생략해도 가능
```

![image](https://user-images.githubusercontent.com/106129152/202395519-1093f7e1-cb72-4f4b-b058-7d5bb2a4a686.png)

이번에는 debt에 값을 넣어보는 여러가지 방법을 살펴보자.

```python
frame2['debt'] = 16.5 # 브로드캐스팅
frame2
```

![image](https://user-images.githubusercontent.com/106129152/202395578-00dbb2fc-dd3e-4623-82c7-188bc044ec29.png)

```python
frame2['debt'] = np.arange(6)
frame2
```

![image](https://user-images.githubusercontent.com/106129152/202395622-876f2ad6-5ab3-45be-9282-7d34d37fe391.png)

```python
sr = pd.Series([1, 2, 3, 4, 5, 6], index=['one', 'two', 'three', 'four', 'five', 'six'])
frame2['debt'] = sr
frame2
```

![image](https://user-images.githubusercontent.com/106129152/202395701-06c8536a-4bd4-4029-b853-7648025d6df3.png)

```python
sr = pd.Series([1, 3, 5], index=['one', 'three', 'five'])
frame2['debt'] = sr
frame2
```

![image](https://user-images.githubusercontent.com/106129152/202395735-77c79d22-841a-4b97-8e43-81e4d5ca3b40.png)

```python
pop = {'Nevada':{2001:2.4, 2002:2.9},
          'Ohio':{2000:1.5, 2001:1.7, 2002:3.6}}
frame3 = pd.DataFrame(pop)
frame3
```

![image](https://user-images.githubusercontent.com/106129152/202395779-4d9cc2c1-ef27-463d-87fe-f4769ee93210.png)

```python
frame3.T
```

![image](https://user-images.githubusercontent.com/106129152/202395835-e27bd418-02bd-4c75-a5f9-a28728b626ca.png)

index와 columns의 이름도 정할 수 있다.

```python
frame3.index.name = 'year'
frame3.columns.name = 'state'
frame3
```

![image](https://user-images.githubusercontent.com/106129152/202395877-3d859b6e-835b-495e-b7f0-933c699703ac.png)

****1.3 Index****

컬럼명, 인덱스 (데이터과 행과 열을 알려주는 메타 데이터)

```python
obj = pd.Series(range(3), index=['a', 'b', 'c'])
obj
# a    0
# b    1
# c    2
# dtype: int64

obj.index
# Index(['a', 'b', 'c'], dtype='object')

obj.index[:2]
# Index(['a', 'b'], dtype='object')

obj.index[1]
# 'b'

# Index 객체 만들기
labels = pd.Index(np.arange(3))
pd.Series([1, 2, 3], index = labels)
# 0    1
# 1    2
# 2    3
# dtype: int64
```

### 🖍***Workshop***

**문제 1 )** 딕셔너리 -> 데이터프레임

```python
dict_data = {'c0':[1,2,3], 'c1':[4,5,6], 'c2':[7,8,9], 'c3':[10,11,12], 'c4':[13,14,15]}

dict_df = pd.DataFrame(dict_data)
```

**문제 2 )** 행 인덱스/열 이름 설정

```python
df = pd.DataFrame([[15, '남', '덕영중'], [17, '여', '수리중']], 
                   index=['준서', '예은'],
                   columns=['나이', '성별', '학교'])

# 준서, 예은 -> 학생1, 학생2
df.index = ['학생1', '학생2']

# 나이, 성별, 학교 -> 연령, 남녀, 소속
df.columns = ['연령', '남녀', '소속']

# 행인덱스/열이름 변경
# rename 사용하여 변경 (부분적으로 수정하고 싶을 때)
df.rename(index = {'준서':'학생1', '예은':'학생2'}, 
          columns = {'나이':'연령', '성별':'남녀', '학교':'소속'},
          inplace = True)
```

### ****2. 중요한 기능들****

****2.1 재색인****

```python
sr = pd.Series([1, 2, 3, 4], index=[0, 3, 4, 5])
sr
# 0    1
# 3    2
# 4    3
# 5    4
# dtype: int64

np.arange(6)
# array([0, 1, 2, 3, 4, 5])

sr.reindex(np.arange(6))
# 0    1.0
# 1    NaN
# 2    NaN
# 3    2.0
# 4    3.0
# 5    4.0
# dtype: float64
```

bfill : 결측값을 바로 아래 값과 동일하게 변경

ffill : 결측값을 바로 위 값과 동일하게 변경

```python
sr.reindex(np.arange(6), method='bfill') # back fill
# 0    1
# 1    2
# 2    2
# 3    2
# 4    3
# 5    4
# dtype: int64

sr.reindex(np.arange(6), method='ffill') # forward fill
# 0    1
# 1    1
# 2    1
# 3    2
# 4    3
# 5    4
# dtype: int64
```

****2.2 로우나 컬럼 삭제하기****

Series의 경우 

```python
obj = pd.Series(np.arange(5), index=['a', 'b', 'c', 'd', 'e'])
obj
# a    0
# b    1
# c    2
# d    3
# e    4
# dtype: int32

obj.drop('c')
# a    0
# b    1
# d    3
# e    4
# dtype: int32

obj.drop(['c', 'd'])
# a    0
# b    1
# e    4
# dtype: int32
```

DataFrame의 경우

```python
data = pd.DataFrame(np.arange(16).reshape(4, 4),
                   index = ['Ohio', 'Colorado', 'Utah', 'New York'],
                   columns = ['one', 'two', 'three', 'four'])
data
```

![image](https://user-images.githubusercontent.com/106129152/202395997-b98a7266-27fe-4396-96bf-ede9d2b8d9f8.png)

```python
# axis=0 (행축), axis=1(열축)
# (1) drop 연산을 할 경우에는 지정된 "축"을 삭제
# (2) 통계/수학 메서드(sum, mean, ...)를 사용할 때는 "축"을 따라서 계산

# 아래 코드는 모두 동일한 결과
# data.drop('Colorado')
# data.drop('Colorado', axis=0) # axis=0 이 디폴트값
data.drop('Colorado', axis='index') # 행축을 삭제
```

![image](https://user-images.githubusercontent.com/106129152/202396041-b419bab5-ebc7-4696-adda-aeabbdb13432.png)

```python
# data.drop('two', axis=1)
data.drop('two', axis='columns')
```

![image](https://user-images.githubusercontent.com/106129152/202396096-5a469e2d-8940-42d5-ae31-daaba8bf0b1f.png)

```python
data.drop(['two', 'four'], axis='columns')
```

![image](https://user-images.githubusercontent.com/106129152/202396122-943f3fa3-4b55-4f8d-93b0-9d22d8a68f4b.png)

****2.3 색인하기, 선택하기, 거르기****

```python
data = pd.DataFrame(np.arange(16).reshape(4, 4),
                   index = ['Ohio', 'Colorado', 'Utah', 'New York'],
                   columns = ['one', 'two', 'three', 'four'])
data
```

![image](https://user-images.githubusercontent.com/106129152/202396159-49c3b9a7-2a10-4d60-8e83-ed7981fe9c5e.png)

```python
data['two'] # data.two 와 동일
# Ohio         1
# Colorado     5
# Utah         9
# New York    13
# Name: two, dtype: int32
```

```python
data[['two', 'four']]
```

![image](https://user-images.githubusercontent.com/106129152/202396196-f7cbae96-c5ab-4c46-8eea-2fc9e3b80ff7.png)

```python
data[data < 5]
```

![image](https://user-images.githubusercontent.com/106129152/202396235-c5e0b5b4-cf7e-480b-8e9b-8efb632913f7.png)

- loc, iloc
    
    ```python
    data.loc['Colorado']['one'] # 라벨 색인
    # 4
    
    data.iloc[1][0] # 정수 색인
    # 4
    ```
    
    ```python
    data.loc['Colorado']['one':'three']
    # one      4
    # two      5
    # three    6
    # Name: Colorado, dtype: int32
    
    data.loc['Colorado'][['one', 'three']] # data.loc['Colorado', ['one', 'three']] 와 동일
    # one      4
    # three    6
    # Name: Colorado, dtype: int32
    
    data.iloc[1, [0, 2]]
    # one      4
    # three    6
    # Name: Colorado, dtype: int32
    ```
    
    ```python
    data.loc[:'Utah'] # data.iloc[:3] 와 동일
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/202396300-b2ece296-11e4-479c-95de-244c2ca78204.png)
