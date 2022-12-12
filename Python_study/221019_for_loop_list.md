> 부트캠프 1주차 2022년 10월 19일

## for 와 range 사용하기
- 파이썬에서는 명령을 반복해서 실행되게 하고 싶을 때, **for** loop(for 반복문)를 사용한다.
- 얼만큼 실행되었는지 확인하기 편하게 i도 같이 출력해보았다.
```
for 변수 in range(횟수):
    반복할 코드
```
```python
for i in range(10):
    print("Hello World!", i)

'''
Hello World! 0
Hello World! 1
Hello World! 2
Hello World! 3
Hello World! 4
Hello World! 5
Hello World! 6
Hello World! 7
Hello World! 8
Hello World! 9
'''
```
횟수만 입력할 수 있는 것은 아니다!
```
for 변수 in range(시작, 끝, 증가폭):
    반복할 코드
```
```python
for i in range(0, 10, 2):
    print("Hello World!", i)

'''
Hello World! 0
Hello World! 2
Hello World! 4
Hello World! 6
Hello World! 8
'''
# 당연히 음수도 사용할 수 있다.
```
**enumerate**는 시퀀스 객체의 값뿐만 아니라, *인덱스까지 반환*해준다.
```python
for i, v in enumerate(range(0, 10, 2)):
    print("Hello World!", i, v)

'''
Hello World! 0 0
Hello World! 1 2
Hello World! 2 4
Hello World! 3 6
Hello World! 4 8
'''
```
range만 사용할 수 있는 것은 아니다.   
for 변수 in 시퀀스 객체 (ex: range, list, tuple, str...)
```python
# 문자열
for i in "Hello":
    print(i)
'''
H
e
l
l
o
'''

# 리스트
for i in [1, 2, 3]:
    print(i)
'''
1
2
3
'''

# 튜플
for i in (1, 2, 3):
    print(i)
'''
1
2
3
'''
```
enumerate도 적용이 가능하다.
```
for i in enumerate(시퀀스 객체):
    반복할 코드
```
```python
for i, v in enumerate("Hello"):
    print(i, v)

'''
0 H
1 e
2 l
3 l
4 o
'''
```
**reversed**는 값을 거꾸로 뒤집어서 반환한다고 생각하면 될 것 같다.
```python
for i in reversed(시퀀스 객체):
    반복할 코드for i in reversed((1, 2, 3)):
    print(i)
'''
3
2
1
'''

for i in reversed("Python"):
    print(i)
'''
n
o
h
t
y
P
'''
```
```
for i in reversed((1, 2, 3)):
    print(i)
'''
3
2
1
'''

for i in reversed("Python"):
    print(i)
'''
n
o
h
t
y
P
'''
```

## Workshop
### 문제) 구구단 출력 프로그램
표준 입력으로 정수가 입력됩니다.   
입력된 정수의 구구단을 출력하는 프로그램을 만드세요(input에서 안내 문자열은 출력하지 않아야 합니다).   
출력형식은 숫자 * 숫자 = 숫자 처럼 만들고 숫자와 * , = 사이는 공백을 한칸 띄웁니다.
```
입력 예
2

결과
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
```python
x = int(input()) # 몇단

for y in range(1, 10):
    print(x, '*', y, '=', x * y)

'''
6 * 1 = 6
6 * 2 = 12
6 * 3 = 18
6 * 4 = 24
6 * 5 = 30
6 * 6 = 36
6 * 7 = 42
6 * 8 = 48
6 * 9 = 54
'''
```
이외에도 구구단을 표현할 수 있는 여러가지 방법이 있다.
```python
# option 1. (format 사용하기)
x = int(input())

for y in range(1, 10):
    print("{0} * {1} = {2}".format(x, y, x*y))
'''
5 입력시
5 * 1 = 5
5 * 2 = 10
5 * 3 = 15
5 * 4 = 20
5 * 5 = 25
5 * 6 = 30
5 * 7 = 35
5 * 8 = 40
5 * 9 = 45
'''

