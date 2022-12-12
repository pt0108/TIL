> 부트캠프 2주차 2022년 10월 26일
   
## 트리 구조와 이진 트리, 이진 탐색 트리
- **트리(Tree) 구조**
    
    Node와 Branch를 이용해서, 사이클을 이루지 않도록 구성한 데이터 구조로, 나무를 거꾸로 뒤집어 놓은 형태이다. 
    
    *ex) 컴퓨터의 상위 폴더 안에 하위 폴더들이 계속 이어져 있는 구조와 구성*
    
    **Node :** 트리에서 데이터를 저장하는 기본 요소
    
    **Root node :** 트리 맨 위에 있는 노드
    
    **Level :** 최상위 노드를 Level 0으로 하였을 때, 하위 Branch로 연결된 노드의 깊이를 나타냄
    
    **Leaf Node :** Child Node가 하나도 없는 노드
    
    **Sibling(Brother Node) :** 동일한 Parend Node를 가진 노드
    
    **Depth :** 트리에서 Node가 가질 수 있는 최대 Level   
    
- **이진 트리(Binary Tree)**
    
    ![image](https://user-images.githubusercontent.com/106129152/200737110-85062d5f-ce49-463c-a44a-1c4b5ea7b028.png)

    이진 트리는 모든 노드의 자식이 최대 2개인 트리(자식이 2개 이하로 구성)를 말한다.
    
    
    ![image](https://user-images.githubusercontent.com/106129152/200737060-fdf2c71b-71fa-4339-8ccd-34cae6a19a74.png)

    이진 트리의 노드를 한 번씩 방문하는 것을 ***순회(Traversal)*** 라고 한다.   
    노드 데이터를 처리하는 순서에 따라 전위 순회, 중위 순회, 후위 순회로 나뉜다.   
    
    **|** **전위** 순회 (**preorder** traversal)

    **① 현재 노드 데이터 처리**

    ② 왼쪽 서브 트리로 이동

    ③ 오른쪽 서브 트리로 이동

    **|** **중위** 순회 (**inorder** traversal)

    ① 왼쪽 서브 트리로 이동

    **② 현재 노드 데이터 처리**

    ③ 오른쪽 서브 트리로 이동

    **| 후위** 순회 (**postorder** traversal)

    ① 왼쪽 서브 트리로 이동

    ② 오른쪽 서브 트리로 이동

    **③ 현재 노드 데이터 처리**   
```python
class TreeNode() :
    def __init__ (self) :
        self.left = None
        self.data = None
        self.right = None
        
node1 = TreeNode()
node1.data = '화사'
node2 = TreeNode()
node2.data = '솔라'
node1.left = node2
node3 = TreeNode()
node3.data = '문별'
node1.right = node3
node4 = TreeNode()
node4.data = '휘인'
node2.left = node4
node5 = TreeNode()
node5.data = '쯔위'
node2.right = node5
node6 = TreeNode()
node6.data = '선미'
node3.left = node6

def preorder(node) :
    if node == None:
        return
    print(node.data, end='->')
    preorder(node.left)
    preorder(node.right)
        
def inorder(node):
    if node == None :
        return
    inorder(node.left)
    print(node.data, end='->')
    inorder(node.right)
        
def postorder(node):
    if node == None :
        return
    postorder(node.left)
    postorder(node.right)
    print(node.data, end='->')
        
print('전위 순회 : ', end = '')
preorder(node1)
print('끝')
print('중위 순회 : ', end = '')
inorder(node1)
print('끝')
print('후위 순회 : ', end = '')
postorder(node1)
print('끝')
```
```
전위 순회 : 화사->솔라->휘인->쯔위->문별->선미->끝
중위 순회 : 휘인->솔라->쯔위->화사->선미->문별->끝
후위 순회 : 휘인->쯔위->솔라->선미->문별->화사->끝
```
   
- 포화 이진 트리(full binary tree)
    
    ![image](https://user-images.githubusercontent.com/106129152/200737396-b5fccc0f-4abd-46d4-9034-3b3dda6725e1.png)
    

- 완전 이진 트리(complete binary tree)
    
    ![image](https://user-images.githubusercontent.com/106129152/200737428-dc95ff3c-b27e-42f9-9506-43aef476a105.png)
    

- 편향 이진 트리(skewed binary tree)
    
    ![image](https://user-images.githubusercontent.com/106129152/200737451-9ce23bf0-c49b-4fc5-bd0e-91ff0b39d785.png)
    

- **이진 탐색 트리(Binary Search Tree, *BST*)**
    
    이진 탐색 트리는 이진 트리에 다음과 같은 추가적인 조건이 있는 트리다. 
    
    - 모든 노드는 왼쪽 가지에 포함되는 어떤 숫자보다도 큰값을 가진다.
    
    - 모든 노드는 오른쪽 가지에 포함되는 어떤 숫자보다도 작은값을 가진다.
    
    - 모든 노드 값은 중복되지 않는다. 즉, 중복된 값은 이진 탐색 트리에 저장할 수 없다.
    
    
    - **탐색** 과정
        
        ① 찾는 값이 현재 노드 값과 같다면 탐색을 종료한다.
        
        ② 찾는 값이 현재 노드 값보다 작다면 왼쪽으로 간다.
        
        ③ 찾는 값 현재 노드 값보다 크다면 오른쪽으로 간다.   
 ```
if 현재 작업 노드의 데이터 == 찾을 데이터 :
  탐색 종료
elif 현재 작업 노드의 데이터 < 찾을 데이터 :
  왼쪽 서브 트리 탐색
else :
  오른쪽 서브 트리 탐색
```
```python
findName = '마마무'
current = root
while True :
    if findName == current.data :
        print(findName, '을(를) 찾음.')
        break
    elif findName > current.data :
        if current.left == None :
            print(findName, '이(가) 트리에 없음')
            break
        current = current.left
    else :
        if current.right == None :
            print(findName, '이(가) 트리에 없음')
            break
        current = current.right

# 마마무 이(가) 트리에 없음
```   

- **삽입** 과정
    
    ① 삽입할 값이 현재 노드 값보다 작다면 왼쪽으로 간다.
    
    ② 삽입할 값이 현재 노드 값보다 크다면 오른쪽으로 간다.
    
    ③ 자식노드가 없을 때까지 ①~②과정을 반복하고 자식노드가 없을 때 만들어서 연결시켜준다.
    
- 이진 탐색 트리 구성
```python
## 함수 선언 부분 ##
class TreeNode() :
    def __init__ (self) :
        self.left = None
        self.data = None
        self.right = None
        
## 전역 변수 선언 부분 ##
memory = []
root = None
nameAry = ['블랙핑크', '레드벨벳', '마마무', '에이핑크',  '걸스데이', '트와이스' ]

## 메인 코드 부분 ##
node = TreeNode()
node.data = nameAry[0]
root = node
memory.append(node)

for name in nameAry[1:] :
    node = TreeNode()
    node.data = name
    current = root
    while True :
        if name < current.data : # 값이 루트보다 작을 때 왼쪽으로 이동
            if current.left == None: 
                current.left = node
                break
            current = current.left
        else : # 값이 루트보다 클 때 오른쪽으로 이동
            if current.right == None:
                current.right = node
                break
            current = current.right
    memory.append(node)
    
print("이진 탐색 트리 구성 완료!")
```   

- **삭제** 과정
    
    삭제할 노드에 브랜치가 없을 때 : Leat Node 삭제
    
    삭제할 노드에 브랜치가 한 개 있을 때 : Childe Node가 하나인 노드 삭제
    
    삭제할 노드에 브랜치가 두 개 있을 때 : Childe Node가 둘인 노드 삭제   
```python
deleteName = '마마무'
current = root
parent = None
while True:
    if deleteName == current.data :
        if current.left == None and current.right == None :
            if parent.left == current :
                parent.left = None
            else :
                parent.right = None
            del(current)
        elif current.left != None and current.right == None :
            if parent.left == current :
                parent.left = current.left
            else :
                parent.right = current.left
            del(current)
        elif current.left == None and current.right != None :
            if parent.left == current:
                parent.left = current.right
            else:
                parent.right = current.right
            del(current)
        print(deleteName, '이(가) 삭제됨.')
        break
    elif deleteName < current.data :
        if current.left == None :
            print(deleteName, '이(가) 트리에 없음')
            break
        parent = current
        current = current.left
    else:
        if current.right == None :
            print(deleteName, '이(가) 트리에 없음')
            break
        parent = current
        current = current.right

# 마마무 이(가) 삭제됨.
```
   
   
→ [**이진 트리 순회**](https://www.jiwon.me/binary-tree-traversal/), [**이진 탐색 트리 with Python**](https://doing7.tistory.com/92), [**자료구조 & 알고리즘 : 트리**](https://lucaseo.github.io/posts/2021-03-01-python-datastructure-tree-bst/)
      
## 선택 정렬
일단, **정렬**은 순서대로 데이터가 나열되어 있는 것을 말한다.

***선택 정렬(Selection Sort)이란?***

→ 여러 데이터 중에서 가장 작은 값을 뽑는 작동을 반복하여 값을 정렬

*(최소값을 찾고 오름차순으로 정렬하는 것을 **최소 선택 정렬**, 최대값을 찾고 내림차순으로 정렬하는 것을 **최대 선택 정렬**이라고 한다.)*

① 주어진 데이터 중 최소값을 찾는다.

② 해당 최소값을 데이터 맨 앞에 위치한 값과 교체한다.

③ 맨 앞의 위치를 뺸 나머지 데이터를 동일한 방법으로 반복한다.
      
→ 크기 n의 배열이 주어졌을 때, index 0부터 n-1까지의 모든 index i에 대해서,   
i번째 부터 n-1 번째까지 값 중 가장 작은 값을 구해서 index i에 놓으면 정렬된 배열을 얻을 수 있다.   

- 선택 정렬 구현
```python
arr = [8, 3, 0, 9, 1, 6, 2, 4, 7, 5]

n = len(arr)
for i in range(n):
    # 가장 작은 데이터의 인덱스
    min_idx = i
    for j in range(i+1, n):
        # 최솟값 찾기
        if (arr[min_idx] > arr[j]):
            min_idx = j
    # 데이터 간의 자리 변경
    arr[i], arr[min_idx] = arr[min_idx], arr[i]

print(arr)
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```   
내부 반복문 → 현재 Index부터 마지막 Index까지 최소값의 Index를 찾아낸다.

외부 반복문 → 최소값의 Index와 현재 Index에 있는 값을 상호 교대(Swap)한다.   

*수업에서의 선택 정렬 구현 예시>*
```python
## 함수 선언 부분 ##
def selectionSort(ary) :
    n = len(ary)
    for i in range(0, n-1) : # 사이클의 반복
        minIdx = i
        for k in range(i+1, n) :
            if ary[k] < ary[minIdx]:
                minIdx = k
        # swap(맨 앞의 값과 최소값을 맞바꿈)        
        ary[minIdx], ary[i] = ary[i], ary[minIdx]
    return ary

## 전역 변수 선언 부분 ##
dataAry = [188, 162, 168, 120, 50, 150, 177, 105]

## 메인 코드 부분 ##
print('정렬 전 -->', dataAry)
dataAry = selectionSort(dataAry)
print('정렬 후 -->', dataAry)
```
```
정렬 전 --> [188, 162, 168, 120, 50, 150, 177, 105]
정렬 후 --> [50, 105, 120, 150, 162, 168, 177, 188]
```
     
## Workshop
### 선택 정렬 응용 문제
```
내림차순으로 자릿수 정렬하기

시간 제한 2초 | 난이도 실버 Ⅴ | 백준 온라인 저지 1427번
배열을 정렬하는 것은 쉽다. 수가 주어지면 그 수의 각 자릿수를 내림차순으로 정렬하시오.

입력

1번째 줄에 정렬할 수 N이 주어진다. N은 1,000,000,000보다 작거나 같은 자연수다.

출력

1번째 줄에 자릿수를 내림차순 정렬한 수를 출력한다.
```
```python
a = list(input())
n = len(a)
for i in range(n-1): # 사이클의 반복
    maxIdx = i
    for j in range((i+1), n):
        if a[maxIdx] < a[j]:
            maxIdx = j
    a[i], a[maxIdx] = a[maxIdx], a[i]
    
for i in range(len(a)):
    print(a[i], end="")
```   
   
→ [**선택 정렬에 대해 알아보자]**(https://heytech.tistory.com/57), [**[알고리즘] 선택 정렬**](https://www.daleseo.com/sort-selection/)   

## 삽입 정렬
***삽입 정렬(Insertion Sort)이란?***

→ 데이터를 하나씩 확인하면서, 각 데이터를 적절한 위치에 삽입하는 방법

① 삽입 정렬은 두번째 인덱스부터 시작한다.

② 해당 인덱스(key 값) 앞에 있는 데이터(B)부터 비교해서 key 값이 더 작으면 B값을 뒤 인덱스로 복사한다.

③ 이를 key 값이 더 큰 데이터를 만날때까지 반복하고, 큰 데이터를 만난 위치 바로 뒤에 key 값을 이동한다.   

- 삽입 정렬 구현
```python
## 함수 선언 부분 ##
def insertionSort(ary) :
    n = len(ary)
    for end in range(1, n) :
        for cur in range(end, 0, -1) :
            if(ary[cur-1] > ary[cur]) :
                ary[cur-1], ary[cur] = ary[cur], ary[cur-1]
    return ary

## 전역 변수 선언 부분 ##
dataAry = [188, 162, 168, 120, 50, 150, 177, 105]

## 메인 코드 부분 ##
print('정렬 전 -->', dataAry)
dataAry = insertionSort(dataAry)
print('정렬 후 -->', dataAry)
```
```
정렬 전 --> [188, 162, 168, 120, 50, 150, 177, 105]
정렬 후 --> [50, 105, 120, 150, 162, 168, 177, 188]
```
내부 반복문 → 정렬 범위에 새롭게 추가된 값과 기존 값들을 뒤에서 부터 계속해서 비교해나가면서 앞의 값이 뒤의 값보다 클 경우 자리 교대(swap)한다.

외부 반복문 → 정렬 범위를 2에서 N으로 확대해 나간다.   

## Workshop
### 성적별 조 편성하기
학생의 성적별로 정렬한 후 가장 성적이 높은 학생과 가장 성적이 낮은 학생을 짝으로 조를 만들어주자. 전체 학생 수는 짝수로 가정한다.   
```python
## 함수 선언 부분 ##
def scoreSort(ary) :
    n = len(ary)
    for end in range(1, n) :
        for cur in range(end, 0, -1) :
            if ( ary[cur-1][1] > ary[cur][1] ) :
                ary[cur-1], ary[cur] = ary[cur], ary[cur-1]
    return ary

## 전역 변수 선언 부분 ##
scoreAry = [['선미', 88], ['초아', 99], ['화사', 71], ['영탁', 78], ['영웅', 67], ['민호', 92]]

## 메인 코드 부분 ##
print('정렬 전 -->', scoreAry)
scoreAry = scoreSort(scoreAry)
print('정렬 후 -->', scoreAry)
print('## 성적별 조 편성표 ##')
for i in range(len(scoreAry)//2) :
    print(scoreAry[i][0], scoreAry[len(scoreAry)-i-1][0])
```
```
정렬 전 --> [['선미', 88], ['초아', 99], ['화사', 71], ['영탁', 78], ['영웅', 67], ['민호', 92]]
정렬 후 --> [['영웅', 67], ['화사', 71], ['영탁', 78], ['선미', 88], ['민호', 92], ['초아', 99]]

## 성적별 조 편성표 ##
영웅 초아
화사 민호
영탁 선미
```
      
→ [**[알고리즘] 삽입 정렬**](https://www.daleseo.com/sort-insertion/)     

## 버블 정렬
***버블 정렬(Bubble Sort)이란?***

→ 첫 번째 값부터 시작해서 바로 앞뒤 데이터를 비교하여 큰 것은 뒤로 보내는 방법

배열 내의 값들을 앞뒤로 서로 비교해서 자리를 바꾸는 작업을 지속적으로 수행해야 한다.   

제일 작은 값을 찾아서 맨 앞에 위치시키는 선택 정렬과 비교했을 때 정반대의 정렬 방향을 가진다!
      
- 버블 정렬의 구현
```python
## 함수 선언 부분 ##
def BubbleSort(ary) :
    n = len(ary)
    for end in range(n-1, 0, -1) :
        for cur in range(0, end) :
            if ary[cur] > ary[cur+1]:
               ary[cur], ary[cur+1] = ary[cur+1], ary[cur]
    return ary

## 전역 변수 선언 부분 ##
dataAry = [188, 162, 168, 120, 50, 150, 177, 105]

## 메인 코드 부분 ##
print('정렬 전 -->', dataAry)
dataAry = BubbleSort(dataAry)
print('정렬 후 -->', dataAry)
```
```
정렬 전 --> [188, 162, 168, 120, 50, 150, 177, 105]
정렬 후 --> [50, 105, 120, 150, 162, 168, 177, 188]
```
내부 반복문 → 첫번째 값부터 이전 패스에서 뒤로 보내놓은 값이 있는 위치 전까지 앞뒤 값을 계속해서 비교해나가면서 앞의 값이 뒤의 값보다 클 경우 자리 교대(swap)를 한다. 

외부 반복문 → 뒤에서 부터 앞으로 정렬 범위를 n-1부터 1까지 줄여나간다.   

- 개선된 버블 정렬의 구현
```python
## 함수 선언 부분 ##
def bubbleSort(ary) :
    n = len(ary)
    for end in range(n-1, 0, -1) :
        changeYN = False
        for cur in range(0, end) :
            if (ary[cur] > ary[cur+1]) :
                ary[cur], ary[cur+1] = ary[cur+1], ary[cur]
                changeYN = True
        if changeYN == False:
            break
            
    return ary

## 전역 변수 선언 부분 ##
dataAry = [50, 105, 120, 188, 150, 162, 168, 177]

## 메인 코드 부분 ##
print('정렬 전 -->', dataAry)
dataAry = bubbleSort(dataAry)
print('정렬 후 -->', dataAry)
```
```
정렬 전 --> [50, 105, 120, 188, 150, 162, 168, 177]
정렬 후 --> [50, 105, 120, 150, 162, 168, 177, 188]
```
   
→ [**[알고리즘] 거품 정렬**](https://www.daleseo.com/sort-bubble/)   

## 퀵 정렬
***퀵 정렬(Quick Sort)이란?***

→ 기준(pivot)을 하나 뽑은 후 기준보다 작은 그룹과 큰 그룹을 나누어 다시 각 그룹으로 정렬하는 방법

= 배열을 pivot 값 기준으로 더 작은 값과 큰 값으로 반복적으로 분할하여 정렬해나가는 방식

**left :** 정렬 대상의 가장 왼쪽 지점을 가리키는 이름

**right :** 정렬 대상의 가장 오른쪽 지점을 가리키는 이름

**pivot :** 기준, 중심점

**low :** 피벗을 제외한 가장 왼쪽에 위치한 지점을 가리키는 이름

**high :** 피벗을 제외한 가장 오른쪽에 위치한 지점을 가리키는 이름   

- 퀵 정렬의 구현
```python
## 함수 선언 부분 ##
def quickSort(ary) :
    n = len(ary)
    if n <= 1 : # 정렬할 리스트의 개수가 1개 이하면
        return ary
    pivot = ary[n // 2]   # 기준값을 중간값으로 지정
    leftAry, rightAry = [], []
    for num in ary :
        if num < pivot : # pivot보다 값이 작으면 leftAry
            leftAry.append(num)
        elif num > pivot : # pivot보다 값이 크면 rightAry
            rightAry.append(num)
    return quickSort(leftAry) + [pivot] + quickSort(rightAry)

## 전역 변수 선언 부분 ##
dataAry = [188, 150, 168,  162, 105, 120,  177,  50]

## 메인 코드 부분 ##
print('정렬 전 -->', dataAry)
dataAry = quickSort(dataAry)
print('정렬 후 -->', dataAry)
```
```
정렬 전 --> [188, 150, 168, 162, 105, 120, 177, 50]
정렬 후 --> [50, 105, 120, 150, 162, 168, 177, 188]
```
   
- 중복값을 고려한 퀵 정렬
```python
## 함수 선언 부분 ##
def quickSort(ary) :
    n = len(ary)
    if n <= 1 :   # 정렬할 리스트의 개수가 1개 이하면
        return ary
    pivot = ary[n // 2]   # 기준값을 중간 값으로 지정
    leftAry, midAry, rightAry = [], [], []
    for num in ary :
        if num < pivot :
            leftAry.append(num)
        elif num > pivot :
            rightAry.append(num)
        else :
            midAry.append(num) 
    return quickSort(leftAry) + midAry + quickSort(rightAry) 

## 전역 변수 선언 부분 ##
dataAry = [120, 120, 188, 150, 168, 50, 50, 162, 105, 120,  177,  50]

## 메인 코드 부분 ##
print('정렬 전 -->', dataAry)
dataAry = quickSort(dataAry)
print('정렬 후 -->', dataAry)
```
```
정렬 전 --> [120, 120, 188, 150, 168, 50, 50, 162, 105, 120, 177, 50]
정렬 후 --> [50, 50, 50, 105, 120, 120, 120, 150, 162, 168, 177, 188]
```
   
- 퀵 정렬의 일반적인 구현
```python
## 함수 선언 부분 ##
def qSort(arr, start, end) :
    if end <= start :
        return
    
    low = start
    high = end
    
    pivot = arr[(low + high) // 2]  # 작은 값은 왼쪽, 큰 값은 오른쪽으로 분리한다.
    while low <= high :
        while arr[low] < pivot :
            low += 1
        while arr[high] > pivot :
            high -= 1
        if low <= high :
            arr[low], arr[high] = arr[high], arr[low]
            low, high = low + 1, high - 1
            
    mid = low
    
    qSort(arr, start, mid-1)
    qSort(arr, mid, end)
    
def quickSort(ary) :
    qSort(ary, 0, len(ary)-1)
    
## 전역 변수 선언 부분 ##
dataAry = [188, 150, 168, 162, 105, 120, 177, 50]

## 메인 코드 부분 ##
print('정렬 전 -->', dataAry)
quickSort(dataAry)
print('정렬 후 -->', dataAry)
```
```
정렬 전 --> [188, 150, 168, 162, 105, 120, 177, 50]
정렬 후 --> [50, 105, 120, 150, 162, 168, 177, 188]
```
   
- **선택 정렬과 퀵 정렬의 성능 비교하기**
    
    **선택 정렬은 O(*N*²)**의 연산횟수를, **퀵 정렬렬은 O(*N log N*)**의 연산 횟수를 갖는다. 
    
    정렬할 데이터양에 따라서 두 정렬 방식의 시간 차이를 비교해 본다. 
    
    데이터는 1000, 10000, 12000, 15000개를 정렬한다.
 
 ```python
 import random
import time

## 함수 선언 부분 ##
def selectionSort(ary) :
    n = len(ary)
    for i in range(0, n-1) :
        minIdx = i
        for k in range(i+1, n) :
            if (ary[minIdx] > ary[k]) :
                minIdx = k
        tmp = ary[i]
        ary[i] = ary[minIdx]
        ary[minIdx] = tmp

    return ary

def qSort(arr, start, end) :
    if end <= start :
        return

    low = start
    high = end

    pivot = arr[(low + high) // 2]	# 작은 값은 왼쪽, 큰 값은 오른쪽으로 분리한다.
    while low <= high:
        while arr[low] < pivot :
            low += 1
        while arr[high] > pivot :
            high -= 1
        if low <= high :
            arr[low], arr[high] = arr[high], arr[low]
            low, high = low + 1, high - 1

    mid = low

    qSort(arr, start, mid-1)
    qSort(arr, mid, end)

def quickSort(ary) :
    qSort(ary, 0, len(ary)-1)

## 메인 코드 부분 ##
countAry = [1000, 10000, 12000, 15000]

for count in countAry :
    tempAry = [ random.randint(10000, 99999) for _ in range(count)]
    selectAry = tempAry[:]
    quickAry = tempAry[:]

    print("## 데이터 수 : ", count, "개")
    start = time.time()
    selectionSort(selectAry)
    end = time.time()
    print("	선택 정렬 --> %10.3f 초" % (end-start))
    start = time.time()
    quickSort(quickAry)
    end = time.time()
    print("	퀵 정렬  --> %10.3f 초" % (end-start))
    print()

    count *= 5
 ```
 ```
 ## 데이터 수 :  1000 개
	선택 정렬 -->      0.059 초
	퀵 정렬  -->      0.002 초

## 데이터 수 :  10000 개
	선택 정렬 -->      3.880 초
	퀵 정렬  -->      0.016 초

## 데이터 수 :  12000 개
	선택 정렬 -->      5.573 초
	퀵 정렬  -->      0.031 초

## 데이터 수 :  15000 개
	선택 정렬 -->      8.411 초
	퀵 정렬  -->      0.047 초
```
데이터의 수가 늘어날수록 처리 속도도 확연히 차이가 나는 것을 볼 수 있다.   

→ [**[알고리즘] 퀵 정렬**](https://www.daleseo.com/sort-quick/), [**정렬 알고리즘 6개 정리**](https://jinhyy.tistory.com/9), [**각 정렬의 특징 및 장단점**](https://coding-factory.tistory.com/615)
