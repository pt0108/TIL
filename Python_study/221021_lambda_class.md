> 부트캠프 1주차 2022년 10월 21일

## 위치 인수와 키워드 인수
- 위치 인수
```python
def print_numbers(a, b, c):
    print(a)
    print(b)
    print(c)
```
```python
print_numbers(10, 20, 30)
'''
10
20
30
'''
```
위치 인수는 **함수에 인수를 순서대로 넣는 방식**으로, 인수의 위치가 정해져 있다.   
   
- 언패킹
```python
l = [10, 20, 30]
print_numbers(*l) # *는 언패킹한다는 의미
'''
10
20
30
'''
```
언패킹은 말 그대로 짐을 푼다고 생각하면 된다!   
 ' * '을 사용하면 된다.   
   
- 가변 인수
```python
def print_numbers(*args): # args는 집합체로 원소의 개수가 가변적임
    for arg in args:
        print(arg)
```
```python
print_numbers(200)
# 200

print_numbers(200, 300, 400)
# 200, 300, 400
```
이런 식으로 제약없이 출력해내는 것을 볼 수 있다.   
   
- 키워드 인수
```python
def personal_info(name, age, address):
    print(name)
    print(age)
    print(address)
```
```python
personal_info("냉동감자", 3, "냉동실")
'''
냉동감자
3
냉동실
'''

personal_info(address = "냉동실", name = "냉동감자", age = 3)
'''
냉동감자
3
냉동실
'''
```
값은 똑같이 나온다.   
   
또, 아래와 같이 **초기값**을 설정해서 값이 입력되지 않았을 때 나오는 값을 설정해줄 수 있다.
```python
def personal_info(name, age, address = "냉동실"):
    print(name)
    print(age)
    print(address)
```
```python
personal_info(name = "냉동감자", age = 3)
'''
냉동감자
3
냉동실
'''
```
   
딕셔너리를 사용하여 호출할 수도 있다.
```python
d = { 'name':'냉동감자', 'age':3, 'address':'냉동실'}
personal_info(*d) # 한 번만 언패킹했기 때문에 키만 출력됨
'''
name
age
address
'''

d = { 'name':'냉동감자', 'age':3, 'address':'냉동실'}
personal_info(**d) # 언패킹을 두 번해서 값이 출력됨
'''
냉동감자
3
냉동실
'''
```
   
키워드 인수를 가변적으로 처리할 수 있다.
```python
def personal_info(**kwargs): # kwargs에는 가변적인 개수의 키와 값의 쌍으로 이루어짐 / 키와 값의 쌍으로 이뤄졌기 때문에 언패킹도 2번
    for k, v in kwargs.items():
        print(k, v)

personal_info(name = "냉동감자")
# name 냉동감자

personal_info(name = "냉동감자", age = "3")
'''
name 냉동감자
age 3
'''
```
→ for 문으로 값이 바닥날 때까지 가져온다고 생각하면 된다.   
   
- args  / kwargs
args와 kwargs가 정확히 뭘까? 주석으로 간단한 설명이 적혀있지만, 더 자세히 찾아보았다. 이들은 관용적으로 사용되는 이름이다.   
**args** → arguments, 정해지지 않은 수의 파라미터를 받음   
**kwargs**→ keyword arguments, 정해지지 않은 수의 키워드 파라미터를 받음   
*파라미터 = 매개변수*   

## 함수에서 재귀 호출 사용하기
함수 안에서 함수 자기자신을 호출하는 방식을 재귀호출(recursive call)이라고 한다.
```python
def hello():
    print('hello world')
    hello()
```
이렇게 종료조건 없이 작성할 경우 무한대로 print를 하다가 에러가 난다.
      
재귀 호출할 경우에는 **종료 조건**이 반드시 있어야 한다!
```python
def hello(count):
    if count == 0: # 종료 조건
        return
    print('hello world', count)
    count -= 1 # count = count - 1
    hello(count)

hello(5)
'''
hello world 5
hello world 4
hello world 3
hello world 2
hello world 1
'''
```
   