# option 2. (서식 지정자 %)
x = int(input())

for y in range(1, 10):
    print("%d * %d = %d" % (x, y, x*y))
'''
3 입력시
3 * 1 = 3
3 * 2 = 6
3 * 3 = 9
3 * 4 = 12
3 * 5 = 15
3 * 6 = 18
3 * 7 = 21
3 * 8 = 24
3 * 9 = 27
'''

# option 3. (문자열 포맷팅(formatting) f를 붙이는 방법)
x = int(input())

for y in range(1, 10):
    print(f"{x} * {y} = {x*y}")
'''
7 입력시
7 * 1 = 7
7 * 2 = 14
7 * 3 = 21
7 * 4 = 28
7 * 5 = 35
7 * 6 = 42
7 * 7 = 49
7 * 8 = 56
7 * 9 = 63
'''
```
개인적으로는 문자열 포맷팅 방식이 가장 편한 것 같다!   
## while 반복문 사용하기
while문은 **조건문이 참인 동안에 while문 아래의 문장이 반복 수행**된다.
```
초기식
while 조건식:
    반복할 코드
    변화식
```
```python
# Hello World를 10번 출력
i = 10
while i > 0 :
    print("Hello World!", i)
    i -= 1

'''
Hello World! 10
Hello World! 9
Hello World! 8
Hello World! 7
Hello World! 6
Hello World! 5
Hello World! 4
Hello World! 3
Hello World! 2
Hello World! 1
'''
```

## Workshop
### 문제 1) 주사위 던지고 눈을 출력하는 동작을 계속 반복하다가 "3"이 나왔을때 멈추기
*random 모듈의 randint 함수는 파이썬 내장 함수가 아니기 때문에 import 해와야 한다.   
→ 이건 노마드 코더 파이썬 강의에서 알게된 것인데, 파이썬 표준 라이브러리에서 제공하는 여러 모듈의 함수들을 참고해서 쓰면 좋다.   
(그 강의에서도 randint 함수를 사용한 숫자 맞추기 게임을 만들었었다.)   
또, 표준 라이브러리에도 없는 수많은 코드들은 pypi 라는 곳에서 찾아볼 수 있다.*
```python
import random

x = random.randint(1, 6) # 1에서 6사이의 무작위수 추출

while x != 3 :
    x = random.randint(1, 6) # 반복할 코드 + 변화식
    print(x)

'''
5
2
5
4
2
4
3
'''
# 이와 같이 무작위로 1부터 6 사이의 숫자를 출력하다가, 3이 나오면 실행을 멈춘다.
```
### 문제 2) 교통카드 잔액 출력하기
표준입력으로 금액(정수)이 입력됩니다.   
1회당 요금은 1,350이고, 교통카드를 사용했을 때마다의 잔액을 각 줄에 출력하는 프로그램을 만드세요  
(input에서 안내 문자열은 출력하지 않아야 합니다).   
단, 최초 금액은 출력하지 않아야 합니다. 그리고 잔액은 음수가 될 수 없으며 잔액이 부족하면 출력을 끝냅니다.
```python
balance = int(input())

while balance >= 1350:
    balance -= 1350
    print("잔액: ", balance, "원")

'''
15000 입력시

잔액:  13650 원
잔액:  12300 원
잔액:  10950 원
잔액:  9600 원
잔액:  8250 원
잔액:  6900 원
잔액:  5550 원
잔액:  4200 원
잔액:  2850 원
잔액:  1500 원
잔액:  150 원
'''
```
### 문제 3) 3으로 끝나는 숫자만 출력하기
0과 73 사이의 숫자 중 3으로 끝나는 숫자만 출력되게 만드세요.
```
출력예
3 13 23 33 43 53 63 73
```
```python
for i in range(74):
    if (i % 10) == 3:
        print(i, end=" ")

