> 부트캠프 1주차 2022년 10월 20일
## 딕셔너리 응용하기
**setdefault** : 키-값 쌍 추가   
**update** : 키의 값 수정, 키가 없으면 키-값 쌍 추가
```python
x = {'a':10, 'b':20, 'c':30, 'd':40}

x.setdefault('e', 50)
x
# {'a': 10, 'b': 20, 'c': 30, 'd': 40, 'e': 50}

x.setdefault('f') # 키만 추가할 수도 있음. (대신 값에 None이 들어감)
x
# {'a': 10, 'b': 20, 'c': 30, 'd': 40, 'e': 50, 'f': None}

x.update({'a':100, 'b':200})
x
# {'a': 100, 'b': 200, 'c': 30, 'd': 40, 'e': 50, 'f': None}

x.update({'a':1000, 'b':2000, 'g':1000})
x
# {'a': 1000, 'b': 2000, 'c': 30, 'd': 40, 'e': 50, 'f': None, 'g': 1000}
```
위와 같이 update는 단순히 수정만 하는 것이 아니라, 키-값 쌍을 수정할 수도 있다.
   
   
**pop(키)** : 특정 키-값 쌍을 삭제한 뒤, 삭제한 값을 반환   
**pop(키, 기본값)** : 키가 없을 때 기본값을 반환   
**clear()** : 딕셔너리의 모든 키-값 쌍을 삭제   
*(키가 없을 때 기본값을 반환하는 것은, 에러를 방지하기에 좋은 기능인 것 같다)*
```python
x
# {'a': 1000, 'b': 2000, 'c': 30, 'd': 40, 'e': 50, 'f': None, 'g': 1000}

result = x.pop('a')
result
# 1000

x
# {'b': 2000, 'c': 30, 'd': 40, 'e': 50, 'f': None, 'g': 1000}
# a와 값이 삭제된 것을 알 수 있음.
```
```python
result = x.pop('a', 0)
result # 'a'가 없기 때문에 입력한 기본값인 0을 반환함
# 0

result = x.pop('b', 0)
result # 'b'가 있기 때문에 'b'의 값인 2000 반환
# 2000

x
# {'c': 30, 'd': 40, 'e': 50, 'f': None, 'g': 1000}
```
   
**get(키)** : 특정 키의 값을 가져옴   
**get(키, 기본값)** : 키가 없을 때 기본값을 반환
```python
result = x.get('c')
result
# 30

x # get은 가져오기만 할 뿐이기 때문에 'c'는 삭제되지 않고 여전함.
# {'c': 30, 'd': 40, 'e': 50, 'f': None, 'g': 1000}

result = x.get('z', 0)
result # 'z'라는 키는 없기 때문에 0을 반환.
# 0
```
   
**items()** : 키-값 쌍을 모두 가져옴   
**keys()** : 키를 모두 가져옴   
**values()** : 값을 모두 가져옴   
→ 이런 함수들은 보통 단독으로 사용하지 않고, for문과 연계해서 씀(10/19에 자주 썼던 range의 경우를 떠올리면 됨!)
```python
x
# {'c': 30, 'd': 40, 'e': 50, 'f': None, 'g': 1000}

x.items()
# dict_items([('c', 30), ('d', 40), ('e', 50), ('f', None), ('g', 1000)])

x.keys()
# dict_keys(['c', 'd', 'e', 'f', 'g'])

x.values()
# dict_values([30, 40, 50, None, 1000])
```
   
for 키, 값 in 딕셔너리.items():
```python
for k, v in x.items():
    print(k, v)
'''
c 30
d 40
e 50
f None
g 1000
'''

for k in x.keys():
    print(k)
'''
c
d
e
f
g
'''

for k in x.values():
    print(k)
'''
30
40
50
None
1000
'''
```
   
