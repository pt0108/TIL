> 부트캠프 1주차 2022년 10월 17일

## 기본 문법
    
파이썬의 타입(자료형)은 미리 지정이 되지 않는다. 입력되는 데이터의 종류에 따라서 결정된다.
```python
a = 3
b = 4

type(a) 
# int

type(b)
# int
```

한 줄에 여러 문장을 작성하고 싶을 때 세미콜론을 사용한다.   
(CSS처럼 작성을 끝마칠 때마다 세미콜론을 사용하지 않음!)
```python
a = 3; b = 4
```

그리고, 파이썬은 **들여쓰기**가 상당히 중요하다. 

띄어쓰기를 4번 하거나, 간단하게 Tab키 한 번만 누르는 방법 등이 있다. (단, 공백과 Tab을 섞어 쓰는 것은 X)
```python
a = 3

if a == 3:
    print("a는 3입니다.")
    print("a가 3이면 이 부분이 실행되는지 확인중입니다.")
    # 여기서 들여쓴 부분은 if문이 실행될 때 출력됨

print("이 부분은 무조건 실행됨")
```
output :
```
a는 3입니다.
a가 3이면 이 부분이 실행되는지 확인중입니다.
이 부분은 무조건 실행됨
```
변수를 생성할 때는, 숫자로 시작하거나, 띄어쓰기를 하거나, 특수 문자를 사용하거나,   
파이썬에 이미 예약된 키워드(if, for, while, and, or, str 등…) 등은 사용할 수 없다.

## 숫자 계산하기
```python
1 + 1
# 2

4 - 3
# 1

2 * 5
# 10

4 / 2
# 2

5 / 2 
# 2.5

5 // 2
# 2 (몫)

5 % 2
# 1 (나머지)

2 ** 10
# 1024 (제곱, 2의 10제곱이 계산됨)
```
또, 괄호( )를 사용해서 연산자의 우선순위를 정할 수도 있다.

## 자료형 변환
type()을 쓰면 데이터의 자료형을 알 수 있다.
```python
a = 2
print(type(a))
# <class 'int'>
```

자료형을 다른 자료형으로 변환시킬 수도 있다.
```python
s = "10"
int(s)
print(type(s))
# type이 'str'에서 'int'로 변환됨
```

## 할당 연산자
```python
a = 3 
```
= 은 **오른쪽에 있는 값을 왼쪽으로 할당**한다는 뜻이다.

```python
a, b = 2, 3
a, b = b, a # a와 b를 맞바꿈
a, b
# (3, 2)
```
파이썬은 이런 식으로 **값을 맞바꿀 수**도 있다.

```python
a = 10 

a += 10
# a = a + 10과 동일, 값은 20.

a -= 10 
# a = a - 10과 동일, 값은 0.

a *= 10
# a = a * 10과 동일, 값은 100.
```
a는 10이라고 했을 때, 할당 연산자로 여러 계산식을 쓸 수 있다.

## Workshop
### 문제 1) 아파트에서 소음이 가장 심한 층수 출력하기
국립환경과학원에서는 아파트에서 소음이 가장 심한 층수를 구하는 계산식을 발표했습니다.   
소음이 가장 심한 층은 **0.2467 * 도로와의 거리(m) + 4.159**입니다.   
다음 소스 코드를 완성하여 소음이 가장 심한 층수가 출력되게 만드세요.   
단, 층수를 출력할 때는 소수점 이하 자리는 버립니다(정수로 출력).  **도로와의 거리: 12m**
```python
int(0.2467 * 12 + 4.159)
# 답: 7(층)
```

### 문제 2) 근의 공식 구하기
근의 공식을 이용하여 x`**`2 + x - 2 = 0의 해를 구하라.
```python
a = 1; b = 1; c = -2

x1 = (-b+(b**2 -4*a*c)**0.5)/2*a
x2 = (-b-(b**2 -4*a*c)**0.5)/2*a
x1, x2
# 답: (1.0, -2.0)
```

## 입력값을 변수에 저장하기

```python
a = input()
# 35를 입력했다면, str '35'로 저장된다. 여기서 a의 타입을 물어도, str로 나온다.
```
**input()**은 **사용자가 입력한 값을 변수에 저장할 수 있는 함수**이다.   
숫자 35가 문자열로 저장되는 이유는, 해당 함수가 **입력받은 값을 문자열로 저장**하기 때문이다.

```python
a = input("숫자를 입력하세요: ")
b = input("숫자를 입력하세요: ")
# input에 "숫자를 입력하세요: "와 같은 값을 넣으면, 입력칸 앞에 출력문구가 뜬다.
```
위에서 각각 10, 20을 입력했다. 여기서 둘을 더하면 어떻게 될까?
```python
a + b 
# '1020' , 말 그대로 문자 10과 20이 더해진 결과가 나온다.

int(a) + int(b)
# 30 , 문자열을 int를 사용해서 숫자로 바꿨더니 10과 20이 더해진 결과가 나왔다.
```