# 3 13 23 33 43 53 63 73
```
→ 10으로 나눈 i의 나머지를 구하는 이유는, 3으로 끝나는 숫자는 10으로 나누면 나머지가 3이 나오기 때문이다!   
또, break와 continue를 사용해서 문제를 풀 수도 있다. 그 전에 이 둘의 용도를 알아보자.
```python
# break 예시
i = 0
while True:
    print(i)
    i += 1
    if i == 10:
        break # break는 반복문을 탈출함
'''
0
1
2
3
4
5
6
7
8
9
'''
```
```python
# conitnue 예시 / continue는 코드 실행을 건너뜀
for i in range(74):
    if (i % 10) != 3:
        continue
    else:
        print(i, end=" ")

# 3 13 23 33 43 53 63 73
```
이제 break와 continue를 같이 사용하면 아래와 같이 쓸 수 있다.
```python
i = 0

while True:
    if i % 10 != 3:
        i += 1
        continue
        
    if i > 73:
        break
    print(i, end=" ")
    i += 1

# 3 13 23 33 43 53 63 73
```
### 문제 4) 알파벳별 빈도 사전 등록
다음의 주어진 문자열 s에서 알파벳 별 빈도를 사전형인 d에 등록하는 파이썬 코드블럭을 작성하시오.
```python
s = 'life is short, so python is easy.'
punct = ',. '
d = {}

결과 print(d) (순서는 상관 없음)
{'a': 1, 'e': 2, 'f': 1, 'i': 3, 'h': 2, 'l': 1, 'o': 3, 'n': 1, 'p': 1, 's': 5, 'r': 1, 't': 2, 'y': 2}
```
```python
s = 'life is short, so python is easy.'
punct = ',. '
d = {}

for c in s:
    if c in punct: # 특수기호나 공백은 건너뜀
        continue
    if c not in d: # d에 없던 키가 들어가면 값에 1을 넣음 / d['l'] = 1
        d[c] = 1 
    else: # d에 있는 키가 또 추가되면 기존 값에 1을 더함 / d['l'] = 2
        d[c] += 1 

print(d, end=" ")

# {'l': 1, 'i': 3, 'f': 1, 'e': 2, 's': 5, 'h': 2, 'o': 3, 'r': 1, 't': 2, 'p': 1, 'y': 2, 'n': 1, 'a': 1}
```
   
## 중첩 루프 사용하기
**반복문 안에 반복문이 들어가는 형태**를 중첩 루프(다중 루프)라고 한다.
```python
for j in range(5):
    for i in range(5):
        print('*', end=" ")
    print()

'''
* * * * * 
* * * * * 
* * * * * 
* * * * * 
* * * * *
'''
```
계단식으로 별 출력하기(1)
```python
for i in range(5): # i : 0 -> 1 -> 2 -> 3 -> 4
    for j in range(i+1):
        print('*', end='') # 첫번째 행은 * 1개, 두번째 행은 * 2개, ...
    print()

'''
*
**
***
****
*****
'''
```
계단식으로 별 출력하기(2)
```python
for i in range(5): # i : 0 -> 1 -> 2 -> 3 -> 4
    # 1. 공백
    for j in range(i): # j : 0 -> 1 -> 2 -> 3 -> 4
        print(" ", end="")
    # 2. 별
    for k in range(5-i): # k : 5 -> 4 -> 3 -> 2 -> 1
        print("*", end="")
    print()

'''
*****
 ****
  ***
   **
    *
'''
```
별로 산 만들기
```python
for i in range(5): # i : 0 -> 1 -> 2 -> 3 -> 4
    # 1. 공백
    for j in range(5-i): # j : 4 -> 3 -> 2 -> 1 -> 0
        print(" ", end="")
    # 2. 별
    for k in range(2*i+1): # k : 1 -> 3 -> 5 -> 7 -> 9
        print("*", end="")
    print()