- **세트**
세트 = {값1, 값2, 값3, ...}   
세트는 중복이 없고(유일한 값만 사용), 순서도 없다.
```python
fruits = {'strawberry', 'grape', 'orange', 'pineapple', 'cherry'}

fruits = {'strawberry', 'strawberry', 'strawberry', 'grape', 'orange', 'pineapple', 'cherry'}
fruits # 중복된 값을 넣어도 유일한 값만 나온다.
# {'cherry', 'grape', 'orange', 'pineapple', 'strawberry'}
```
```python
x = {'a', 'a', 'b'}
y = {'a', 'b', 'a'}
z = {'b', 'a'}

x == y
# True 

y == z
# True

x == z
# True
```
→ x, y, z 셋의 유일한 값은 결국 'a'와 'b'뿐이기 때문에 True가 나오는 것이다.   
   
추가로, 빈 세트를 만들 때 그냥 중괄호를 사용하면 안된다.
```python
l = [] # l = list()
t = () # t = tuple()
d = {} # d = dict()

# 빈 세트 만드는 법. 단순히 중괄호를 쓰는 것은 딕셔너리와 중복되므로 사용 불가.
s = set()
```
   
## Workshop
### 문제1) 리스트와 반복문
아래에 주어진 리스트 l1의 요소 중에서 l2의 요소와 값이 같은 경우 삭제하는 파이썬 코드 작성하기
```python
l1 = ['a', 'b', 'c', 'd', 'a', 'b', 'a', 'b']
l2 = ['b', 'a']
결과 l1
['c', 'd']
```
```python
l1 = ['a', 'b', 'c', 'd', 'a', 'b', 'a', 'b']
l2 = ['b', 'a']

for c2 in l2: # b->a
    while c2 in l1: # while을 사용해서 l2안의 값인 c2가 l1 안에서 전부 삭제되게 함.
        print(c2, 'will be removed') 
        l1.remove(c2)

l1

'''
b will be removed
b will be removed
b will be removed
a will be removed
a will be removed
a will be removed

['c', 'd']
'''
```
삭제 과정을 눈으로 보고 이해하기 쉽게 출력 문구를 넣었다.   
출력 문구를 보면 b와 a가 전부 삭제될 때까지 계속 실행되는 것을 알 수 있다.
```python
# 참고
l1 = ['a', 'b', 'c', 'd', 'a', 'b', 'a', 'b']
l2 = ['b', 'a']

list(set(l1) - set(l2))

#['d', 'c']
```
   
### 문제2) 'the'의 개수 출력하기
아래 문자열에서 'the'의 개수를 출력하는 프로그램을 만드세요.   
단 , 모든 문자가 소문자인 'the'만 찾으면 되며 'them', 'there', 'their' 등은 포함되지 않아야 합니다.
```
the grown-ups' response, this time, was to advise me to lay aside my drawings of boa 
constrictors, whether from the inside or the outside, and devote myself instead to 
geography, history, arithmetic, and grammar. That is why, at the, age of six, I gave 
up what might have been a magnificent career as a painter. I had been disheartened 
by the failure of my Drawing Number One and my Drawing Number Two. Grown-ups never 
understand anything by themselves, and it is tiresome for children to be always and 
forever explaining things to the.
```
```python
paragraph = "the grown-ups' response, this time, was to advise me to lay aside my drawings of boa constrictors, whether from the inside or the outside, and devote myself instead to geography, history, arithmetic, and grammar. That is why, at the, age of six, I gave up what might have been a magnificent career as a painter. I had been disheartened by the failure of my Drawing Number One and my Drawing Number Two. Grown-ups never understand anything by themselves, and it is tiresome for children to be always and forever explaining things to the."

# paragraph.count('the') 
# their, them 이런 단어까지 모두 count하므로 사용 불가
```
```python
word_list = paragraph.split()
count = 0
for word in word_list:
    if word.strip(',.') == 'the':        
        count += 1 # 0번째부터 세는 것을 고려
count
# 6
```
→ 우선 paragraph 를 split 해서 word_list 에 담는다. 그리고 출력될 count 에 0을 넣고 준비해둔다.   
word_list 안의 것을 word 로 정하고, ‘,.’ 은 strip으로 지운다. 그러면 온전한 ‘the’의 개수만 구할 수 있다.
   
