> 부트캠프 2주차 2022년 10월 25일
   
## 선형 리스트
**선형 리스트** ***Linear List* :** 데이터를 일정한 순서로 나열한 구조(데이터의 논리적인 순서와 기억 장소에 저장되는 물리적 순서가 일치)이다. 

*→ 데이터를 논리적인 순서대로 메모리에 연속하여 저장하고 구현하는 방식이다. **배열**을 이용해서 구현한다!*
![image](https://user-images.githubusercontent.com/106129152/200704983-ad0cc585-c41b-49f3-a1a0-933603bd36d1.png)   
| **장점**

Index로 접근할 수 있기 때문에 접근 속도가 매우 빠르다. 

연속된 메모리 공간에 존재하기 때문에 관리가 편하다.

| **단점**

메모리 사용의 비효율성 문제를 가지고 있다.

배열의 크기 > 데이터 수: 메모리 공간의 낭비를 가져온다.

배열의 크기 < 데이터 수: 데이터를 저장할 수 없다.

삽입 & 삭제 연산 후에 연속적인 물리 주소를 유지하기 위해 원소들을 이동시키는 추가 작업과 시간이 소요된다.   
- **선형 리스트의 원리**
    - 선형 리스트 생성
    - 데이터 삽입
    - 데이터 삭제
    
- **삽입 연산**
    
    새로운 원소를 삽입하려면 그 자리를 만들기 위해 삽입할 위치 이후의 원소들을 모두 한 칸씩 뒤로 옮겨야 한다.
    
    ① 원소를 삽입할 빈 자리를 만든다.
    
    ② 삽입할 자리 이후의 원소들은 한 칸씩 뒤로 이동한다.
    
    ③ 빈 자리에 원소를 삽입한다.   
![image](https://user-images.githubusercontent.com/106129152/200705158-503ae0ce-3ff6-4fe4-b589-6951aa1c08b4.png)   
   
삽입할 자리를 만들기 위한 자리 이동 횟수를 구하는 방법은 다음과 같다.
```
N 개의 원소로 이루어진 선형 리스트에서 인덱스 K에 원소를 삽입하는 경우

마지막 원소의 인덱스 - 삽입할 자리의 인덱스 + 1 -> (N - 1) - K + 1
```
   
   
- **삭제 연산**
    
    원소를 삭제하려면, 삭제한 이후 빈 자리를 채우기 위해 삭제한 위치 이후 원소들의 자리를 한 칸씩 앞으로 옮겨야 한다.
    
    ① 원소를 삭제한다.
    
    ② 삭제한 자리 이후의 원소들은 한 칸씩 앞으로 이동해서 빈 자리를 채운다.   
![image](https://user-images.githubusercontent.com/106129152/200705339-d03ecd57-29ba-487c-9b95-513012bc6b47.png)
   
삭제 후 빈 자리를 채우기 위한 자리 이동 횟수는 다음과 같다.
```
N개의 원소로 이루어진 선형 리스트에서 인덱스 K의 원소를 삭제하는 경우

마지막 원소의 인덱스 - 삭제한 자리의 인덱스 -> (N - 1) - K
```
   
→ [**선형 리스트(1)**](https://toward-the-future.tistory.com/entry/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%84%A0%ED%98%95-%EB%A6%AC%EC%8A%A4%ED%8A%B8-Linear-List), [**선형 리스트 파이썬 구현(2)**](https://velog.io/@cha-suyeon/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%84%A0%ED%98%95-%EB%A6%AC%EC%8A%A4%ED%8A%B8Linear-List) 
      
## Workshop
### 문제) 숫자의 합 구하기
시간 제한 1초 | 난이도 브론즈 Ⅳ | 백준 온라인 저지 11720번

N개의 숫자가 공백 없이 써 있다. 이 숫자를 모두 합해 출력하는 프로그램을 작성하시오.

**입력**

1번째 줄에 숫자의 개수 N(1<=N<=100), 2번째 줄에 숫자 N개가 공백 없이 주어진다.

**출력**

입력으로 주어진 숫자 N개가 합을 출력한다.
```python
n = int(input())
numbers = list(input()) # numbers = ['1', '0', '9', '8', ...]
s = 0 # sum, 합을 담을 변수

for i in numbers:
    s = s + int(i) # i : 1 -> 0 -> 9 -> 8 -> ...
print(s)
```   
   
## 단순 연결 리스트
***단순*** ***연결 리스트 Singly* *Linked List* :** 동적 메모리 할당을 이용해 노드들을 한 방향으로 연결하여 리스트를 구현(단방향 순환구조)한 자료구조이다.

단순 연결 리스트는 데이터를 **노드** 단위로 삽입하고 삭제한다.

삽입이나 삭제시 항목들의 이동이 필요 없으나,

항목을 탐색하려면 원하는 노드를 찾을 때까지 차례로 방문하는 순차탐색을 이용해야 한다.   
![image](https://user-images.githubusercontent.com/106129152/200710998-10211dda-25be-469c-92e7-9d47e7cd1d08.png)
   
   
**배열**의 순서는 실제와 같은 **물리적**인 반면, **리스트**의 순서는 **논리적**이라 볼 수 있다.

**노드(Node)** : 데이터와 링크가 함께 구성된 항목

**헤드(Head)** : 첫번째 노드

**링크(Link)** : 다음 데이터를 가리키는 포인터 변수
```python
class Node:
	def __init__(self, item):
    	self.data = item   # data
        self.next = None   # next link (다음 인자를 가리킴)
```
![image](https://user-images.githubusercontent.com/106129152/200710759-d84187ab-e967-48a3-a4d0-6df6ff041121.png)
      
- **삽입**
    
    ① 공백 노드를 생성한다. 링크가 가리키게 하고, 새 노드에 값을 저장한다.
    
    ![image](https://user-images.githubusercontent.com/106129152/200711156-13a69493-0aff-4594-ae7f-5f7cc8a33c51.png)
    
    ② 새 노드의 링크값을 저장한다. ← 새 노드의 링크 필드에 다음 노드의 주소 값을 저장한다.
    
    ![image](https://user-images.githubusercontent.com/106129152/200711190-616c5955-03fe-4438-b0da-ca0bed585805.png)
    
    ③ 앞 노드와 새 노드를 연결한다. ← 앞 노드의 링크 필드에 새 노드의 주소 값을 저장한다.
    
    ![image](https://user-images.githubusercontent.com/106129152/200711222-22734ab5-077d-4fad-af49-1aca8d683a3d.png)
    

- **삭제**
    
    ① 삭제할 노드의 앞 노드를 찾는다.
    
    ![image](https://user-images.githubusercontent.com/106129152/200711274-fa6db1e7-ffae-4970-9e06-c7b4e33da153.png)
    
    ② 삭제할 노드의 앞 노드와 삭제한 노드의 다음 노드를 연결한다. ← 앞 노드에 삭제할 노드의 링크 필드값을 저장한다.
    
    ![image](https://user-images.githubusercontent.com/106129152/200711349-fe6dd86c-dd24-469e-835f-3120430f36b5.png)
   
## Workshop
### 연결 리스트 응용
```python
class Node() :
    def __init__ (self) :
        self.data = None
        self.link = None
        
def printNodes(start) :
    current = start
    if current == None :
        return
    print(current.data, end = ' ')
    while current.link != None:
        current = current.link
        print(current.data, end = ' ')
    print()
    
def makeSimpleLinkedList(namePhone) :
    global memory, head, current, pre
    printNodes(head)
    node = Node()
    node.data = namePhone
    memory.append(node)
    if head == None : # 첫 번째 노드일 때
        head = node
        return    
    if head.data[0] > namePhone[0] : # 첫 번째 노드보다 작을 때
        node.link = head
        head = node
        return
    
    # 중간 노드로 삽입하는 경우
    current = head
    while current.link != None :
        pre = current
        current = current.link
        if current.data[0] > namePhone[0]:
            pre.link = node
            node.link = current
            return
        
# 삽입하는 노드가 가장 큰 경우
    current.link = node
    
## 전역 변수 선언 부분 ##
memory = []
head, current, pre = None, None, None
dataArray = [["지민", "010-1111-1111"], ["정국", "010-2222-2222"], ["뷔", "010-3333-3333"], ["슈가", "010-4444-4444"], ["진", "010-5555-5555"]]

## 메인 코드 부분 ##
if __name__ == "__main__" :
    for data in dataArray : # 5 iterations : 지민 -> 정국 -> 뷔 -> 슈가 -> 진
        makeSimpleLinkedList(data)
    printNodes(head)
```
→ 실행하면 아래와 같이 출력된다.   
![image](https://user-images.githubusercontent.com/106129152/200711469-4c9d0cdc-956c-4c73-82bc-12950e9203f8.png)   
   
→ [**단순 연결 리스트 파이썬 구현(1)**](https://velog.io/@cha-suyeon/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EB%8B%A8%EC%88%9C-%EC%97%B0%EA%B2%B0-%EB%A6%AC%EC%8A%A4%ED%8A%B8Singly-Linked-List), [**연결 리스트(2)**](https://toward-the-future.tistory.com/entry/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%97%B0%EA%B2%B0-%EB%A6%AC%EC%8A%A4%ED%8A%B8-Linked-List?category=1031164), [**연결 리스트(3)**](https://daeun-computer-uneasy.tistory.com/20)   
   
## 스택과 큐
스택과 큐는 모두 선형 자료 구조이다. 

**삽입(push) :** 자료 구조에 데이터를 삽입하는 역할

**삭제(pop)** : 자료 구조에서 데이터를 삭제하는 역할

- **스택 *Stack* :** 먼저 삽입한 데이터는 밑에 쌓이고, 나중에 삽입한 데이터는 위에 쌓이는 구조다.
    
    LIFO(**후입선출**, Last In First Out) 방식이다. (=나중에 들어온 값이 먼저 나가는 구조) 
    
    삽입과 삭제가 일어나는 위치를 **top**이라고 한다.
    
    → 삽입과 삭제가 한 방향에서만 이루어진다. 프링글스 과자통을 생각하면 이해하기 쉽다!   
    ![image](https://user-images.githubusercontent.com/106129152/200713043-bf5b00c8-3398-478a-afed-a92948dc366a.png)
   
    파이썬은 list 자료형의 append와 pop 메소드만으로 스택 구현이 가능하다.

    **append()** : 리스트 가장 뒤쪽(맨 끝)에 데이터를 삽입

    **pop()** : 리스트 가장 뒤쪽(맨 끝)의 데이터를 삭제   
    
## Workshop
- 스택 일반
```python
# %load "(실습 4) 스택 일반.py"
## 함수 선언 부분 ##
def isStackFull() :
    global SIZE, stack, top
    if (top >= SIZE-1) :
        return True
    else :
        return False
def isStackEmpty() :
    global SIZE, stack, top
    if (top == -1) :
        return True
    else :
        return False
def push(data) :
    global SIZE, stack, top
    if (isStackFull()) :
        print("스택이 꽉 찼습니다.")
        return
    top += 1
    stack[top]= data
def pop() :
    global SIZE, stack, top
    if (isStackEmpty()) :
        print("스택이 비었습니다.")
        return None
    data = stack[top]
    stack[top] = None
    top -= 1
    return data
def peek() :
    global SIZE, stack, top
    if (isStackEmpty()) :
        print("스택이 비었습니다.")
        return None
    return stack[top]
## 전역 변수 선언 부분 ##
SIZE = int(input("스택의 크기를 입력하세요 ==> "))
stack = [ None for _ in range(SIZE) ]
top = -1
## 메인 코드 부분 ##
if __name__ == "__main__" :
    select = input("삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> ")
    while (select != 'X' and select != 'x') :
        if select=='I' or select =='i' :
            data = input("입력할 데이터 ==> ")
            push(data)
            print("스택 상태 : ", stack)
        elif select=='E' or select =='e' :
            data = pop()
            print("추출된 데이터 ==> ", data)
            print("스택 상태 : ", stack)
        elif select=='V' or select =='v' :
            data = peek()
            print("확인된 데이터 ==> ", data)
            print("스택 상태 : ", stack)
        else :
            print("입력이 잘못됨")
        select = input("삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> ")
    print("프로그램 종료!")
```
   
- 스택 응용
### 웹 서핑에서 이전 페이지 돌아가기 
```python
import webbrowser
import time
## 함수 선언 부분 ##
def isStackFull() :
    global SIZE, stack, top
    if (top >= SIZE-1) :
        return True
    else :
        return False
def isStackEmpty() :
    global SIZE, stack, top
    if (top == -1) :
        return True
    else :
        return False
def push(data) :
    global SIZE, stack, top
    if (isStackFull()) :
        print("스택이 꽉 찼습니다.")
        return
    top += 1
    stack[top] = data
def pop() :
    global SIZE, stack, top
    if (isStackEmpty()) :
        print("스택이 비었습니다.")
        return None
    data = stack[top]
    stack[top] = None
    top -= 1
    return data
def peek() :
    global SIZE, stack, top
    if (isStackEmpty()) :
        print("스택이 비었습니다.")
        return None
    return stack[top]
## 전역 변수 선언 부분 ##
SIZE = 100
stack = [ None for _ in range(SIZE) ]
top = -1
## 메인 코드 부분 ##
if __name__ == "__main__" :
    urls = [ 'naver.com', 'daum.net', 'nate.com']
    for url in urls : # url : naver.com -> daum.net -> nate.com
        # 1. stack에 push
        push(url)
        # 2. url open(with brwoser)
        webbrowser.open('http://' + url)
        print(url, end = '-->')
        time.sleep(1)        
    print("방문 종료")
    time.sleep(5)
    while True :
        # 1. stack에서 pop 
        url = pop()
        if url == None:
            break
        # 2. url open(with browser)
        webbrowser.open('http://' + url)
        print(url, end = '-->')
        time.sleep(1)
    print("방문 종료")
```
```
naver.com-->daum.net-->nate.com-->방문 종료
nate.com-->daum.net-->naver.com-->스택이 비었습니다.
방문 종료
```
   
### 헨젤과 그레텔
헨젤과 그레텔이 돌을 떨어뜨리면서 숲으로 들어간다.   
과자집에서 집으로 돌아갈 때는 떨어뜨린 순서와 반대로 돌을 주워야 한다.   
스택을 이용해서 집으로 무사히 돌아가도록 하자.
```python
import random
## 함수 선언 부분 ##
def isStackFull() :
    global SIZE, stack, top
    if (top >= SIZE-1) :
        return True
    else :
        return False
def isStackEmpty() :
    global SIZE, stack, top
    if (top == -1) :
        return True
    else :
        return False
def push(data) :
    global SIZE, stack, top
    if (isStackFull()) :
        return
    top += 1
    stack[top] = data
def pop() :
    global SIZE, stack, top
    if (isStackEmpty()) :
        return None
    data = stack[top]
    stack[top] = None
    top -= 1
    return data
def peek() :
    global SIZE, stack, top
    if (isStackEmpty()) :
        return None
    return stack[top]
## 전역 변수 선언 부분 ##
SIZE = 10
stack = [ None for _ in range(SIZE) ]
top = -1
## 메인 코드 부분 ##
if __name__ == "__main__" :
    stoneAry = ["빨강", "파랑", "초록", "노랑", "보라", "주황"]
    random.shuffle(stoneAry)
    print("과자집에 가는길 : ", end = ' ')
    for stone in stoneAry :
        push(stone)        
        print(stone, "-->", end = ' ')
    print("과자집")
    print("우리집에 오는길 : ", end = ' ')
    while True :
        stone = pop()
        if stone == None:
            break
        print(stone, "-->", end = ' ')
    print("우리집")
```
```
과자집에 가는길 :  파랑 --> 보라 --> 주황 --> 빨강 --> 노랑 --> 초록 --> 과자집
우리집에 오는길 :  초록 --> 노랑 --> 빨강 --> 주황 --> 보라 --> 파랑 --> 우리집
```
      
- **큐 *Queue* :** 한 쪽 끝(rear)에서 데이터가 삽입이 되고, 다른 한쪽 끝(front)에서는 데이터가 삭제되는 구조다.
    
    FIFO(**선입선출,** First In First Out) 방식이다. (=먼저 들어온 값이 먼저 나가는 구조)
    
    입력된 순서대로 작업을 수행해야 할 때 활용할 수 있다.
    
    → 출구는 **머리(front)**로 정해 삭제 연산만 수행하고, 입구는 **꼬리(rear)**로 정해 삽입 연산만 수행한다.
    
    ![image](https://user-images.githubusercontent.com/106129152/200717732-501cf96f-100d-4170-99f2-09dc3957edef.png)
    
    파이썬은 collections 모듈의 deque 자료 구조를 사용하면 빠르게 큐를 구현할 수 있다.
    
    **peek :** 추출될 데이터를 큐에 그대로 두고 확인만 하는 것
    
    **enQueue :** 데이터를 삽입하는 작업
    
    **deQueue :** 데이터를 삭제하는 작업
    
    ![image](https://user-images.githubusercontent.com/106129152/200717773-fe254b9a-4db4-480a-a4d2-6af21fed2cd7.png)
      
## Workshop
- 큐 일반
```python
## 함수 선언 부분 ##
def isQueueFull() :
    global SIZE, queue, front, rear
    if (rear == SIZE-1) :
        return True
    else :
        return False
def isQueueEmpty() :
    global SIZE, queue, front, rear
    if (front == rear) :
        return True
    else :
        return False
def enQueue(data) :
    global SIZE, queue, front, rear
    if (isQueueFull()) :
        print("큐가 꽉 찼습니다.")
        return
    rear += 1
    queue[rear] = data
    
def deQueue() :
    global SIZE, queue, front, rear
    if (isQueueEmpty()) :
        print("큐가 비었습니다.")
        return None
    front += 1
    data = queue[front]
    queue[front] = None
    return data

def peek() :
    global SIZE, queue, front, rear
    if (isQueueEmpty()) :
        print("큐가 비었습니다.")
        return None
    return queue[front+1]
## 전역 변수 선언 부분 ##
SIZE = int(input("큐의 크기를 입력하세요 ==> "))
queue = [ None for _ in range(SIZE) ]
front = rear = -1
## 메인 코드 부분 ##
if __name__ == "__main__" :
    select = input("삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> ")
    while (select != 'X' and select != 'x') :
        if select=='I' or select =='i' :
            data = input("입력할 데이터 ==> ")
            enQueue(data)
            print("큐 상태 : ", queue)
        elif select=='E' or select =='e' :
            data = deQueue()
            print("추출된 데이터 ==> ", data)
            print("큐 상태 : ", queue)
        elif select=='V' or select =='v' :
            data = peek()
            print("확인된 데이터 ==> ", data)
            print("큐 상태 : ", queue)
        else :
            print("입력이 잘못됨")
        select = input("삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> ")
    print("프로그램 종료!")
```
```python
def isQueueFull() :
    global SIZE, queue, front, rear
    if (rear != SIZE-1) : # rear 뒤에 여유가 있는 상태
        return False
    elif (rear == SIZE -1) and (front == -1) : # 큐가 꽉 찬 상태
        return True
    else :
        for i in range(front+1, SIZE) :
            queue[i-1] = queue[i]
            queue[i] = None
            
        front -= 1
        rear -= 1
        return False
        
SIZE = 5
queue = [None, None, "문별", "휘인", "선미"]
front = 1
rear = 4

print("큐가 꽉 찼는지 여부 ==>", isQueueFull())
print("큐 상태 ==> ", queue)
```
```python
큐가 꽉 찼는지 여부 ==> False
큐 상태 ==>  [None, '문별', '휘인', '선미', None]
```
   
- 큐 응용
### 유명 맛집의 대기줄
유명 맛집의 대기줄에는 손님들이 들어온 순서대로 줄을 선다.   
그리고 대기줄이 꽉 차면 더 이상 손님을 받지 않는다.   
이제 대기줄 손님들은 자리가 생기면 1명씩 식당으로 들어간다.   
맨 앞쪽 손님이 대기줄에서 식당으로 들어갈 때마다 대기줄 뒤쪽 손님들은 한 칸씩 이동해서 줄을 다시 서도록 한다.
```python
## 함수 선언 부분 ##
def isQueueFull() :
    global SIZE, queue, front, rear
    if (rear == SIZE-1) :
        return True
    else :
        return False

def isQueueEmpty() :
    global SIZE, queue, front, rear
    if (front == rear) :
        return True
    else :
        return False

def enQueue(data) :
    global SIZE, queue, front, rear
    if (isQueueFull()) :
        print("큐가 꽉 찼습니다.")
        return
    rear += 1
    queue[rear] = data

def deQueue() :
    global SIZE, queue, front, rear
    if (isQueueEmpty()) :
        print("큐가 비었습니다.")
        return None
    front += 1
    data = queue[front]
    queue[front] = None

    # 모든 사람을 한칸씩 앞으로 당기기
    for i in range(front+1, rear+1) :
            queue[i-1] = queue[i]
            queue[i] = None
    front -= 1
    rear -= 1

    return data

def peek() :
    global SIZE, queue, front, rear
    if (isQueueEmpty()) :
        print("큐가 비었습니다.")
        return None
    return queue[front+1]

## 전역 변수 선언 부분 ##
SIZE = 5
queue = [ None for _ in range(SIZE) ]
front = rear = -1

## 메인 코드 부분 ##
if __name__ == "__main__" :
    enQueue('정국')
    enQueue('뷔')
    enQueue('지민')
    enQueue('진')
    enQueue('슈가')
    print("대기 줄 상태 : ", queue)

    for _ in range(rear+1) :
        print(deQueue(), '님 식당에 들어감')
        print("대기 줄 상태 : ", queue)

    print("식당 영업 종료!")
```   
   
→ [**스택(1)**](https://toward-the-future.tistory.com/entry/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%8A%A4%ED%83%9DStack?category=1031164), [**스택과 큐의 개념(2)**](https://brightwon.tistory.com/8), [**스택과 큐 파이썬 구현(3)**](https://velog.io/@combi_jihoon/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%8A%A4%ED%83%9D-%ED%81%90python-%EA%B5%AC%ED%98%84), [**스택과 큐 파이썬 구현(4)**](https://growingarchive.tistory.com/248), [**큐(5)**](https://toward-the-future.tistory.com/entry/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%ED%81%90Queue-%EC%84%A0%ED%98%95-%ED%81%90Linear-Queue-%EC%9B%90%ED%98%95-%ED%81%90Circular-Queue-%EC%97%B0%EA%B2%B0-%ED%81%90Linked-List-Queue-%EB%8D%B0%ED%81%ACDouble-Ended-Queue?category=1031164)   
   
## 참고 - 로그(*log*)
로그(log)는 지수함수의 역함수이다. 어떤 수를 나타내기 위해 고정된 밑을 몇 번 곱하여야 하는지를 나타낸다고 볼 수 있다.   

$$
{\displaystyle x}는 {\displaystyle a}를 밑으로 하는 {\displaystyle y}의 로그”라 하고 {\displaystyle \log _{a}y=x}로 표기한다.
$$

$$
 {\displaystyle 3^{4}=81}이므로 {\displaystyle \log _{3}81=4}
$$