재귀 함수는 반복문으로도 동일하게 구현이 가능하다.
```python
for def hello(count):
    for i in range(count):
        print("hello world")
hello(5)
```
   
특정 조건을 반복문과 재귀 호출 두 가지로 봐보자!   
(1) 10 ~ 1 까지의 합
```python
# 반복
sum = 0
for i in range(10, 0, -1):
    sum = sum + i

sum
# 55

# 재귀
def add_sum(i):
    if i == 1: # 종료조건
        return 1
    sum = i + add_sum(i-1)
    return sum

add_sum(10)
# 55
```
   
(2) 팩토리얼   
→ 여기서 팩토리얼이란, 1부터 지정된 수까지 모든 수의 곱을 의미한다.
```python
# 반복
# n! = n * (n-1) * (n-2) * (n-3) * ... * 1

fact_val = 1
for i in range(5, 0, -1):
    fact_val = fact_val * i
    
fact_val # 5!
# 120

# 재귀
def factorial(i):
    if i == 1:
        return 1
    result = i *factorial(i-1)
    return result

factorial(5)
# 120
```
   
(3) 구구단 출력
```python

# 반복
x = 2 # 몇 단

for y in range(1, 10):
    print(x, '*', y, '=', x*y)
'''
2 * 1 = 2
2 * 2 = 4
2 * 3 = 6
2 * 4 = 8
2 * 5 = 10
2 * 6 = 12
2 * 7 = 14
2 * 8 = 16
2 * 9 = 18
'''
```
```python
def gugu(x, y): # x: 단, y: 1~9
    print(x, '*', y, '=', x*y)
    if y < 9: 
        gugu(x, y+1)
# 여기까지 실행시키면 위의 반복문과 같은 결과가 나온다.
        
for dan in range(2, 10):
    print('----- %d 단 -----' % dan)
    gugu(dan, 1)
    print()
```
바로 위 코드를 전부 작성하고 실행하면
```python
----- 2 단 -----
2 * 1 = 2
2 * 2 = 4
2 * 3 = 6
2 * 4 = 8
2 * 5 = 10
2 * 6 = 12
2 * 7 = 14
2 * 8 = 16
2 * 9 = 18
```
위와 같은 형태로 2단부터 9단까지 출력된다.
   
## 람다 표현식
람다 표현식은 **이름 없는 함수를 만드는데 사용**된다.   
20일 차에서 잠깐 응용하는 문제가 나와서 살짝 짚고 넘어갔었다.      
다음과 같이 입력한 값에 10을 더해주는 함수가 있다고 하자.
```python
def plus_ten(x):
    return x + 10

plus_ten(2)
# 12
```
이를 람다 표현식을 사용하면 어떻게 될까?
   
- lambda 매개변수 : 식
```python
plus_ten = lambda x : x + 10
plus_ten(2)
# 12
```
이렇게 해도 결과는 똑같다.
```python
(lambda x : x + 10)(2)
# 12
```
      
- lambda 매개변수 : 식1 if 조건식 else 식2
```python
a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
# 3의 배수이면 문자열로 만들고, 그렇지 않으면 있는 그대로 출력하기

my_format = lambda x : str(x) if x % 3 == 0 else x
list(map(my_format, a))
# [1, 2, '3', 4, 5, '6', 7, 8, '9', 10]
```
```python
list(map(lambda x : str(x) if x % 3 == 0 else x, a))
# [1, 2, '3', 4, 5, '6', 7, 8, '9', 10]
```
람다를 사용한 변수를 넣는 방법도 있지만, 그 자리에 람다 표현식 자체를 집어넣어도 결과는 똑같다.   
```python
a = [1, 2, 3, 4, 5]
b = [2, 4, 6, 8, 10]

mul = lambda x, y : x * y

# 두 리스트를 요소별로 곱셈한 결과를 리스트로 출력
list(map(mul, a, b))
# [2, 8, 18, 32, 50]

list(map(lambda x, y : x * y, a, b))
# [2, 8, 18, 32, 50]
```
   
