> 부트캠프 1주차 2022년 10월 18일

## 논리 연산자
a **and** b   
둘 중 하나라도 False면, False가 출력이 된다. 
a **or** b   
둘 중 하나만 True가 있어도, True가 출력이 된다.
**not** a   
a가 True면 False를, False면 True를 출력한다. (값을 부정)
### 비교 연산자와 논리 연산자를 함께 사용
```python
10 == 10 and 10 != 5
# True

10 == 10 and 10 == 5
# False
```
## Workshop
### 문제) 합격 여부 출력하기
국어, 영어, 수학, 과학 점수가 있을 때 한 과목이라도 50점 미만이면 불합격이라고 정했습니다.   
다음 소스 코드를 완성하여 합격이면 True, 불합격이면 False가 출력되게 만드세요.
korean = 92   
english = 47   
mathmatics = 86   
science = 81   
```python
print(korean >= 50 and english >= 50 and mathmatics >= 50 and science >= 50)
# False

not(korean < 50 or english < 50 or mathmatics < 50 or science < 50)
# False
```
여기서, all(), any()를 사용할 수도 있다.   
all()은 전부 True여야 True가 나옴 / and 비슷. 모두 True여야 True 반환   
any()는 any는 하나라도 True가 있으면 True / or 비슷. 하나라도 True인게 있으면 True   
*각각의 요소들이 연속적으로 이어진 자료형을 시퀀스 자료형(sequence types)이라고 한다.*   
## 문자열 사용하기
```python
s1 = 'hello'
s2 = "hello"
s3 = '''hello'''
s4 = """hello"""

# 전부 같은 문자열 hello 가 출력된다.
```
작성할 문자에 따옴표가 있으면, 이를 출력하는 여러가지 방법이 있다.
```python
s1 = 'hello "python"'
# hello "python"

s2 = "hello 'python'"
# hello 'python'

s3 = """hello "python" """
# hello "python"

s4 = '''hello 'python' '''
# hello 'python'
```
큰따옴표나 작은따옴표 앞에 \를 붙이는, 이스케이프 문자를 사용하는 방법도 있다.
```python
s5 = 'hello \'python\''
# hello 'python'
```
따옴표를 3개씩 쓰면 이런 방식의 출력도 가능하다.
```python
s6 = '''here is
python world
it is
real!!!'''

# 큰따옴표, 작은따옴표 상관없음! 
'''
here is
python world
it is
real!!!
'''
```
## Workshop
'python' is a "programming language"   
that lets you work quickly   
and   
integrate systems more effectively.   

를 출력해보자.
```python
s = ''''python' is a "programming language"
that lets you work guickly
and
integrate systems more effectively.'''
print(s)
```
## 리스트(list)와 튜플(tuple)
리스트 = [값, 값, 값, ...]   
꼭 같은 타입에 한정해서 값을 넣지 않아도 된다.
```python
scores = [90, 95, 100, 80, 70, 100]
print(scores)
# [90, 95, 100, 80, 70, 100]

person = ["James", 17, 175.3, True]
print(person)
# ['James', 17, 175.3, True]
```
빈 리스트 만들기       
리스트 = []   
리스트 = list()   
```python
empty_list1 = []
print(empty_list1)
# []

empty_list2 = list()
print(empty_list2)
# []
```
리스트 = list(range(횟수))
```python
a = list(range(10))
print(a)
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```
리스트 = list(range(시작, 끝))
```python
b = list(range(5, 10))
print(b)
# [5, 6, 7, 8, 9]
```
리스트 = list(range(시작, 끝, 증가폭))
```python
c = list(range(0, 10, 2))
print(c)
# [0, 2, 4, 6, 8]

d = list(range(10, 0, -1))
print(d)
# [10, 9, 8, 7, 6, 5, 4, 3, 2, 1] 
```
   
튜플 = (값, 값, 값, ...)   
튜플 = 값, 값, 값, ...   
list와의 차이점은 **수정이 불가**하단 것
```python
a = (1, 2, 3, 4)
print(a)
# (1, 2, 3, 4)

b = 1, 2, 3, 4
print(b)
# (1, 2, 3, 4)

c = (1,) # 인수가 하나일 때는 꼭 콤마를 찍어줘야함
type(c)
# tuple
```
튜플 = tuple(range(횟수))
```python
a = tuple(range(10))
print(a)
# (0, 1, 2, 3, 4, 5, 6, 7, 8, 9)
```
튜플 = tuple(range(시작, 끝))
```python
b = tuple(range(5, 12))
print(b)
# (5, 6, 7, 8, 9, 10, 11)
```
튜플 = tuple(range(시작, 끝, 증가폭))
```python
c = tuple(range(5, 12, 3))
print(c)
# (5, 8, 11)
```
리스트를 튜플로, 튜플을 리스트로 바꿀 수도 있다.
```python
a = [1, 2, 3]
tuple_a = tuple(a)
print(tuple_a)
# (1, 2, 3)

b = (1, 2, 3)
list_b = list(b)
print(list_b)
# [1, 2, 3]
```
   