'''
     *
    ***
   *****
  *******
 *********
'''
```
- FizzBuzz 문제
1에서 100까지 출력   
3의 배수는 Fizz 출력   
5의 배수는 Buzz 출력   
3과 5의 공배수는 FizzBuzz 출력
```python
for i in range(1, 101):
    if (i % 3) == 0 and (i % 5) == 0: # 3과 5의 공배수, 최우선순위로 실행한다. 
        print("FizzBuzz")
    elif (i % 3) == 0: # 3의 배수
        print("Fizz")
    elif (i % 5) == 0: # 5의 배수
        print("Buzz")
    else:
        print(i)
```
   
## 리스트 응용하기
**append** : 요소 하나를 추가   
**extend** : 리스트를 연결하여 확장   
**insert** : 특정 인덱스에 요소 추가
```python
a = [10, 20, 30]
```
- append
```python
a.append(500)
a
# [10, 20, 30, 500]

a = [] # 빈 리스트에도 추가가 가능함
a.append(10)
a
# [10]
```
- extend
```python
a = [10, 20, 30]
b = [40, 50, 60]

a.extend(b)

a
# [10, 20, 30, 40, 50, 60]
```
extend는 a를 기준으로 모두 다 합쳐진다.   
a + b 와 같은 + 연산은 a와 b가 그대로 유지된다.
- insert
```python
a = [10, 20, 30]
a.insert(1, 500)
a # 1번째 자리에 500이 삽입됨
# [10, 500, 20, 30]
```
   
**insert(0, 요소)**: 리스트의 맨 처음에 요소를 추가
**insert(len(리스트), 요소)**: 리스트의 맨 끝에 요소를 추가
```python
a = [10, 20, 30]
a.insert(0, 100)
a
# [100, 10, 20, 30]

len(a)
# 4

a.insert(len(a), 1000)
a
# [100, 10, 20, 30, 1000]

a.insert(-1, 2000)
a
# [100, 10, 20, 30, 2000, 1000]
```
   
**pop**: 마지막 요소 또는 특정 인덱스의 요소를 삭제   
**remove**: 특정 값을 찾아서 삭제
   
- pop
```python
a = [10, 20, 30]
x = a.pop() # 특정 인덱스를 지정하지 않아 마지막 요소를 삭제
x # 30

a
# [10, 20]
```
```python
a = [10, 20, 30]
x = a.pop(1) # 인덱스를 찾아서 삭제
x # 20

a
# [10, 30]
```
   
- remove
```python
a = [10, 20, 30]
a.remove(30) # 값을 찾아서 삭제

a
# [10, 20]
```
   
**index(값)**: 리스트에서 특정 값의 인덱스 구함   
**count(값)**: 리스트에서 특정 값의 개수를 구함
   
- index
```python
a = [10, 20, 30]
a.index(20) 
# 1
```
→ 추가로, 존재하지 않는 값을 구하려고 하면 에러가 발생한다.
   
- count
```python
a = [10, 10, 20, 30, 30, 30]
a.count(30)
# 3
```
   
**reverse()**: 리스트에서 요소의 순서를 반대로 뒤집음   
**sort()**: 리스트의 요소를 정렬함(기본값: 오름차순)   
**clear()**: 리스트의 모든 요소를 삭제함
```python
a = [10, 20, 30] 
a.reverse()
a
# [30, 20, 10]

a = [10, 50, -1, 0, 4, 10000]
a.sort()
a
# [-1, 0, 4, 10, 50, 10000]

a = [10, 50, -1, 0, 4, 10000]
a.sort(reverse=True) # 기본값은 reverse=False
a
# [10000, 50, 10, 4, 0, -1]
```
   
= : 같은 공간을 공유한다.
```python
a = [0, 0, 0, 0]
b = a

a is b # True
```
b = a 라고 했을 때, a is b는 True가 나온다. 여기서 b만 수정해보면
```python
b[1] = 1000
b
# [0, 1000, 0, 0]