### 문제3) 평균 점수 구하기
다음 소스 코드를 완성하여 평균 점수가 출력되게 만드세요.
```python
maria = {'korean' : 94, 'english': 91, 'mathmatics': 89, 'science': 83 }
```
```python
# 내가 적은 답

list(maria.values()) 
a = sum(list(maria.values()))/len(list(maria.values()))
print(a)
# 89.25
```
```
# option 1

total_v = 0
for v in maria.values():
    total_v = total_v + v
total_v/len(maria)
# 89.25
```
위 방법은 total_v 라는 그릇을 만들어두고, v의 합계를 넣은 다음 len(maria) 만큼 나누는 방법이다. *len(maria)는 4다!*
```
# option 2

sum(maria.values())/len(maria)
# 89.25
```
   
### 문제4) 특정값 삭제하기 *(개인적으로 상당히 어렵게 느껴져서 강조!)*
표준 입력으로 문자열 여러개와 숫자 여러개가 두 줄로 입력되고, 첫 번째 줄은 키, 두번째 줄은 값으로 하여 딕셔너리를 생성합니다.   
다음 코드를 완성하여 딕셔너리에서 키가 'delta'인 키-값 쌍과 값이 30인 키-값 쌍을 삭제하도록 만드세요.
```python
입력
alpha bravo charlie delta
10 20 30 40
결과
{'alpha':10, 'bravo':20}
```
   
(1) 인풋
```python
keys = input("key : ").split()
values = list(map(int, input("value : ").split()))
# key : alpha bravo charlie delta
# value : 10 20 30 40

keys
# ['alpha', 'bravo', 'charlie', 'delta']

values
# [10, 20, 30, 40]
```
우선 각각 문자열과 숫자들을 keys 와 values 에 리스트 형태로 넣는다.   
values 는 입력된 문자열의 공백을 split으로 삭제하고, map 함수로 int를 일괄 적용해서 숫자형으로 바꾼다.
      
(2) 딕셔너리 구성
```python
d = dict(zip(keys, values))
d
# {'alpha': 10, 'bravo': 20, 'charlie': 30, 'delta': 40}
```
리스트로 값이 저장된 keys와 values를 딕셔너리로 만드는데, zip 함수를 사용해서 키-값 쌍으로 묶어준다.
      
(3) ‘delta’ 키 삭제
```python
# del d['delta']

d.pop('delta')
d
# {'alpha': 10, 'bravo': 20, 'charlie': 30}
```
del을 사용해서 딕셔너리 안의 ‘delta’ 를 삭제할 수 있고, pop 메소드를 사용해서 삭제할 수도 있다. 
      
(4) 30 값 삭제
```python
n = {} # new dict 생성
for k, v in d.items():
    if v != 30:
        n.setdefault(k, v) # 값이 30이 아닌 경우만 n에 추가.
n
# {'alpha': 10, 'bravo': 20}
```
이제 n이라는 빈 딕셔너리를 생성한다.   
d에 k와 v를 만든 이유는 키와 값 두 개가 필요하기 때문!!   
items로 d 안의 키-값 쌍을 꺼내서 k와 v에 할당하고, if문으로 값이 30이 아닌 것들만 n이라는 빈 딕셔너리에 setdefault로 추가한다.   
그러면 원하는 결과를 얻을 수 있다.
      
여기서 추가로 **딕셔너리 표현식**을 응용해보자!   
→ {키:값 for 변수 in 리스트 if 조건식}
```python
{k : v for k, v in d.items() if v != 30}
# {'alpha': 10, 'bravo': 20}

# 최종
result = {k : v for k, v in d.items() if k !='delta' and v != 30}
result
# {'alpha': 10, 'bravo': 20}
```
딕셔너리 표현식을 사용해서 ‘delta’가 아닌 키와 30이 아닌 값만 넣는 if 조건식을 넣으면 한 줄로 작성이 가능하다.
   
## 파일 사용하기
파일 객체 = open("파일 이름", "파일 열기 모드")   
파일 객체.wirte("문자열")   
파일 객체.close()
```python
파일 열기 모드
r : 읽기 모드
w : 쓰기 모드
a : 추가 모드 -> 파일의 마지막에 새로운 내용을 추가
```
   
```python
fd = open("hello.txt", "w")
fd.write("hello world!")
fd.close()

# hello world! 가 쓰여진 hello.text가 생성됨
```
추가로 주피터 노트북에서는 느낌표(!) 뒤에 명령 프롬프트에서 사용하는 명령어를 입력하면 명령 프롬프트를 사용할 수 있다.
```python
!dir
```
위를 실행하면, 디렉터리 목록이 시간대별로 쭉 뜬다. hello.txt 가 생성된 것도 확인할 수 있다.
      