## Workshop
### 문제1) range로 리스트 만들기
[5, 3, 1, -1, -3, -5, -7. -9]가 출력되게 만드세요.
```python
a = list(range(5, -10, -2))
print(a)
# [5, 3, 1, -1, -3, -5, -7, -9]
```
   
### 문제2) range로 튜플 만들기
표준입력으로 정수가 입력됩니다. range의 시작하는 숫자는 -10, 끝나는 숫자는 10이며   
입력된 정수만큼 증가하는 숫자가 들어가도록 튜플을 만들고, 해당 튜플을 출력하는 프로그램을 만드세요   
(input에서 안내 문자열은 출력하지 않아야 합니다.)   
입력: 2(임의), 출력: (-10, -8, -6, -4, -2, 0, 2, 4, 6, 8)
```python
step = int(input())
print(tuple(range(-10, 10, step)))
# (-10, -8, -6, -4, -2, 0, 2, 4, 6, 8)
```
   
## 시퀀스 자료형 활용하기
시퀀스 자료형: list, tuple, range, str 등   
값 in 시퀀스 객체
```python
a = [1, 2, 3, 4, 5]
1 in a
# True

b = (1, 2, 3, 4, 5)
10 in b
# False

c = "Hello"
'H' in c
# True

10 in range(10)
# False / range(10)을 list로 출력해보면 0부터 9까지 나오기 때문에 10은 포함되어있지 않음!
```
시퀀스 객체1 + 시퀀스 객체2
```python
a = [1, 2, 3, 4, 5]
b = [6, 7, 8, 9, 10]

a + b
# [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

c = (1, 2, 3, 4, 5)
d = (6, 7, 8, 9, 10)

c + d
# (1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

list(range(5)) + list(range(5))
# [0, 1, 2, 3, 4, 0, 1, 2, 3, 4]

s1 = "Hello "
s2 = "World"

s1 + s2
# 'Hello World'
```
시퀀스 객체 * 정수
```python
[1, 2, 3] * 3
# [1, 2, 3, 1, 2, 3, 1, 2, 3]

3 * (1, 2, 3)
# (1, 2, 3, 1, 2, 3, 1, 2, 3)

list(range(5)) * 2
# [0, 1, 2, 3, 4, 0, 1, 2, 3, 4]

"Hello " * 3
# 'Hello Hello Hello '
```
**len(시퀀스 객체)**   
len은 문자열의 길이를 반환해주는 함수지만, 시퀀스 객체에 사용하면 객체 안에 들어있는 요소를 카운팅할 수 있다.
```python
a = [1, 2, 3]
len(a)
# 3

b = (1, 2, 3, 4, 5)
len(b)
# 5

len(range(10))
# 10

len("Hello")
# 5
```
시퀀스[인덱스]   
여타 프로그래밍 언어들이 그렇듯, 파이썬도 0부터 숫자를 센다.
```python
scores = [90, 80, 100, 90]

scores[1]
# 80 / 두번째 스코어를 갖고 오고 싶을 때, 1을 입력하면 됨

scores[-1]
# 90 / 음수 인덱스, 마지막 값을 가지고 올 때 편리

s = "Hello"
s[0]
# 'H'

s[-2]
# 'l' / 뒤에서 두번째 값
```
시퀀스 객체[인덱스] = 값   
위 문법은 list 객체에서만 유효, tuple, range, str에서는 요소 값을 변경할 수 없음.
```python
scores = [90, 100, 100, 70]
scores[0] = 95
print(scores)
# [95, 100, 100, 70] / 0번째 값을 95로 수정했기 때문
```
del 시퀀스 객체[인덱스]   
이 문법도 마찬가지로 list 객체에서만 유효하다.
```python
a = [1, 2, 3, 4]
del a[2]
print(a)
# [1, 2, 4] / del을 사용해서 3번째 값이 삭제됨
```
시퀀스 객체[시작 인덱스:끝 인덱스]
```python
a = [10, 20, 30, 40, 50]

a[0:3] # 3번째(=40)는 포함 안됨 (즉, 0~2번째까지 가져오는 문법)
# [10, 20, 30]

a[:3] # 0번째는 생략 가능
# [10, 20, 30]

a[2:5]
# [30, 40, 50]

a[2:] # 마지막번째도 생략 가능
# [30, 40, 50]

a[:] # 시작 인덱스와 끝 인덱스를 모두 생략하면 처음부터 끝까지 가져옴
# [10, 20, 30, 40, 50]

a[3:-1] # 위에서 말한 것과 마찬가지로 -1번째는 포함하지 않으므로 40, 50이 아닌 40만 가져옴.
# [40]
```
시퀀스객체[시작 인덱스:끝 인덱스:증가폭]
```python
a = list(range(0, 100, 10))
a
# [0, 10, 20, 30, 40, 50, 60, 70, 80, 90]

a[0:5]
# [0, 10, 20, 30, 40]

a[0:5:2]
# [0, 20, 40]


a[-1::-1] # 끝 인덱스가 생략된 상태
# [90, 80, 70, 60, 50, 40, 30, 20, 10, 0]
```
   