a
[0, 1000, 0, 0]
```
위처럼 b의 1번째 인덱스만 수정했는데 a도 똑같이 수정된 모습을 볼 수 있다. 
   
**copy()** : 별도의 공간이 할당된다.
```python
a = [0, 0, 0, 0]
b = a.copy()

a is b
# False
```
copy를 사용하면 = 을 사용했을 때와 다르게 a is b가 False로 나온다.   
아까처럼 b의 1번째 인덱스를 수정하면 쉽게 이해할 수 있다.
```python
b[1] = 1000
b
# [0, 1000, 0, 0]

a
# [0, 0, 0, 0]
```
   
- copy()와 deepcopy()
위에서 말했듯, copy된 리스트는 원본 리스트에 영향을 미치지 않는다.   
하지만 아래와 같은 2차원 리스트에서는 문제가 발생한다.
```python
a = [[10, 20], [30, 40]] # 2차원 리스트
b = a.copy()

b[0][0] = 1000
b
# [[1000, 20], [30, 40]] 
# b의 0번째 리스트의 0번째 인덱스를 변경

a
# [[1000, 20], [30, 40]] 
```
방금 배운대로라면 분명 a의 값은 수정되지 않았어야 한다. 하지만 copy는 2차원 리스트에서 제 역할을 하지 못한다.   
이럴 때, copy 모듈의 deepcopy를 사용하면 된다!
```python
import copy

a = [[10, 20], [30, 40]] 
b = copy.deepcopy(a)

b[0][0] = 1000
b
# [[1000, 20], [30, 40]]

a
# [[10, 20], [30, 40]]
```
   
- 반복문으로 리스트 요소 출력하기
for 요소 in 리스트:
```python
a = [10, 20, 30]
for v in a:
    print(v)
'''
10
20
30
'''
```
for 인덱스, 요소 in enumerate(리스트):
```python
a = [10, 20, 30]
for i, v in enumerate(a, start=1):
    print(i, v)

'''
1 10
2 20
3 30
'''
```
   
- 리스트의 가장 작은 수, 가장 큰 수, 합계
```python
a = [10, 20, 30]

min(a) # 가장 작은 수
# 10 

max(a) # 가장 큰 수
# 30 

sum(a) # 합계
# 60

sum(a)/len(a) # 평균값
# 20.0
```
   
- 리스트 표현식
[식 for 변수 in 리스트]
```python
list(range(10))
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

# 1. for문 이용, list의 append()함수 이용
l = []
for i in range(10):
    l.append(i*2)
l
# [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]

# 2. 리스트 표현식
[i*2 for i in range(10)]
# [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```
보다시피, 리스트 표현식을 사용하는 것이 훨씬 짧고 간결하다.   
이번에는 단어의 길이를 리스트로 구해보자.
```python
word_list = ["python", "is", "easy"]

# 1. for문 이용
word_count = []
word_list = ["python", "is", "easy"]
for word in word_list:
    word_count.append(len(word))
word_count
# [6, 2, 4]

# 2. 리스트 표현식 
[len(word) for word in word_list]
# [6, 2, 4]
```
   
[식 for 변수 in 리스트 if 조건식]   
1 ~10 까지의 숫자에서 짝수인 경우만 출력해보자.
```python
# 1. for문 이용
l = []
for i in range(10):
    if i % 2 == 0:
        l.append(i)
l
# [0, 2, 4, 6, 8]

# 2. 리스트 if 조건식
[i for i in range(10) if i % 2 == 0]
# [0, 2, 4, 6, 8]
```
   