파일 객체 = open("파일 이름", "파일 모드")   
변수 = 파일 객체.read("문자열")   
파일 객체.close()
```python
fd = open("hello.txt", "r")
s = fd.read() # 전체 데이터를 가져옴
print(s)
fd.close()
# Hello World!
```
   
with는 구문이 끝나는 순간 자동으로 파일 close가 된다.
```python
with open("파일명", "파일 모드") as fd:
    코드
```
```python
with open('hello.txt', 'r') as fd:
    s = fd.read() # 전체 데이터를 가져옴
print(s)
# Hello World!
```
   
Hello World!!!를 3번 반복하고, 그 반복횟수도 옆에 쓸 수 있다.
```python
with open('hello.txt', 'w') as fd:
    for i in range(3):
        fd.write('Hello World!!! {} \n'.format(i))
```
   
```python
line_list = ["여기는\n", "플레이데이터입니다\n", "오늘도\n", "화이팅\n"]
with open('play.txt', 'w') as fd:
    fd.writelines(line_list)
```
위 코드를 작성해서 play.txt 를 생성한 후
```python
with open('play.txt', 'r') as fd:
    lines = fd.readlines()
lines
# ['여기는\n', '플레이데이터입니다\n', '오늘도\n', '화이팅\n']
```
내용이 잘 들어간 걸 볼 수 있다.
      
fd.**read**() : 파일에 있는 모든 데이터를 읽음   
fd.**readline**() : 한줄로 읽은 문자열을 반환   
fd.**readlines**() : 라인별로 읽은 문자열들을 리스트 형태로 반환   
   
fd.**write**(문자열) : 파일에 문자열을 씀   
fd.**writelines**(리스트) : 리스트에 있는 여러 문자열을 한 라인씩 씀   
```python
with open('play.txt', 'r') as fd:
    line = None
    while line != '':
        line = fd.readline()
        print(line.strip('\n'))

'''
여기는
플레이데이터입니다
오늘도
화이팅
'''
```
   
- pickle
pickle은 텍스트 상태의 데이터가 아닌 파이썬 객체 자체를 바이너리 파일로 저장하는 것이다.   
다만, 파이썬 표준 라이브러리에서는 pickle을 안전하지 않은 모듈로 보고, json 모듈을 추천한다.
```python
import pickle

name = "James" # 파이썬 문자열 객체
age = 17 # 파이썬 정수 객체
scores = {'korean':90, 'english':80} # 파이썬 딕셔너리 객체

with open("student.pkl", "wb") as fd:
    pickle.dump(name, fd)
    pickle.dump(age, fd)
    pickle.dump(scores, fd)

...

with open("student.pkl", "rb") as fd:
    loaded_name = pickle.load(fd)
    loaded_age = pickle.load(fd)
    loaded_scores = pickle.load(fd)

loaded_name
# 'James'

loaded_age
# 17

loaded_scores
# {'korean': 90, 'english': 80}
```
   
## Workshop
### 문제1) 파일에서 10자 이하인 단어 개수 세기
단어가 줄 단위로 저장된 words.txt 파일이 주어집니다. 10자 이하인 단어의 개수가 출력되게 만드세요.
```python
with open('words.txt', 'r') as fd:
    word_list = fd.readlines()
    for word in word_list:
        if len(word.strip('\n')) <= 10:
            count += 1
count
# 8
```
줄 단위로 저장된 파일이기 때문에 readlines를 사용해서 리스트를 생성한다. 
   
### 문제2) 특정 문자가 들어 있는 단어 찾기
문자열이 저장된 words2.txt 파일이 주어집니다(문자열은 한 줄로 저장되어 있습니다).   
words2.txt 파일에서 문자 c가 포함된 단어를 각 줄에 출력하는 프로그램을 만드세요.   
단어를 출력할 때는 등장한 순서대로 출력해야 하며 ,(콤마)와 .(점)은 출력하지 않아야 합니다.
```python
with open('words2.txt', 'r') as fd:
    paragraph = fd.read()
    word_list = paragraph.split()
    for word in word_list:
        if 'c' in word:
            print(word.strip(',.'))
'''
dictator
subjects
change
costume
elegance
accepted
'''
```
   
