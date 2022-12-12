> 부트캠프 2주차 2022년 10월 24일

## 예외 처리하기
예외란, 실행 중에 감지되는 에러들을 말한다.   
예외 처리는 **에러가 발생하더라도 스크립트 실행을 중단하지 않고 계속 실행하고자 할 때** 사용한다.
```
try:
    실행할 코드
except:
    예외가 발생했을 때 처리할 코드
```
```python
try:
    x = int(input("나눌 숫자를 입력하세요: "))
    y = 10/x 
    print(y)
except:
    print("예외가 발생했습니다.")
    x = int(input("0이 아닌 숫자를 다시 입력해주세요: "))
    y = 10/x 
    print(y)

'''
나눌 숫자를 입력하세요: 0
예외가 발생했습니다.
0이 아닌 숫자를 다시 입력해주세요: 5
2.0
'''
```
   
- 특정 예외만 처리하기
```python
try:
    실행할 코드
except 예외 이름1:
    예외가 발생했을 때 처리할 코드
except 예외 이름2:
    예외가 발생했을 때 처리할 코드
```
```python
try: 
    x = int(input("나눌 숫자를 입력하세요: "))
    y = 10/x 
    print(y)
except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")

'''
나눌 숫자를 입력하세요: 0
0으로 나눌 수 없습니다.
'''
```
→ 이렇게 except 에 ZeroDivisionError 라는 특정 예외를 지정할 수 있다. 
```python
y = [10, 20, 30]

try: 
    index, x = map(int, input("인덱스와 나눌 숫자를 입력하세요: ").split())
    y = y[index]/x
    print(y)
except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")
except IndexError:
    print("잘못된 인덱스입니다.")

'''
인덱스와 나눌 숫자를 입력하세요: 3 0
잘못된 인덱스입니다.
'''
```
파이썬 자습서에서 [**에러와 예외에 대한 설명**](https://docs.python.org/ko/3/tutorial/errors.html?highlight=%EC%98%88%EC%99%B8)을 참고하면 좋다.   
[**구체적인 예외**](https://docs.python.org/ko/3/library/exceptions.html#concrete-exceptions)들도 나열되어 있다.   
   
- 예외 메세지 출력하기
```python
try:
    실행할 코드
except 예외 이름 as 변수:
    예외가 발생했을 때 처리할 코드
```
```python
y = [10, 20, 30]

try: 
    index, x = map(int, input("인덱스와 나눌 숫자를 입력하세요: ").split())
    y = y[index]/x
    print(y)    
except ZeroDivisionError as e:
    print("0으로 나눌 수 없습니다.", e)    
except IndexError as e:
    print("잘못된 인덱스입니다.", e)

'''
인덱스와 나눌 숫자를 입력하세요: 3 2
잘못된 인덱스입니다. list index out of range
'''
```
이렇게 변수에 예외 메세지를 담아서 출력시킬 수도 있다.   
   
- 예외 발생 여부에 따라 분기 
```python
try:
    실행할 코드
except 예외 이름 as 변수:
    예외가 발생했을 때 처리할 코드
else:
    예외가 발생하지 않았을 때 실행할 코드
```
```python
y = [10, 20, 30]

try: 
    index, x = map(int, input("인덱스와 나눌 숫자를 입력하세요: ").split())
    y = y[index]/x # <-- 문제가 생겼을 때 예외가 발생하는 위치    
except ZeroDivisionError as e:
    print("0으로 나눌 수 없습니다.", e)    
except IndexError as e:
    print("잘못된 인덱스입니다.", e)
else: 
    print(y) # <-- 예외가 발생하지 않을 시 연산 결과를 출력

'''
인덱스와 나눌 숫자를 입력하세요: 0 2
5.0
'''
```
→ else를 추가해 예외가 발생하지 않았을 때 실행할 코드를 작성할 수 있다.   
   
- 예외 발생 여부와 상관없이 처리 (*finally*)
```python
try:
    실행할 코드
except 예외 이름 as 변수:
    예외가 발생했을 때 처리할 코드
else:
    예외가 발생하지 않았을 때 실행할 코드
finally:
    예외 발생 여부와 상관없이 항상 실행할 코드
```
```python
y = [10, 20, 30]

try: 
    index, x = map(int, input("인덱스와 나눌 숫자를 입력하세요: ").split())
    y = y[index]/x 
except ZeroDivisionError as e:
    print("0으로 나눌 수 없습니다.", e)   
except IndexError as e:
    print("잘못된 인덱스입니다.", e)    
else: 
    print(y)
finally:
    print("프로그램이 종료되었습니다.")

'''
인덱스와 나눌 숫자를 입력하세요: 0 5
2.0
프로그램이 종료되었습니다.
'''
```
→ 예외가 발생하던, 발생하지 않던 간에 **finally는 무조건 실행**된다.   
   
- 예외 발생시키기
```python
raise Exception("에러 메세지")
```
```python
try:
    x = int(input("3의 배수를 입력하세요 : "))

    if x % 3 != 0: # 3으로 나눴을 때 나머지가 0이 아니면 3의 배수가 아님
        raise Exception("3의 배수가 아닙니다.")

except Exception as e:
    print("예외가 발생했습니다.", e)

'''
3의 배수를 입력하세요 : 2
예외가 발생했습니다. 3의 배수가 아닙니다.
'''
```
→ 직접 예외를 만들고, 에러 메세지를 정할 수도 있다.   
   
## 이터레이터
- **이터레이터(iterator) :** 값을 차례대로 꺼낼 수 있는 객체(object)   
파이썬에서는 이터레이터만 생성하고 값이 "필요한 시점"이 되었을 때 값을 만드는 방식을 사용한다.   
데이터 생성을 뒤로 미루는 방식을 지연평가(lazy evaluation)라고 한다.   
   
- **반복 가능한 객체** 는 말 그대로 반복할 수 있는 객체이다.
ex) 문자열, 리스트, 딕셔너리, 세트, …   
객체 안에 요소가 여러 개 들어있고, 한 번에 하나씩 꺼낼 수 있는 객체를 말한다.   
객체가 반복 가능한 객체인지 알아보는 방법은 객체의 iter 메서드가 들어있는지 확인해보면 된다.   
```python
l = [1, 2, 3]
l # 반복 가능한 객체

# [1, 2, 3]

dir(l)
```
*→ **dir 함수**: 해당 객체가 어떤 변수와 메소드(method)를 가지고 있는지 나열*   
list 에는 `'__iter__'` 가 들어있는 것을 확인할 수 있다.   
   
- 이터레이터 만들기
```python
class 이터레이터이름:
    def __iter__(self):
        코드
    def __next__(self):
        코드
```
   
아래와 같이 range 와 유사한 myrange 이터레이터를 만들어 보았다.
```python
class myrange:
    def __init__(self, stop):
        self.current = 0
        self.stop = stop
        
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.current < self.stop:
            r = self.current
            self.current += 1
            return r
        else:
            raise StopIteration
```
```python
for i in myrange(3):
    print(i)

'''
0
1
2
'''
```
```python
myrange(10)[0]
# TypeError 발생
```
→ 단, range 처럼 인덱스로 접근을 하지 못한다.   
   
- 인덱스로 접근할 수 있는 이터레이터 만들기   
**getitem()** 함수 작성   
딥러닝 프레임워크에 데이터셋을 준비할 때 이런 방식이 사용된다.
```python
class 이터레이터 이름:
    def __getitem__(self, 인덱스):
        코드
```
```python
# 예시
class myrange:
    def __init__(self, stop):
        self.stop = stop
        
    def __getitem__(self, index):
        if index < self.stop:
            return index
        else:
            return IndexError
```
```
myrange(10)[4]
# 4
```   

## 제너레이터
이터레이터를 만들어주는 또다른 방식(함수를 사용)   
제너레이터는 **이터레이터를 생성해주는 함수**이다.   
이터레이터에서는 클래스 안에 iter(), next(), getitem() 메서드들을 구현해야 하지만,   
제너레이터는 함수 안에서 **yield**라는 키워드만 사용하면 간단히 작성할 수 있다.
```python
def myrange2(): # 함수로서 이터레이터를 만들 수 있음
    yield 0 
    yield 1
    yield 2
```
→ 제너레이터에서는 차례대로 결과를 반환하고자 return 대신 yield 키워드를 사용한다.
```python
for i in myrange2():
    print(i)

'''
0
1
2
'''
```
모든 제너레이터는 이터레이터를 만들므로 제너레이터 객체는 이터레이터라 할 수 있다.   
   
## 모듈과 패키지
모듈을 가져오는 방법   
- import 모듈
- import 모듈1, 모듈2   
   
모듈을 사용하는 방법   
- 모듈.변수   
- 모듈.함수   
- 모듈.클래스   
```python
import math

math.sqrt(4.0) # 제곱근을 반환하는 함수
# 2.0

math.pi # π
# 3.141592653589793
```
   
- import 모듈 **as** 이름   
as를 사용하여 모듈의 이름을 바꿀 수 있다.
```python
import math as m

m.sqrt(4.0)
# 2.0

m.pi
# 3.141592653589793
```
```python
# 참고 (데이터 분석을 위한 파이썬 생태계에서 사용하는 모듈들)
import numpy as np # 관례적으로 사용
import pandas as pd
```
→ 참고로 더 적어두자면, numpy는 데이터 프레임과 시리즈를 사용하기 쉽게해주는 라이브러리고,   
pandas는 수학적 연산을 쉽게 해주는 라이브러리라고 이해할 수 있다.    
앞으로 배울 데이터 분석에서 자주 사용할 모듈!   
   
from 모듈 import 변수   
from 모듈 import 함수   
from 모듈 import 클래스
```python
from math import sqrt 

sqrt(4.0) 
# 2.0

from math import pi
pi
# 3.141592653589793
```
→ from을 사용해서 필요한 것만 import 하면 모듈까지 작성할 필요가 없다   
   
- from 모듈 import 변수, 함수, 클래스, ...   
여러 개를 한번에 import 하는 것도 가능하다.
```python
from math import sqrt, pi

sqrt(4.0)
# 2.0

pi
# 3.141592653589793
```
   
- from 모듈 import 변수 as 이름   
as를 사용해서 모듈뿐만 아니라 변수의 이름도 바꿀 수 있다.
```python
from math import pi as Pi

Pi
# 3.141592653589793
```
   
패키지 안의 모듈 가져오는 방법   
- import 패키지.모듈
- import 패키지.모듈1, 패키지.모듈2, ...   
   
패키지 안의 모듈 사용하는 방법
- 패키지.모듈.변수
- 패키지.모듈.함수
- 패키지.모듈.클래스   
```python
import urllib.request

response = urllib.request.urlopen("http://www.google.co.kr") # 패키지.모듈.함수()
response.status
# 200
```
이렇게 urllib 패키지의 request 모듈을 가져와서 사용할 수 있다.   
→ 참고: request의 urlopen 함수는 말그대로 url을 여는 것인데,   
응답 status로 뜬 200이라는 숫자는 http 상태코드 중 하나로, 요청이 성공적으로 되었을 때의 코드이다.   
   
- import 패키지.모듈 as 이름
마찬가지로 as 사용이 가능하다.
```python
import urllib.request as r

r.urlopen("http://www.google.co.kr")
response.status
# 200
```
   
- from 패키지.모듈 import 변수
from 패키지.모듈 import 클래스   
from 패키지.모듈 import 함수   
from 패키지.모듈 import 변수, 클래스, 함수...
```python
from urllib.request import urlopen

urlopen("http://www.google.co.kr")
response.status
# 200
```
   
- from 패키지.모듈 import `*`
```python
from urllib.request import *

urlopen("http://www.google.co.kr")
response.status
```
→ `*`를 import 해서 전부 가져오는 것도 가능하다. `*`의 의미는 css 에서 문서 전체에 적용할 때 `*`{ } 를 사용했던 것을 떠올리면 비슷한 것 같기도 하다.
      
참고 : 어떤 스크립트 파일이든 파이썬 인터프리터가 최초로 실행한 스크립트 파일의 `__name__`에는 'main'이 들어간다.   
이는 **프로그램의 시작점(entry point)** 이라는 뜻이다.   
   
- 패키지 만들기
모듈은 스크립트 파일이 한 개지만, 패키지는 폴더(디렉터리)로 구성되어 있다.   
   
## 시간 복잡도 표기법
- **시간 복잡도 표기법**
    - **빅-오(O(n))**: 최악일 때의 연산 횟수를 나타낸 표기법
        
        최악의 경우를 고려하므로, 가장 많이 사용되는 방법이다.
        
        *→ 입력값의 변화에 따라 연산을 실행할 때, **연산 횟수에 비해 시간이 얼마만큼 걸리는가**? 를 표기하는 방법!*
```python
 # 1에서 100 사이의 무작위수를 찾아 출력
import random
findNumber = random.randrange(1, 101) # findNumber

for i in range(1, 101): # 1 ~ 100
    if i == findNumber:
        print(i)
        break
        
# 최선일 때 1회
# 보통일 때 50회
# 최악일 때 100회: O(n)
 ```
 ```python
 sum = 0
fact = 1

for i in range(10):
    sum += i
    
for j in range(1, 11):
    fact *= j
    
print(sum, fact)
# 45 3628800

# 시간 복잡도: O(2n) --> O(n)으로 간주
```
```python
 array = [3, 5, 1, 2, 4] # 5개의 데이터

for i in array: # array에는 5개의 데이터
    for j in array: # array에는 5개의 데이터
        temp = i * j # i: 3, j: 3, 5, 1, 2, 4 -> i: 5, j: 3, 5, 1, 2, 4 ...
        print(temp)

# 시간 복잡도 --> 5*5(25) -> n*n(n**2) -> O(n**2) 5번씩 5번 돌았기 때문에 n의 제곱이 된다.
```
    
    
```python
# manatee1 = {"name":"cute", "age":2, ....} # 총 m개의 키
# manatee2 = {"name":"handsome", "age":1, ....} # 총 m개의 키
# manatee3 = {"name":"pretty", "age":3, ....} # 총 m개의 키

# manatees =  [manatee1, manatee2, manatee3......] # 총 n마리의 manatee를 저장하는 리스트

def example1(manatees):
    for manatee in manatees: # n iterations
        print(manatee['name'])
# 시간 복잡도 -> O(n)
        
def example2(manatees):
    print(manatees[0]['name'])
    print(manatees[0]['age'])
# 시간 복잡도 -> O(1)
    
def example3(manatees):
    for manatee in manatees: # n iterations
        for manatee_property in manatee: # m iterations
            print(manatee_property, ": ", manatee[manatee_property])
# 시간 복잡도 -> O(n*m)
            
def example4(manatees):
    oldest_manatee = "No manatees here!"
    for manatee1 in manatees: # n iterations
        for manatee2 in manatees:# n iterations
            if manatee1['age'] < manatee2['age']: 
                oldest_manatee = manatee2['name'] 
            else:
                oldest_manatee = manatee1['name'] 
    print(oldest_manatee)
    
# 시간 복잡도 -> O(n²)
```
      
- **O(1)**
    
    constant complexity, **상수** 시간. 
    
    입력값의 크기와 관계없이, 즉시 출력값을 얻어낼 수 있어서 입력값이 증가하더라도 시간이 늘어나지 않는다.
    
- **O(log n)**
    
    Logarithmic complexity, **로그** 시간.
    
    빅-오 표기법 중 O(1) 다음으로 빠른 시간 복잡도를 가진다.
    
    문제를 해결하는데 필요한 단계들이 연산마다 특정 요인에 의해 줄어든다.
    
- **O(n)**
    
    Linear complexity, **선형** 시간.
    
    입력값이 증가함에 따라 시간 또한 선형적으로 같은 비율로 증가한다.
    
    입력값이 커지면 커질수록 계수의 영향력이 퇴색되기 때문에, 같은 비율로 증가하고 있다면 모두 O(n)으로 표기한다!
    
- **O(n²)**
    
    quadratic complexity, 제곱 시간.
    
    입력값이 증가함에 따라 시간이 n의 제곱수의 비율로 증가한다.
    
- **O(2ⁿ)**
    
    Exponential complexity, **지수** 시간.
    
    빅-오 표기법 중 가장 느린 시간 복잡도를 가진다.
    
    문제를 해결하기 위한 단계의 수는 주어진 상수값 C 의 n 제곱이다.
    
    ![image](https://user-images.githubusercontent.com/106129152/200517655-223fc007-aa43-43d7-aa0c-b014401f78cf.png)
    
    
    ![image](https://user-images.githubusercontent.com/106129152/200517790-0211bf04-434f-4a6f-a6fe-5549c8bb7bbb.png)
    

*→ 참고 링크: [시간 복잡도 1(파이썬)](https://blog.chulgil.me/algorithm/), [시간 복잡도2(자바스크립트)](https://velog.io/@shitaikoto/Algorithm-Time-complexity)*