## Workshop
### 문제) 리스트에서 특정 요소만 뽑아내기
리스트 a에 들어있는 문자열 중에서 길이가 5인 것들만 리스트 형태로 출력되게 만드세요
```python
a = ['alpha', 'bravo', 'charlie', 'delta', 'echo', 'foxtrot', 'golf', 'hotel', 'india']
```
```python
result = [a1 for a1 in a if len(a1) == 5]
print(result)

# ['alpha', 'bravo', 'delta', 'hotel', 'india']

# 만약 for문을 썼다면
l = []
for i in a: # 9번 순회
    if len(i) == 5:
        l.append(i)
```
- 리스트에서 map 사용하기
**map()**: 리스트나 튜플의 요소를 지정된 함수로 처리해주는 함수   
→ map은 원본 리스트나 튜플을 변경하지 않고 새 리스트를 생성한다.
```python
a = [1.2, 2.5, 3.7, 4.6]
l = []
for i in a:
    l.append(int(i))
l
# [1, 2, 3, 4]
```
for 문을 사용하면 위처럼 작성해야 한다.  
그러나 map을 사용해서 일괄 적용하면 아래와 같이 짧게 쓸 수 있다.
```python
list(map(int, a))
# [1, 2, 3, 4]
```
   
## 튜플 응용하기
튜플은 읽기만 가능하기 때문에 사용 가능한 메소드가 거의 없다.
   
index(값): 특정값의 인덱스 구하기
```python
a = (10, 20, 30)
a.index(30)
# 2
```
   
count(값): 특정값의 개수 구하기
```python
a = (10, 10, 10, 20, 20, 30)
a.count(10)
# 3
```
   
## Workshop
### 문제) 자동 로또 생성기
- 1~45 숫자 중에서 6개를 고르는 로또 번호를 자동으로 만들어 주는 프로그램 작성하기
- 사용자가 입력한 개수만큼 번호 쌍을 생성하기(예: 5를 입력하면 5 세트의 번호가 생성되도록 하기)
- 한번 뽑힌 것은 뽑히지 않도록 하고, 최종 출력은 오름차순 정렬해서 보여주기
```python
import random

count = int(input("로또를 몇회 뽑으시겠습니까? : "))

total = []
for i in range(count):
    lotto = []

    while True:       
        pick = random.randint(1, 45)
        if pick not in lotto:
            lotto.append(pick)

        if len(lotto) >= 6:
            break
    lotto.sort()
    total.append(lotto)
total

'''
5 입력시
[[1, 20, 25, 31, 43, 45],
 [7, 11, 16, 30, 32, 39],
 [1, 2, 13, 19, 21, 44],
 [9, 12, 37, 41, 42, 45],
 [9, 10, 25, 35, 38, 42]]
'''
```
여기서 randint 가 아닌 sample을 사용하면 더 간단하게 작성할 수 있다.
```python
import random

count = int(input("로또를 몇회 뽑으시겠습니까? : "))

total = []
for i in range(count):     
    lotto = random.sample(range(1, 45), 6)
    lotto.sort()
    total.append(lotto)
total

# 3 입력시
# [[6, 13, 22, 31, 35, 38], [2, 8, 10, 26, 38, 40], [6, 7, 18, 27, 29, 33]]
```
파이썬 표준 라이브러리에서는 sample을   
“중복 없는(without replacement) 무작위 표본 추출(sampling)에 사용됩니다. “라고 설명하고 있다.   

## 문자열 응용하기
- replace('바꿀 문자열', '새 문자열') : 문자열 바꾸기
```python
s = "Hello World!"
result = s.replace('World!', 'Python!')
result
# 'Hello Python!'
```
   
- split('기준 문자열') : 문자열 분리하기
```python
s = 'apple pear grape pineapple orange'
result = s.split()
result
# ['apple', 'pear', 'grape', 'pineapple', 'orange']

s = 'apple.pear.grape.pineapple.orange'
result = s.split('.')
result
# ['apple', 'pear', 'grape', 'pineapple', 'orange']
```
   
- '구분자'.join(리스트): 문자열 삽입
```python
'/'.join(result)
# 'apple/pear/grape/pineapple/orange'
```
   