## split()
문자열에서 제공하는 split 함수는 whitespace(스페이스 등) 기준으로 나눈 결과를 리스트로 반환한다.
```python
# two_num 이라는 함수를 만들고, '10 20' 을 입력한 상태.

two_num_list = two_num.split()
two_num_list
# ['10', '20'] 
```

또, split 함수에 구분자를 지정하면 그에 맞게 나눈 결과가 리스트로 반환된다.
```python
"abc:def".split(':')
# ['abc', 'def']
```

## map()
map 함수는 리스트 안에 있는 원소 모두를 **일괄 적용**할 때 사용한다.
```python
two_num_list = list(map(int, two_num_list))
two_num_list
# [10, 20] , int 함수를 사용했기 때문에 리스트 안의 문자열이 숫자로 바뀌었음!
```

```python
# (1) 두 개 이상 입력받기
n = input("숫자 두 개를 입력하세요 : ")

# (2) 구분자를 통해 나누기
l = n.split()

# (3) 일괄 자료형 변환
l1, l2 = map(int, l)
l1, l2

# 이를 실행하면 최종적으로 (5, 8) 이 나온다.
```

## Workshop
### 문제1) 정수 세 개를 입력 받고 합계 출력하기
```python
x, y, z = map(int, input("세 개의 정수를 입력하세요 : ").split())
print(x+y+z)

# 3 5 8 을 입력했다면 16 출력됨.
```

### 문제2) 평균 점수 구하기
표준 입력으로 국어, 영어, 수학, 과학 점수가 입력됩니다.   
평균 점수를 출력하는 프로그램을 만드세요(input에서 안내 문자열은 출력하지 않아야 합니다.)   
단, 평균 점수를 출력할 때는 소수점 이하 자리는 버립니다(정수로 출력).
```python
k, e, m, s = map(int, input().split())
avg = (k+e+m+s)//4
print(avg)
# 58 80 93 70 을 입력했다면 75 출력됨.
```

## 출력 방법 알아보기
print(값1, 값2, 값3, ...)   
print(변수1, 변수2, 변수3, ...)
```python
print(1, 2, 3, 4)
# 1 2 3 4

print(k, e, m, s)
# (위의 Workshop 문제풀이에서 입력한 58, 80, 93, 70) 58 80 93 70
```

print(값1, 값2, 값3, ... **sep** = '문자' 또는 '문자열')   
print(변수1, 변수2, 변수3, ... sep = '문자' 또는 '문자열')   
sep의 기본값은 공백(white space)
```python
print(1, 2, 3, 4, sep = '! ')
# 1! 2! 3! 4

print(k, e, m, s, sep = ', ')
# 58, 80, 93, 70

print(2, 3, sep = 'X')
# 2X3
```

개행문자(\n)라는 제어문자를 지정하면 줄바꿈이 되어서 출력된다.
```python
print(1, 2, 3, sep = '\n')

'''
1
2
3
'''

print(1, 2, 3, sep = '\t')
# '\t'를 쓰면 문자의 뒤에 Tab키만큼의 공간이 들어간다.
```

print(값1, 값2, 값3, ... **end** = '문자' 또는 '문자열')      
print(변수1, 변수2, 변수3, ... end = '문자' 또는 '문자열')   
end의 기본값은 줄바꿈
```python
print(1, 2, 3, 4)
print(5, 6, 7, 8)

'''
1 2 3 4 
5 6 7 8

이런식으로 줄바꿈이 기본값으로 들어가있다.
'''

print(1, 2, 3, 4, end = ' ')
print(5, 6, 7, 8)

# 1 2 3 4 5 6 7 8 
```

## Workshop
### 문제) 날짜와 시간 출력하기
2022/10/17 16:26:06
```python
year = 2022
month = 10
day = 17
hour = 16
minute = 26
second = 6
```
```python
# 날짜
print(year, month, day, sep = '/', end = ' ')

# 시간
print(hour, minute, sep = ':', end = ':')
print('%02d'% second) # 총 두자리를 할당하고, 빈자리는 0을 넣는 '%02d'

# 2022/10/17 16:16:06
```

## bool 자료형과 비교 연산자
bool은 boolean, 불린형을 뜻한다.   
참과 거짓을 나타내는 값이라고 생각하면 된다! (True/False)

숫자 비교하기
```python
10 == 10
# True / 10과 10이 같은지 비교

10 != 5
# True / 10과 5가 다른지 비교
```

문자열도 비교가 가능하다. 추가로, 파이썬은 대소문자도 구분한다.
```python
'python' == 'Python'
# False
```

당연히 부등호도 사용할 수 있다.
```python
10 > 20
# False / 10이 20보다 큰지 비교

10 <= 10
# True / 10이 10보다 작거나 같은지 비교
```