## Workshop
### 문제1) 최근 3년간 연구 출력하기
리스트 year에 연도, population에 서울시 인구수가 저장되어 있습니다.   
아래 소스 코드를 완성하여 최근 3년간 연도와 인구수를 각각 리스트로 출력되게 만드세요.
```python
year = [2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018]
population = [10249679, 10195318, 10143645, 10103233, 10022181, 9930616, 9857426, 9838892]
```
```python
print(year[-3:]) 
print(population[-3:])
# [2016, 2017, 2018] 
# [9930616, 9857426, 9838892]
```
year와 population을 연결지어서 한꺼번에 출력할 수도 있다!
```python
# year와 population을 연결지어서 한꺼번에 출력할 수 있음
list(zip(year[-3:], population[-3:]))

# [(2016, 9930616), (2017, 9857426), (2018, 9838892)]
```
   
### 문제2) 인덱스가 홀수인 요소 출력하기
다음 소스 코드를 완성하여 튜플 n에서 인덱스가 홀수인 요소들이 출력되게 만드세요.
```python
n = -32, 75, 97, -10, 9, 32, 4, -15, 0, 76, 14, 2
```
```python
n[1:len(n):2]
# (75, -10, 32, -15, 76, 2)
```
→ “인덱스”가 홀수인 요소들을 출력하는 것이기 때문에 증가폭 2를 넣은 것
   
### 문제3) 리스트의 마지막 요소 5개 삭제하기
표준 입력으로 숫자 또는 문자열 여러개가 입력되어 리스트 x에 저장됩니다(입력되는 숫자 또는 문자열의 개수는 정해져 있지 않음).   
리스트 x의 마지막 요소 5개를 삭제한 뒤 튜플로 출력되게 만드세요.
```python
x = input().split()
del x[-5:]
print(tuple(x))
# a b c d e f 입력 / ('a',) 출력
```
   
색인 → 시퀀스에서 하나를 가져오는 것   
슬라이싱 → 어떤 구간을 가져오는 것   
## Workshop
### 문제1) 주민번호로 성별 구분하기
아래와 같은 홍길동씨의 주민번호를 대쉬(-) 기호 전후로 쪼개보자.   
성별이 남자면 'male', 여자면 'female'을 출력하세요.
```
아래와 같은 홍길동씨의 주민번호를 대쉬(-) 기호 전후로 쪼개보자. 성별이 남자면 'male', 여자면 'female'을 출력하세요.
```
```python
t = pin.split('-')
# ['881204', '1068234']

if t[-1].startswith('1'):
    print('male')
else:
    print('female')
# male
```
선생님 답안
```python
if pin.split('-')[1][0] == '1':
# pin을 split으로 나눈 후 2번째 항목의 0번째 값이 1인지 구분하는 것
    print('male')
else:
    print('female')
# male
```
## 문제2) 핸드폰 번호 가리기
전화번호가 문자열 phone_number로 주어졌을 때, 전화번호의 뒷 4자리를 제외한 나머지 숫자를 전부 * 으로 가린 문자열을 출력하세요.   
**제한 조건**   
s는 길이 4 이상, 20이하인 문자열입니다.   
입출력 예
```
phone_number 출력 문자열
"01033334444" "*******4444"
"027778888" "*****8888"
```
```python
phone_number = input()
s1 = '*' * len(phone_number[:-4])
s2 = phone_number[-4:]
s1 + s2
# 01033334444 를 입력했을 시, '*******4444' 출력.
```
   