upper() : 대문자로 바꿈   
lower() : 소문자로 바꿈   
strip() : 문자열 양쪽에 있는 연속된 모든 공백을 삭제   
lstrip() : 문자열 왼쪽에 있는 연속된 모든 공백을 삭제   
rstrip() : 문자열 오른쪽에 있는 연속된 모든 공백을 삭제
```python
'python'.upper()
# 'PYTHON'

'PYTHON'.lower()
# 'python'

'     Python     '.strip()
# 'Python'

'     Python     '.lstrip()
# 'Python     '

'     Python     '.rstrip()
# '     Python'

' ,  . . ..  Python  . . ,.   '.strip(',. ') # 기본값이 공백인 것이지, 무조건 공백만 삭제하는 것은 아님.
# 'Python'

'python'.center(20) 
# '       python       '
# 20(길이)만큼의 전체 사이즈를 확보하고 문자열을 중간에 배치 / 중앙정렬 같은 기능?
```
*참고 (10/21 추가)*
단어 리스트에서 개별 단어들 strip 을 하고 싶으면 ···
```python
a = ["abc.", "def,"]

[word.strip(',.') for word in a] # 리스트 표현식 이용
# ['abc', 'def']
```
```
list(map(lambda x:x.strip(',.'), a)) # map과 lambda 함수 이용
# ['abc', 'def']
```
   
index('찾을 문자열') : 문자열에서 특정 문자열을 찾아서 인덱스를 반환하고, 없으면 에러 발생   
find('찾을 문자열') : 문자열에서 특정 문자열을 찾아서 인덱스를 반환하고, 없으면 -1 반환
```python
s = 'apple pear grape pineapple orange'

s.index('pl') # 왼쪽부터 찾음
# 2

s.rindex('pl') # 오른쪽부터 찾음
# 23

s.index('ppp') # -> 에러 발생

s.find('ppp') # -1

s.find('pl') # 인덱스와 똑같이 작용, 왼쪽부터 찾음
# 2

s.rfind('pl') # 오른쪽부터 찾음
# 23
```
   
count('문자열') : 현재 문자열에서 특정 문자열이 몇번 나오는지 알아냄
```python
s = 'apple pear grape pineapple orange'

s.count('pl')
# 2
```
   
- 서식 지정자 ( = 문자열 포맷 코드)
아래에서 사용한 코드만 간단하게 설명을 써봄!   
**%s** = 문자열(string)   
**%d** = 정수(integer)   
**%f** = 부동 소수(floating-point)
```python
name = '냉동감자'
"나는 %s 입니다." % name 
# '나는 냉동감자 입니다.'

age = 23
"나이는 %d살 입니다." % age
# '나이는 23살 입니다.'

score = 4.2
"내 학점은 %.2f 입니다." % score
# '내 학점은 4.2 입니다.'
```
합쳐서 한번에 쓸 수도 있다.
```
name = '냉동감자'
age = 23
score = 4.2

"나는 %s 입니다. 나이는 %d살 입니다. 내 학점은 %.2f 입니다." % (name, age, score)
# '나는 냉동감자 입니다. 나이는 23살 입니다. 내 학점은 4.20 입니다.'
```
   
- format 함수
```python
name = '냉동감자'
"나는 {} 입니다.".format(name)
# '나는 냉동감자 입니다.'
```
format 역시 한번에 사용이 가능하다.
```python
name = '냉동감자'
age = 23
score = 4.2

"나는 {} 입니다. 나이는 {}살 입니다. 내 학점은 {} 입니다.".format(name, age, score)
# '나는 냉동감자 입니다. 나이는 23살 입니다. 내 학점은 4.2 입니다.'
```
   
- f 포맷팅
파이썬 3.6부터 사용 가능한 기능이다.   
아래와 같이 문자열 앞에 f 접두사를 붙이면 기능을 사용할 수 있다.
```python
name = '냉동감자'
age = 23
score = 4.2

f"나는 {name} 입니다. 나이는 {age}살 입니다. 내 학점은 {score} 입니다."
# '나는 냉동감자 입니다. 나이는 23살 입니다. 내 학점은 4.2 입니다.'
```