## 함수
함수는 코드의 용도를 구분하고, 코드를 재사용하고, 실수를 줄일 수 있게 해준다.
```
def 함수 이름():
    코드
```
```python
def hello():
    print("Hello World!")

hello()
# Hello World!
```
   
```
def 함수 이름(매개변수1, 매개변수2):
    코드
```
```python
def add(a, b):
    c = a + b
    print(c)

add(1, 2)
# 3
```
   
```
def 함수 이름(매개변수1, 매개변수2):
    코드
    return 반환값
```
```python
def add(a, b):
    c = a + b
    return c

result = add(1, 2)
result
# 3
```
   
```
def 함수 이름(매개변수1, 매개변수2):
    코드
    return 반환값1, 반환값2
```
```python
def add_sub(a, b):
    return a + b, a - b

x, y = add_sub(10, 20)

x, y
# (30, -10)
```
   
- (참고) **sorted 함수**를 사용한 정렬   
*바로 다음에 풀 Workshop 문제를 위한 참고 설명*
```python
l = [1, 4, 5, 6, -1, -10]
result = sorted(l) # sorted() 함수는 다른 시퀀스 객체에서도 사용할 수 있음
result # 정렬의 결과물이 반환되고, l은 원본 그대로 유지
# [-10, -1, 1, 4, 5, 6]
```
   
(1) 리스트
```python
# 단어의 리스트가 준비
words = ["abc", "defgh", "jklm", "nm"]

list(map(len, words)) # 각 단어의 값이 나옴
# [3, 5, 4, 2]

sorted(words, key = len) # key 매개변수에 적당한 함수를 제공해주면, 그에 맞게 정렬
# ['nm', 'abc', 'jklm', 'defgh']
```
   
(2) 딕셔너리
```python
# 딕셔너리 정렬 (점수 순으로 정렬)
scores = {"James":90, "Selly":80, "Jun":100}

def ret_score(x):
    # print(x)
    return x[1]
sorted(scores.items(), key = ret_score, reverse = True)
# [('Jun', 100), ('James', 90), ('Selly', 80)]
```
이렇게 함수를 만들어서 정렬하는 방법과
```python
sorted(scores.items(), key = lambda x:x[1], reverse = True)
# [('Jun', 100), ('James', 90), ('Selly', 80)]
```
lambda 를 사용하는 방법도 있다.
   
## Workshop
### 문제) I have a dream 연설문 단어 빈도수 계산
WordCount 함수에서 ihaveadream.txt 파일을 열어 전체 내용 중 단어를 키로, 빈도를 값으로 매핑한 사전형 자료를 반환하세요.   
단 stopwords.txt에 있는 단어는 제외시킵니다.   
WordCount 함수의 결과를 result.txt로 저장하세요.   
majorityCnt 함수에서 사전형 자료를 인수로 받아 값을 기준으로 내림차순으로 정렬하여 값이 가장 큰 키를 반환하세요.   
   
(1) 우선 각 파일을 열어서 읽은 내용을 speech와 stopwords에 담는다.
```python
with open('ihaveadream.txt', 'r') as fd1:
    speech = fd1.read()
with open('stopwords.txt', 'r') as fd2:
    stopwords = fd2.read()
```
   
(2) 텍스트 파일 안에는 대문자와 소문자가 섞여있기 때문에 lower를 사용하고, split으로 단어를 쪼개서 리스트에 넣는다.
```python
word_list = speech.lower().split()
stop_list = stopwords.lower().split()
```
   