## 딕셔너리(dictionary)
딕셔너리 = {키1:값1, 키2:값2, 키3:값3, ...}   
키와 값이 쌍을 이루고 있다.  또, 순서가 있는 자료형이 아니다.   
Key에는 변하지 않는 값을 사용하고, Value에는 변하는 값과 변하지 않는 값 모두 사용할 수 있다.
```python
year_pop = {2016 : 9930616, 2017 : 9857426, 2018 : 9838892}

type(year_pop)
# dict / 딕셔너리의 타입을 물어보면 dict 라고 나옴
```
딕셔너리에서는 어떤 값을 찾아가기 위한 유일한 수단이 ‘키’가 된다.   
그러므로 ‘키’는 중복될 수 없다.   
*중복된 키가 있으면 문법 상 오류는 뜨지 않지만, 그 값을 색인하면 중복값 중 뒤에 있는 값이 조회된다.*      
2016년의 population을 알고 싶다면
```python
year_pop[2016]
# 9930616
```
**빈 딕셔너리** 만들기   
딕셔너리 = {}   
딕셔너리 = dict()
```python
x = {}

x = dict()
```
**dict()** 로 딕셔너리 만들기   
딕셔너리 = dict(zip([키1, 키2], [값1, 값2]))   
딕셔너리 = dict([(키1, 값1), (키2, 값2)])
```python
dict(zip(['health', 'melee', 'armor'], [490, 500, 18.72]))

dict([('health', 490), ('melee', 500), ('armor', 18.72)])

# {'health': 490, 'melee': 500, 'armor': 18.72}
```
딕셔너리의 키로 값 조회하기   
딕셔너리[키]
```python
year_pop[2016]
# 9930616
```
딕셔너리의 값 변경하기   
딕셔너리[키] = 값
```python
lux = {(1, 2): 490, 'melee': 500, 'armor': 18.72}

lux['melee'] = 1000
# lux를 출력해보면 {(1, 2): 490, 'melee': 1000, 'armor': 18.72} 로 값이 변경됨

lux['attack_speed'] = 500
# {(1, 2): 490, 'melee': 1000, 'armor': 18.72, 'attack_speed': 500} 
# 위와 같이 값을 추가할 수도 있음! 단, 없는 키를 조회하면 에러.
```
딕셔너리에 키가 있는지 확인하기   
키 in 딕셔너리
```python
'melee' in lux
# True

'power' in lux
# False
```
딕셔너리 키 개수 구하기   
len(딕셔너리)
```python
len(lux)
# 4
```
   
## Workshop
### 문제1) 게임 캐릭터 능력 저장
표준 입력으로 문자열 여러 개와 숫자(실수) 여러 개가 두 줄로 입력됩니다.   
입력된 첫 번째 줄은 키, 두 번째 줄은 값으로 하여 딕셔너리를 생성한 뒤 딕셔너리를 출력하는 프로그램을 만드세요.   
input().split()의 결과를 변수 한개에 저장하면 리스트로 저장됩니다.
```python
(입력 예)
health health_regen mana mana_regen
575.6 1.7 338.8 1.63

(결과)
{'health':575.6, 'health_regen':1.7, 'mana':338.8, 'mana_regen':1.63}
```
```python
key_list = input().split()
val_list = input().split()

dict(zip(key_list, val_list))

# 입력 예를 그대로 입력해보면,
'''
{'health': '575.6',
 'health_regen': '1.7',
 'mana': '338.8',
 'mana_regen': '1.63'}
'''
```
### 문제2) 교통카드 시스템 만들기
표준 입력으로 나이(만 나이)가 입력됩니다(입력 값은 7 이상 입력됨).   
교통카드 시스템에서 시내버스 요금은 다음과 같으며 각 나이에 맞게 요금을 차감한 뒤 잔액이 출력되게 만드세요(if, elif 사용).   
현재 교통카드에는 9,000원이 들어있습니다.
   
- 어린이(초등학생, 만 7세 이상 12세 이하): 650원
- 청소년(중∙고등학생, 만 13세 이상 18세 이하): 1,050원
- 어른(일반, 만 19세 이상): 1,250원
```python
age = int(input())
balance = 9000 # 교통카드 잔액
```
```python
age = int(input())
balance = 9000 # 교통카드 잔액

if 7 <= age <= 12:
    print(balance - 650)
elif 13 <= age <= 18:
    print(balance - 1050)
elif 19 <= age:
    print(balance - 1250)

# 15를 입력했을 시, 청소년 요금이 차감되어 7950이 출력됨
```
하지만 위 코드는 ‘입력 값은 7 이상 입력됨’ 부분을 적용하지 못한 오류가 있다.   
선생님 답안 : 
```python
# 선생님 풀이

age = int(input())
balance = 9000

if 7 <= age <=12: # 어린이
    balance -= 650
elif 13 <= age <= 18: # 청소년
    balance -= 1050
elif age >= 19: # 어른
    balance -= 1250
else:
    print('오류입니다.')
print(balance)
```