**map**(함수, 반복 가능한 객체) : 반복 가능한 객체에 함수를 일괄 적용   
**filter**(함수, 반복 가능한 객체) : 반복 가능한 객체에 함수에서 출력하는 조건에 맞는 것만 가져옴
```python
def f(x):
    return x > 5 and x < 10 # True or False

a = [3, 2, 8, 19, 16, 15, 9, 1, 0]

list(filter(f, a))
# [8, 9]
```
   
## Workshop
### 문제1) 거리 계산
리스트를 이용하여 점 사이의 거리를 계산 해 보자.   
직교 좌표 위에서 A는 (1, 1), B는 (3, 2), C는 (5,7)일 때 X(2, 3)와 A/B/C와의 거리를 각각 구하여라.   
위 코드블럭을 이용하여 distMeasure 함수를 정의하라.
![image](https://user-images.githubusercontent.com/106129152/200475343-bdda696c-1f07-4456-93d5-dfa08fc13c91.png)
```python
# option 1

points = [(1, 1), (3, 2), (5, 7)] # A, B, C
x = (2, 3)

def distMeasure():
    result = []
    for point in points: # A, B, C
        dist = ((point[0] - x[0])**2 + (point[1] - x[1])**2)**(1/2) # 거리를 구하는 공식
        result.append(dist)
    return result

result = distMeasure()
result
# [2.23606797749979, 1.4142135623730951, 5.0]
```
```python
# option 2 map 사용

points = [(1, 1), (3, 2), (5, 7)] # A, B, C
x = (2, 3)

def distMeasure_1p(point): # A or B or C
    dist = ((point[0] - x[0])**2 + (point[1] - x[1])**2)**(1/2)
    return dist

list(map(distMeasure_1p, points))
# [2.23606797749979, 1.4142135623730951, 5.0]
```
```python
# option 3 (map + lambda 사용)

distMeasure_1p = lambda point: ((point[0] - x[0])**2 + (point[1] - x[1])**2)**(1/2)
list(map(distMeasure_1p, points))
# [2.23606797749979, 1.4142135623730951, 5.0]

# option 4 (한줄에)

list(map(lambda point: ((point[0] - x[0])**2 + (point[1] - x[1])**2)**(1/2), points))
# [2.23606797749979, 1.4142135623730951, 5.0]
```
   
### 문제2) 이미지 파일만 가져오기
다음 소스 코드를 완성하여 확장자가 .jpg, .png인 이미지 파일만 출력되게 만드세요.   
여기서는 람다 표현식을 사용해야 하며 출력 결과는 리스트 형태여야 합니다.   
람다 표현식에서 확장자를 검사할 때는 문자열 메서드를 활용하세요.
```python
files = ['font', '1.png', '10.jpg', '11.gif', '2.jpg', '3.png', 'table.xslx', 'spec.docx']
실행결과
['1.png', '10.jpg', '2.jpg', '3.png']
```
```python
files = ['font', '1.png', '10.jpg', '11.gif', '2.jpg', '3.png', 'table.xslx', 'spec.docx']

# option 1

def filter_img(file):
    if file.find('.jpg') != -1 or file.find('.png') != -1: # -1 은 0, 없음을 뜻함
        return True # filter가 True인 것들만 가져옴

list(filter(filter_img, files))
# ['1.png', '10.jpg', '2.jpg', '3.png']
```
```python
# option 2

def filter_img(file):
    if ('jpg' in file) or ('png' in file):
        return True # filter가 True인 것들만 가져옴

list(filter(filter_img, files))
# ['1.png', '10.jpg', '2.jpg', '3.png']
```
```python
# option 3 람다식 정의

filter_img = lambda file : file.find('.jpg') != -1 or file.find('.png') != -1
list(filter(filter_img, files))
# ['1.png', '10.jpg', '2.jpg', '3.png']
```
```python
# option 4 람다식, 한줄 작성

list(filter(lambda file : file.find('.jpg') != -1 or file.find('.png') != -1, files))
# ['1.png', '10.jpg', '2.jpg', '3.png']
```
   
### 문제3) 파일 이름 한꺼번에 변경하기
표준 입력으로 숫자.확장자 형식으로 된 파일 이름 여러 개가 입력됩니다.   
파일 이름이 숫자 3개이면서 앞에 0이 들어가는 형식으로 출력되게 만드세요.   
예를 들어 1.png는 001.png, 99.docx는 099.docx, 100.xlsx는 100.xlsx처럼 출력되어야 합니다.   
그리고 람다 표현식을 사용해야 하며 출력 결과는 리스트 형태여야 합니다.   
람다 표현식에서 파일명을 처리할 때는 문자열 포매팅과 문자열 메서드를 활용하세요.
```python
입력 예
1.jpg 10.png 11.png 2.jpg 3.png
결과
['001.jpg', '010.png', '011.png', '002.jpg', '003.png']
입력 예
97.xlsx 98.docx 99.docx 100.xlsx 101.docx 102.docx
결과
['097.xlsx', '098.docx', '099.docx', '100.xlsx', '101.docx', '102.docx']
```
```python
files = input().split()
# 1.jpg 10.png 11.png 2.jpg 3.png 입력

files
# ['1.jpg', '10.png', '11.png', '2.jpg', '3.png']

names = []
exts = []
for file in files:
    name = file.split('.')[0]
    names.append(int(name))

    ext = file.split('.')[1]
    exts.append(ext)

names, exts
# ([1, 10, 11, 2, 3], ['jpg', 'png', 'png', 'jpg', 'png'])
```
→ input 된 값을 split으로 나눠서 앞의 파일명은(인덱스 0번) name, 뒤의 확장자는(인덱스 1번) ext에 저장한다.   
각각의 name과 ext는 for문 위에 만들었던 빈 딕셔너리들인 names와 exts에 append된다.   
이때, 입력된 파일명은 숫자형이 아닌 문자열로 저장되기 때문에 int를 써서 숫자로 바꿔준다.
```python
# format 함수 연습
name = 1
ext = 'jpg'
"{:03d}.{}".format(name, ext) 
# '001.jpg'
```
```python
def fmt(name, ext):
    return "{:03d}.{}".format(name, ext)

list(map(fmt, names, exts))
# ['001.jpg', '010.png', '011.png', '002.jpg', '003.png']
```
***:03d** → 3자리 수로 하되 비어있는 곳은 0으로 채워넣겠다는 뜻*   
이제 각각 저장된 값들은 format 함수로 다시 연결된다.
```python
list(map(lambda name, ext:"{:03d}.{}".format(name, ext), names, exts))
# ['001.jpg', '010.png', '011.png', '002.jpg', '003.png']
```
## 변수의 사용 범위
**전역 변수**는 함수의 외부에서 선언된 변수로, 모든 함수에 접근이 가능하다.   
**지역 변수**는 함수 내부에서 선언된 변수로, 함수 내부에서만 사용할 수 있다.
```python
x = 10 # 전역 변수

def foo():
    x = 20 # 지역 변수
    print("foo()", x)
    
foo()
print("main()", x)

'''
foo() 20
main() 10
'''
```
```python
x = 10 # 전역 변수

def foo():
    global x 
    x = 20 # 지역 변수
    print("foo()", x)
    
foo()
print("main()", x) # 함수 내부에서 수정된 x가 바깥에서도 유효 (x가 global로 선언되었기 때문)

'''
foo() 20
main() 20
'''
```
→ 여기서 **grobal 키워드**로 변수를 재선언 해주면, 지역 변수였던 것도 함수 바깥에서 유효하게 작동한다.   

## 클래스
**클래스는 붕어빵 틀**과 같은 것이고,   
그 클래스에 속한 **인스턴스는 붕어빵**이라고 생각하면 이해하기 쉽다.
```
class 클래스 이름: # 붕어빵 틀
    def 메서드(self):
        코드
```
```python
class Person:
    def greeting(self):
        print("Hello")
```
→ Person 이라는 클래스는, “Hello”를 print 하는 함수 greeting을 갖고 있다.   
   
인스턴스 = 클래스() # 붕어빵
```python
james = Person()
mary = Person()
```
→ 그리고 james 와 mary는 Person이라는 붕어빵 틀에서 찍어져 나온 붕어빵이다.   
   
인스턴스.메서드()
```python
james.greeting()
# Hello

mary.greeting()
# Hello
```
   
   
```python
# 파이썬에서 흔히 볼 수 있는 클래스
a = int(10)
print(type(a))
# <class 'int'>

b = list(range(10))
print(type(b))
# <class 'list'>

b.append(3) # 인스턴스 메서드를 사용한 예
```
   
```python
class 클래스 이름:
    def __init__(self):
        self.속성 = 값   # 붕어빵 앙꼬
```
→ 클래스를 선언할 때 초기화 함수 __init__( )를 구현하면 객체를 생성하는 것과 동시에 속성값을 지정할 수 있다.   
   
```python
class Person:
    def __init__(self):
        self.hello = "안녕하세요"
    
    def greeting(self):
        print(self.hello)

james = Person()
james.greeting()
# 안녕하세요
```
   
```python
class 클래스 이름:
    def __init__(self, 매개변수1, 매개변수2, ...):
        self.속성1 = 매개변수1
        self.속성2 = 매개변수2
```
```python
class Person:
    def __init__(self, hello_msg):
        self.hello = hello_msg
    
    def greeting(self):
        print(self.hello)
```
```python
james = Person("안녕하십니까") # 매개변수 안녕하십니까
james.greeting() # 매개변수 안녕하십니까를 출력
# 안녕하십니까

selly = Person("안녕하세요?")
selly.greeting()
# 안녕하세요?
```
   
```python
class Person:
    def __init__(self, hello_msg, name, age, address):
        self.hello = hello_msg
        self.name = name
        self.age = age
        self.address = address
    
    def greeting(self):
        print(self.hello)
        print("저는 {}입니다".format(self.name))
        print("나이는 {}살입니다".format(self.age))
        print("{}에 살고 있습니다".format(self.address))
```
```python
james = Person("안녕하십니까", "제임스", 17, "서초동")
james.greeting()
'''
안녕하십니까
저는 제임스입니다
나이는 17살입니다
서초동에 살고 있습니다
'''

maria = Person("안녕하세요", "마리아", 20, "방배동")
maria.greeting()
'''
안녕하세요
저는 마리아입니다
나이는 20살입니다
방배동에 살고 있습니다
'''
```
   
```python
class 클래스 이름:
    def __init__(self, 매개변수):
        self.__속성 = 값 # 비공개 속성
```
```python
class Person:
    def __init__(self, hello_msg, name, age, address, wallet):
        self.hello = hello_msg
        self.name = name
        self.age = age
        self.address = address
        self.__wallet = wallet # 비공개 속성
    
    def greeting(self):
        print(self.hello)
        print("저는 {}입니다".format(self.name))
        print("나이는 {}살입니다".format(self.age))
        print("{}에 살고 있습니다".format(self.address))
        
    def pay(self, amount):
        self.__wallet = self.__wallet - amount # 비공개 속성이어도 함수 안에서는 사용 가능
        print("지갑에 {}원 남았습니다.".format(self.__wallet))
```
```python
selly = Person("안녕?", "셀리", 15, "강남역", 10000)
selly.greeting()
'''
안녕?
저는 셀리입니다
나이는 15살입니다
강남역에 살고 있습니다
'''
# 비공개 속성은 외부에서 접근 불가(에러 발생)

selly.pay(5000)
# 지갑에 5000원 남았습니다.
```
*→ 비공개 속성은 외부에서 확인할 수 없지만, 함수 안에서는 사용이 가능하다.*   

## 클래스 속성과 인스턴스 속성 
```python
class 클래스 이름:
    속성 = 값
```
**클래스 속성** : 모든 인스턴스들이 공유, 인스턴스 전체가 사용해야 하는 값을 저장할 때 사용   
**인스턴스 속성** : 인스턴스별로 독립되어 있음. 각 인스턴스가 값을 따로 저장할 때 사용   
   
```python
# 클래스 속성 bag을 사용하여 인스턴스 모두가 공용으로 사용
class Person:
    bag = [] # 클래스 바로 밑에 선언, 인스턴스에 종속적이지 않음
    
    def put_bag(self, stuff):
        Person.bag.append(stuff)
```
   
```python
james = Person()
james.put_bag("책")

maria = Person()
maria.put_bag("열쇠")

james.bag
# ['책', '열쇠']

maria.bag
# ['책', '열쇠']
```
   
```python
class Person:
    def __init__(self):
        self.bag = []

    def put_bag(self, stuff):
        self.bag.append(stuff)
```
```python
james = Person()
james.put_bag("책")

maria = Person()
maria.put_bag("열쇠")

james.bag
# ['책']

maria.bag
# ['열쇠']
```   
   
## 클래스 상속 사용하기
```
class 기반 클래스 이름 :
    코드

class 파생 클래스 이름(기반 클래스) :
```
```python
class Person:
    def greeting(self):
        print("안녕하세요")

class Student(Person):
    def study(self):
        print("공부중입니다")
```
이와 같이 Student 클래스의 기반 클래스에 Person 을 넣어 상속해보았다.   
   
```python
james = Student()
james.study()
# 공부중입니다

james.greeting() 
# 안녕하세요
```
→ james는 Student 클래스이지만, Person 클래스를 상속받았으므로 greeting을 사용하는 것이 가능하다.   
상속받은 클래스의 기능까지도 사용 가능하다는 것을 알 수 있다.   
   
```python
class Person:
    def __init__(self):
        print("Person initialized")
        
    def greeting(self):
        print("안녕하세요")
        
class Student(Person):
    def __init__(self):
        print("Student initialized")
        
    def study(self):
        print("공부중입니다")
```
```python
james = Student()
# Student initialized
```
→ 자식 클래스에 __init__ 가 정의되어 있지 않다면 부모 클래스의 __init__ 을 사용한다.   
자식 클래스에 __init__ 가 정의되어 있다면 이것이 우선이다.      
```python
class Person:
    def __init__(self):
        print("Person initialized")
        self.hello = "안녕하세요"
        
    def greeting(self):
        print(self.hello)
        
class Student(Person):
    def __init__(self):
        print("Student initialized")
        
    def study(self):
        print("공부중입니다")
```
```python
james = Student()
james.study()
'''
Student initialized
공부중입니다
'''
```
    
```python
class Person:
    def __init__(self):
        print("Person initialized")
        self.hello = "안녕하세요"
        
    def greeting(self):
        print(self.hello)
        
class Student(Person):
    def __init__(self):
        super().__init__() # 부모 클래스의 __init__()를 강제로 호출
        print("Student initialized")
        
    def study(self):
        print("공부중입니다")
```
```python
james = Student()
james.greeting()
'''
Person initialized
Student initialized
안녕하세요
'''
```
- 메서드 오버라이딩
파생 클래스에서 기반 클래스의 메서드를 새로 정의하는 것이 메서드 오버라이딩이다.   
말 그대로 기반 클래스의 메서드를 무시하고 새로운 메서드를 만든다는 뜻이다!   
주로 원래 기능을 유지하면서 새로운 기능을 덧붙일 때 사용한다.
```python
class Person:
    def greeting(self):
        print("안녕하세요")
        
class Student(Person):
    def greeting(self):
        print("안녕하세요. 저는 인공지능 과정 25기 학생입니다.")
```
```python
james = Student()
james.greeting()
# 안녕하세요. 저는 인공지능 과정 25기 학생입니다.
```
   
```python
class Person:
    def greeting(self):
        print("안녕하세요")
        
class Student(Person):
    def greeting(self):
        super().greeting()
        print("저는 인공지능 과정 25기 학생입니다.")
```
```python
james = Student()
james.greeting()
'''
안녕하세요
저는 인공지능 과정 25기 학생입니다.
'''
```
   
- 다중 상속 사용하기
```
class 기반 클래스1
    코드

class 기반 클래스2
    코드

class 파생 클래스(기반 클래스1, 기반 클래스2)
    코드
```
```python
class Person:
    def greeting(self):
        print("안녕하세요")

class University:
    def manage_credit(self):
        print("학점 관리")
        
class Undergraduate(Person, University):
    def study(self):
        print("공부하기")
```
```python
james = Undergraduate()
james.study()
# 공부하기

james.manage_credit()
# 학점 관리

james.greeting()
# 안녕하세요
```
   
- 추상 클래스
추상 클래스는 **메서드의 목록만 가진 클래스**이며 상속받는 클래스에서 메서드 구현을 강제하기 위해 사용한다.
```python
from abc import *

class 추상클래스(metaclass=ABCMets):
    @abstractmethod
    def 메서드 이름(self):
        코드
```
   
```python
from abc import *

class StudentBase(metaclass=ABCMeta):
    @abstractmethod
    def study(self):
        pass
    
    def gotoschool(self):
        pass
```
```python
class Student(StudentBase):
    def study(self):
        print("공부하기")
        
    def gotoschool(self):
        print("학교가기")
```
```python
james = Student()
james.study()
# 공부하기
```
   
## Workshop
### 문제) 리스트에 기능 추가하기
아래 예시와 같이 리스트(list)에 replace 메서드를 추가한 AdvancedList 클래스를 작성하세요.   
AdvancedList는 list를 상속받아서 만들고, replace 메서드는 리스트에서 특정 값으로 된 요소를 찾아서 다른 값으로 바꾸도록 만드세요.
```python
x = AdvancedList([1, 2, 3, 1, 2, 3, 1, 2, 3])
x.replace(1, 100)
print(x)
결과
[100, 2, 3, 100, 2, 3, 100, 2, 3]
```
보통 replace의 old는 변경하고 싶은 문자, new는 새로 바꿀 문자이다.
```python
# option1 (for)
class AdvancedList(list):
    def replace(self, old, new): # self : list 형의 데이터 (ex- [1, 2, 3, ...])
        for idx, v in enumerate(self): # idx: 0, 1, 2, 3, ... v: 1, 2, 3, 1, 2, 3
            if v == old:
                self[idx] = new # x[0] = 100, x[3] = 100, x[6] = 100
```
→ 클래스 AdvancedList를 만들고 list를 상속받게 만든다.  `class AdvancedList(list):`   
리스트를 상속받았으므로 self로 리스트의 모든 메서드를 사용할 수 있게 되었다.   
그리고 replace에 필요한 old, new에 들어갈 것들을 만들어 주어야 한다.   
   
문제에서는 리스트에 있는 숫자 1을 100으로 바꾸게끔 알려주고 있다.   
enumerate를 사용했기 때문에 idx 에는 인덱스가, v에는 그에 맞는 값이 들어가게 된다.   
   
이때, `if v == old:` ← v가 변경하고 싶은 문자(old)와 같다면,   
`self[idx] = new` ← 새로 바꿀 문자로 적용한다.   
   
그래서 x에 AdvancedList([1, 2, 3, 1, 2, 3, 1, 2, 3])을 넣고, x.replace(1, 100) 를 한 뒤   
x를 출력하면 [100, 2, 3, 100, 2, 3, 100, 2, 3] 가 나오게 되는 것이다!   
*old에 1, new에 100이 들어간 결과*라고 생각하면 된다.   
   
```python
# option2 (while)
class AdvancedList(list):
    def replace(self, old, new): # self : list 형의 데이터 (ex- [1, 2, 3, ...])
        while old in self:
            idx = self.index(old)
            self[idx] = new
```
```python
x = AdvancedList([1, 2, 3, 1, 2, 3, 1, 2, 3])
x.replace(1, 100)
print(x)
# [100, 2, 3, 100, 2, 3, 100, 2, 3]
```
나에게는 상당히 어렵게 느껴지는 문제라, 하나씩 풀어 생각해도 단숨에 이해하지 못하는 부분들이 있다.   
해당 문제의 해설을 조금 가져오자면,
> while로 반복하면서 self에 특정 요소가 있을 때 계속 반복하도록 만든 뒤 요소를 바꿔주면 됩니다. 물론 리스트에서 특정 요소가 있는지 확인할 때는 in 연산자를 사용합니다. 이 방식을 사용하면 리스트에서 요소를 계속 바꾸다가 바꿀 값이 없으면 반복을 끝냅니다.   
   
이해하는데에 더 도움이 된다.