(3) 이제 stopwords.txt에 있는 단어는 제외시키고, 단어와 빈도를 값으로 매핑한 딕셔너리를 반환할 차례다.   
선생님께서는 2가지 옵션을 알려주셨다.
```python
# option1
d = {}
for word in word_list: # word : i -> am -> happy -> ...
    if word in stop_list:
        continue
    if word not in d:
        d[word] = 1 # 이 단어가 처음 등장시 최초로 카운트
    else:
        d[word] += 1 # 이 단어가 등록된 경우에는 카운트 누적
```
→ 단어 등장시 카운트 하는 방식   
```python
# option2
d = {}
for word in word_list:
    if word in stop_list:
        continue
    d[word] = d.get(word, 0) + 1 # 이미 단어가 사전에 있는 경우, 없는 경우 모두 값을 가져온다.
```
→ **get**을 사용하는 방식   
get은 오늘 딕셔너리 응용 파트에서 배웠듯, **키가 없을 때 기본 값을 반환**하는 딕셔너리 관련 함수이다.   
option 1처럼 카운트하는 방식도 있지만,   
option 2처럼 get을 사용하면 이미 단어가 있는 경우, 없는 경우 모두 값을 반환하기 때문에 더 간단하게 쓸 수 있다.   
   
(4) 그 다음은 문제에서 요구한 WordCount() 함수를 만들고 텍스트 파일로 저장할 차례이다.
```python
def WordCount():
    d = {}
    for word in word_list:
        if word in stop_list:
            continue
        d[word] = d.get(word, 0) + 1 # 이미 단어가 사전에 있는 경우, 없는 경우 모두 값을 가져온다.
    return d
```
→ option 2에서 작성한 코드를 WordCount() 함수에 입력
```python
d = WordCount()
with open('result.txt', 'w') as fd3:
    fd3.write(str(d))
```
→ result.txt 파일을 생성하고, 결과값을 저장했다. 이때, 그냥 딕셔너리를 쓸 수 없어서 str으로 한번 감싸준다.   
   
(5) 문제의 최종 단계! 이제 위에서 정렬에 대해 짚고 넘어간 이유를 알 수 있다. 
```python
def majorityCnt(d):
    # result = sorted(d.items(), key = ret_score, reverse = True)
    result = sorted(d.items(), key = lambda x:x[1], reverse = True)
    return result[0]
```
→ sorted의 reverse 기본값은 False이기 때문에, **True로 입력하면 오름차순이 아닌 내림차순으로 정렬**이 가능하다.
```python
most_freq_word = majorityCnt(d)
print(most_freq_word)

# ('freedom', 19)
```
문제가 원하는 답은 ('freedom', 19) 였다.
      
추가로, (5) 에서 사용된 **lambda** 에 대해 모르는 것이 많아 자세한 설명을 찾아보았다!   
   
→ lambda는 함수를 생성할 때 사용하는 예약어로 **def와 동일한 역할**을 한다. 보통 함수를 한줄로 간결하게 만들 때 사용한다.   
**def를 사용해야 할 정도로 복잡하지 않거나, def를 사용할 수 없는 곳에 주로 쓰인다.**
```python
lambda 매개변수1, 매개변수2, ... : 매개변수를 사용한 표현식
```
lambda 예약어로 만든 함수는 return 명령어가 없어도 결괏값을 돌려준다고 한다.
      
(5) 에서 주석처리가 되어 있는 **result = sorted(d.items(), key = ret_score, reverse = True)** 에서   
ret_score가 뭐였지~ 하고 생각해보니 sorted를 사용한 정렬 파트에서 만든 함수였다.   
   
ret_score 가 하는 역할을 해석해보면, **x의 1번째 값을 기준으로 sorted** 해주는 것이다.   
즉, 아래 코드에서는 점수를 기준으로 정렬하게 해주는 것이다.
```python
def ret_score(x):
    # print(x)
    return x[1]
sorted(scores.items(), key = ret_score, reverse = True)
# [('Jun', 100), ('James', 90), ('Selly', 80)]
```
   
정확히 이해가 됐다! 다시 (5) 의 lambda를 사용한 코드를 되짚어보자.
```python
def majorityCnt(d):
    # result = sorted(d.items(), key = ret_score, reverse = True)
    result = sorted(d.items(), key = lambda x:x[1], reverse = True)
    return result[0]
```
둘 다 해내는 역할에 차이점은 없다. 다만, ret_score를 쓰기 위해서는 def로 함수를 만들어야 하는 점이고,   
lambda를 사용하면 굳이 def로 함수를 만들 필요 없이 한 줄로 해결이 가능하다는 것이다!   
key에는 함수가 들어가고, 그에 맞게 정렬을 해준다.
