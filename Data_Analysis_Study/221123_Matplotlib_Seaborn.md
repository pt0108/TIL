> 부트캠프 6주차 2022년 11월 23일 

# 11/23 Matplotlib, Seaborn

## Matplotlib (11/22~11/23)

### ****matplotlib API 개요****

정보 시각화는 데이터 분석에서 무척 중요

시각화는 특잇값을 찾아내거나, 데이터 변형이 필요한지 알아보거나, 모델에 대한 아이디어를 찾기 위한 과정의 일부

파이썬 시각화 도구로 matplotlib 활용

→ 공식 사이트 [https://matplotlib.org/](https://matplotlib.org/)

→ [맷플롯립, 데이터 시각화 알아보기](https://laboputer.github.io/machine-learning/2020/05/04/matplitlib-tutorial/)

```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
```

```python
plt.plot([1, 2, 3], [4, 5, 6]) # .plot(x축, y축)
plt.title("Hello Plot")

plt.show() # 주피터 노트북에서는 plt.show()를 하지 않아도 그림이 표시
```

![image](https://user-images.githubusercontent.com/106129152/203497318-b708b5cd-e4eb-407f-9a1a-b9363d219ea4.png)

****Figure와 Axes****

![image](https://user-images.githubusercontent.com/106129152/203497348-af0e7e2a-8989-4489-8a18-867de3dc5d53.png)

**Figure** : 그림을 그리기 위한 도화지의 역할, 그림판의 크기 등을 조절

**Axes** : 실제 그림을 그리는 메소드들과 x축, y축, title등의 속성을 가짐

```
plt.plot([1, 2, 3], [4, 5, 6]) # 기본 설정값의 Figure가 만들어진 후, 내부적으로 Axes.plot()호출
plt.title("Hello Plot") # Axes.set_title() 호출
plt.show() # Figure.show() 호출
```

```python
plt.figure(figsize=(10, 4)) # 가로가 10, 세로가 4인 Figure 객체를 생성해서 반환
plt.plot([1, 2, 3], [4, 5, 6])
plt.title("Hello plot")
plt.show()
```

![image](https://user-images.githubusercontent.com/106129152/203497385-52c5774f-0b82-4933-b34f-95c9fef5a4d8.png)

```python
plt.figure(facecolor='red', figsize=(10, 4))
plt.plot([1, 2, 3], [4, 5, 6])
plt.title("Hello plot")
plt.show()
```

![image](https://user-images.githubusercontent.com/106129152/203497410-8ac08963-812a-41ea-a91a-6b9f267257da.png)

```python
# Figure를 가져옴
plt.figure()
# <Figure size 432x288 with 0 Axes>
# <Figure size 432x288 with 0 Axes>

# Axes를 가져옴
plt.axes()
```

![image](https://user-images.githubusercontent.com/106129152/203497441-00141538-2b31-4146-a0bb-21b67a6544db.png)

```python
# Figure와 Axes를 함께 가져옴 (기본적으로 1개의 Axes를 설정)
fig, axes = plt.subplots()
print(type(fig), type(axes))
```

![image](https://user-images.githubusercontent.com/106129152/203497465-33bef6e5-efcc-40af-90f7-aad7b3aca6db.png)

```python
# Figure와 Axes를 함께 가져옴 (여러개의 Axes를 가지는 Figure 설정)
fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(10, 4))
print(type(fig), type(axes))
```

![image](https://user-images.githubusercontent.com/106129152/203497492-f717bc9a-ee5f-4651-9f1d-6e0c5ccd8b99.png)

****plot 함수 안에 올 수 있는 데이터****

```python
# list
plt.plot([1, 2, 3], [4, 5, 6])

# ndarray
plt.plot(np.array([1, 2, 3]), np.array([4, 5, 6]))

# Series
plt.plot(pd.Series([1, 2, 3]), pd.Series([4, 5, 6]))
```

위의 코드 전부 동일한 결과를 갖는다.

****색상, 마커, 라인스타일 등 변경****

```python
# 그래프의 색 변경
plt.plot([1, 2, 3], [4, 5, 6], 'g') # 'g' : color = 'green'의 축약형
```

![image](https://user-images.githubusercontent.com/106129152/203497663-3605752d-797e-4144-88a3-7c854446eb1b.png)

```python
# 원형 마커 설정하기
plt.plot([1, 2, 3], [4, 5, 6], color='green', marker='o') # 축약형 'go-' 와 같음
```

![image](https://user-images.githubusercontent.com/106129152/203497683-9b40fef0-1c39-4278-bc0f-3d3952115f5b.png)

```python
# 라인 형태 변경하기
plt.plot([1, 2, 3], [4, 5, 6], color='green', marker='o', linestyle='dashed') # 축약형 'go--' 와 동일
```

![image](https://user-images.githubusercontent.com/106129152/203497714-8ebb3be2-d32a-4ead-9e98-011b5492b833.png)

```python
# 마커 사이즈 조절하기
plt.plot([1, 2, 3], [4, 5, 6], color='green', marker='o', linestyle='dashed', linewidth=3, markersize=10)
```

![image](https://user-images.githubusercontent.com/106129152/203497736-1d11ef43-73d1-43e4-aacf-8aa642b70c36.png)

****x축, y축에 축명을 텍스트로 할당. xlabel, ylabel 적용****

```python
plt.plot([1, 2, 3], [4, 5, 6], color='green', marker='o', linestyle='dashed', linewidth=3, markersize=10)
plt.xlabel('x axis')
plt.ylabel('y axis')
```

![image](https://user-images.githubusercontent.com/106129152/203497758-74f9d78c-76e2-4a7d-b079-fc44ec82e8c5.png)

****x축, y축 틱값 표기****

```python
plt.plot([1, 2, 3], [4, 5, 6], color='green', marker='o', linestyle='dashed', linewidth=3, markersize=10)
plt.xlabel('x axis')
plt.ylabel('y axis')

plt.xticks([1, 2, 3]) # x축 눈금
plt.yticks([4, 5, 6]) # y축 눈금
```

![image](https://user-images.githubusercontent.com/106129152/203497788-db2b6783-5ceb-4c08-937f-cbe6f0b3e425.png)  

****x축, y축 틱값을 표현을 회전해서 보여줌****

```python
plt.plot(['hello', 'python', 'world'], [4, 5, 6], color='green', marker='o', linestyle='dashed', linewidth=3, markersize=10)
plt.xlabel('x axis')
plt.ylabel('y axis')

plt.xticks(rotation=70) # x축 눈금
plt.yticks([4, 5, 6]) # y축 눈금
```

![image](https://user-images.githubusercontent.com/106129152/203497852-403219cc-0736-4223-94c3-aa71e5b06f54.png)

****xlim()은 x축값을 제한하고, ylim()은 y축값을 제한****

```python
x = np.arange(100)
y = x*2

plt.plot(x, y)
plt.xticks(np.arange(0, 100, 5))
plt.show()
```

![image](https://user-images.githubusercontent.com/106129152/203497881-d9d9f24b-1892-4013-a502-27cfc73bd4a0.png)

```python
x = np.arange(100)
y = x*2

plt.plot(x, y)
plt.xticks(np.arange(0, 100, 5))

# x축과 y축에 표시될 구간 설정
plt.xlim(0, 50)
plt.ylim(0, 100)
plt.show()
```

![image](https://user-images.githubusercontent.com/106129152/203497903-0e039858-a9f6-4c75-ab36-04784c07b5e4.png)

→ 처음 만들었던 그래프의 (50, 100) 부분만 보여지는 것!

****범례 설정하기****

```python
x = np.arange(100)
y = x*2

plt.plot(x, y, label='test')
plt.xticks(np.arange(0, 100, 5))

# x축과 y축에 표시될 구간 설정
plt.xlim(0, 50)
plt.ylim(0, 100)

# 범례 설정
plt.legend() # label이 함께 설정되어 있어야 함
plt.show()
```

![image](https://user-images.githubusercontent.com/106129152/203497933-3c164a2f-0faa-4c0b-b351-8d218595d948.png)

****여러개의 plot을 하나의 Axes내에서 그리기****

```python
x1 = np.arange(100)
y1 = x1*2

x2 = np.arange(100)
y2 = x2*3

plt.plot(x1, y1, label='y=2x')
plt.plot(x2, y2, label='y=3x')

# 범례 설정
plt.legend() # label이 함께 설정되어 있어야 함
plt.show()
```

![image](https://user-images.githubusercontent.com/106129152/203497962-f808483d-0c2a-4a1b-bd0c-4bae15f1ddce.png)

```python
x1 = np.arange(10)
y1 = x1*2

plt.plot(x1, y1, color='red', marker='^', label='line') # 선 그래프
plt.bar(x1, y1, color='green', label='bar') # 막대 그래프

plt.xticks(x1)
# 범례 설정
plt.legend() # label이 함께 설정되어 있어야 함
plt.show()
```

![image](https://user-images.githubusercontent.com/106129152/203497975-68d50c97-7462-4be9-862f-ae1487ab6235.png)

****Axes 객체에서 직접 작업 하기****

```python
x1 = np.arange(10)
y1 = x1*2

figure = plt.figure()
axes = plt.axes()

axes.plot(x1, y1, color='red', marker='^', label='line') # 선 그래프
axes.bar(x1, y1, color='green', label='bar') # 막대 그래프

axes.set_xticks(x1)

axes.set_xlabel('x axis')
axes.set_ylabel('y axis')

# 범례 설정
axes.legend() # label이 함께 설정되어 있어야 함
plt.show()
```

![image](https://user-images.githubusercontent.com/106129152/203497998-e2a4579e-a5e5-4481-ad94-fb5d2fd86e25.png)

코드는 조금씩 달라도 위에서 만든 그래프와 동일하게 나왔다.

****여러개의 subplots을 가지는 Figure를 생성하고 여기에 개별 그래프를 시각화****

```python
figure, axes = plt.subplots(nrows=2, ncols=2, figsize=(12, 8))

x1 = np.arange(10)
y1 = x1*2

x2 = np.arange(20)
y2 = x2*2

axes[0][0].plot(x1, y1, color='red', marker='o', linestyle='dashed', label='red line') 
axes[0][1].bar(x2, y2, color='green', label='green bar')
axes[1][0].plot(x1, y1, color='green', marker='o', linestyle='dashed', label='green line')
axes[1][1].bar(x2, y2, color='red', label='red bar')

axes[0][0].legend()
axes[0][1].legend()
axes[1][0].legend()
axes[1][1].legend()

axes[0][0].set_xlabel('axes[0][0] x axis')
axes[0][1].set_xlabel('axes[0][1] x axis')
axes[1][0].set_xlabel('axes[1][0] x axis')
axes[1][1].set_xlabel('axes[1][1] x axis')
```

![image](https://user-images.githubusercontent.com/106129152/203498026-7115ddb9-b698-47a4-9445-4c6d8af6d137.png)

legend()는 다 개별적용을 시켜줘야 한다!

## 추측 통계

→ [기술 통계와 추리 통계란 무엇인가?](https://drhongdatanote.tistory.com/25)

위의 링크에 들어가면 통계의 개념에 대해 정리한 많은 포스트들이 있다.

인공지능 부트캠프를 시작한 이후,

수포자나 다름 없던 나에게 어마어마한 지식들이 쏟아져 들어왔다.

특히 이산수학, 선형대수, 확률과 통계 등에 대해서 알고 있는 배경 지식은 거의 0과 다름 없는 판국이기 때문에, 관련 자료를 더 열심히 찾아보고 학습해야할 것 같다.

확률과 통계에 관해서는 [이 책](http://www.yes24.com/Product/Goods/72336483)을 통해 기본 지식을 다지면 좋을 것 같다.

**알아둘 개념**

*출처 :  네이버 지식백과 / 수학백과*

- **독립 시행의 확률**
    
    시행 :  같은 조건에서 반복할 수 있으며, 매번 결과가 달라질 수 있는 관찰이나 실험
    
    독립시행 : 동전이나 주사위를 여러 번 던지는 것처럼 매번 같은 조건에서 어떤 시행을 반복할 때, 각 시행의 결과가 다른 시행의 결과에 영향을 주지 않는 시행
    
- **조건부 확률**
    
    확률 : 표본공간에서 다양한 사건이 일어날 가능성을 따지는 것
    
    조건부확률 :  특정한 사건을 고정하고 그 사건이 일어났다는 조건 하에서 다른 사건이 일어날 확률을 따지는 것
    
- **베이즈의 정리(원인의 확률)**
    
    조건부 확률을 계산하는 방법의 하나
    
    결과 B에 원인 A가 있었을 확률을 구하는 것
    
- **확률변수와 확률분포**
    
    확률변수 : 실험 결과마다 실수를 대응하는 함수
    
    확률분포 : 확률실험의 표본공간에 대하여, 확률분포는 각 사건들의 확률을 결정하는 것
    
- **연속확률변수**
    
    임의로 선택한 사람의 키나 어느 지역의 연간 강수량과 같은 확률변수는 연속된 실수 구간의 값을 취할 수 있는데 이런 확률변수를 연속확률변수라고 함
    
- **정규분포**
    
    도수분포곡선이 평균값을 중심으로 하여 좌우대칭인 종 모양을 이루는 것
    
- **이항분포**
    
    일정한 확률을 가진 독립시행을 반복할 때 확률변수 X가 따르는 분포
    

네이버 지식백과에서 정말 짧게 뜻만 써놓은 것을 적어두었다. 

개념을 정확히 이해하려면 더 깊은 공부가 필요할 것 같다.

## Seaborn

- Seaborn 공식 사이트 : [https://seaborn.pydata.org/tutorial.html](https://seaborn.pydata.org/tutorial.html)
- Matplotlib 기반으로 쉽게 작성됨. Matplotlib의 high level API
- Matplotlib보다 수려한 디자인을 제공, Pandas와 쉽게 연동
- Matplotlib을 어느 정도 알고 있어야 한다.

→ [seaborn 데이터 시각화](https://datascienceschool.net/01%20python/05.04%20%EC%8B%9C%EB%B3%B8%EC%9D%84%20%EC%82%AC%EC%9A%A9%ED%95%9C%20%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EB%B6%84%ED%8F%AC%20%EC%8B%9C%EA%B0%81%ED%99%94.html)

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
titanic_df = pd.read_csv('./datasets/titanic_train.csv')
titanic_df.head()
```

![image](https://user-images.githubusercontent.com/106129152/203498766-f699f09d-d027-405a-b74a-0d1da111e6b2.png)

### 수치형 데이터 시각화

**1. 히스토그램**

수치형 데이터의 구간별 빈도수를 나타내는 그래프

- matplotlib 지원
    
    ```python
    hist = plt.hist(titanic_df['Age'], bins=20)
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/203498800-ae2d6b21-d945-4bfd-8eba-920944899662.png)
    
- pandas에서 직접 호출 가능
    
    ```python
    titanic_df['Age'].hist(bins=20)
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/203498826-7b7f2ddc-f008-44e1-852c-91cadb6b939c.png)
    
- seaborn 지원
    
    ```python
    sns.histplot(data=titanic_df, x='Age', bins=20)
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/203498852-fd2f3633-4270-43a8-8a42-6b7814fc2e90.png)
    
    ```python
    sns.histplot(data=titanic_df, x='Age', bins=20, hue='Survived', multiple='stack')
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/203498876-30b48626-8526-49cd-939f-9ae5cb2d02c8.png)
    
    ```python
    sns.histplot(data=titanic_df, x='Age', bins=20, kde=True)
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/203499234-a1fbd9a4-c412-479c-9ed2-186c74f36229.png)
    

**2. 커널밀도추정 함수**

히스토그램을 매끄럽게 곡선으로 연결한 그래프

```python
sns.kdeplot(data=titanic_df,x='Age')
```

![image](https://user-images.githubusercontent.com/106129152/203499256-beb2908c-bb73-4ce6-9f13-99e8990f6d63.png)

```python
sns.kdeplot(data=titanic_df,x='Age', hue='Survived', multiple='stack')
```

![image](https://user-images.githubusercontent.com/106129152/203499271-d23fc843-a3f2-4c01-815b-3c4c9ee6a3e1.png)

```python
sns.displot(data=titanic_df, x='Age', kde=True, rug=True)
```

![image](https://user-images.githubusercontent.com/106129152/203499293-564fd335-7232-43b6-b8a2-b6bd971e7b2e.png)

여기서 참고하면 좋은 것이 있는데,

seboarn의 함수는 크게 figure level과 axes level로 나뉜다.

![image](https://user-images.githubusercontent.com/106129152/203499314-bb711ca2-0a62-4b86-8359-0fe7536df197.png)

위 이미지에서 가장 상위에 있는 큰 네모 안의 함수들이 figure level 함수인데, 

figure level 함수는 axes level 함수와 달리 matplotlib에 영향을 받지 않는다. 

axes level 함수는 matplotlib의 axes에 그리기 때문에 matplotlib의 메소드와 연계할 수 있다.

### 범주형 데이터 시각화

**1. 막대그래프(barplot)**

범주형 데이터 값에 따라 수치형 데이터 값이 어떻게 달라지는지 파악할 때 사용

범주형 데이터에 따른 수치형 데이터의 평균과 신뢰구간을 그려줌

수치형 데이터 평균은 막대높이로, 신뢰구간은 오차 막대로 표현함

```python
sns.barplot(data=titanic_df, x='Pclass', y='Age')
# ci = None 을 넣으면 오차막대가 표시되지 않음
```

![image](https://user-images.githubusercontent.com/106129152/203499365-a58aad70-fe36-48be-8c2f-a574d9f1da18.png)

```python
sns.barplot(data=titanic_df, x='Pclass', y='Age', hue='Sex')
```

![image](https://user-images.githubusercontent.com/106129152/203499389-2648d0b3-7693-4952-a35a-f9530533d93c.png)

```python
sns.barplot(data=titanic_df, x='Pclass', y='Survived', hue='Sex')
```

![image](https://user-images.githubusercontent.com/106129152/203499417-bbacba33-7dc8-4f54-8b7b-b5c4c9f122bd.png)

```python
# Age 카테고리를 만들어서 시각화
bins = [0, 18, 25, 35, 60, 80]
group_names = ['Childeren', 'Youth', 'YoungAdult', 'MiddleAged', 'Senior']
titanic_df['Age_cat']= pd.cut(titanic_df['Age'], bins, labels=group_names)

sns.barplot(data=titanic_df, x='Age_cat', y='Survived')
```

![image](https://user-images.githubusercontent.com/106129152/203499443-66f9f26f-8f99-4247-866d-9176474595cb.png)

```python
sns.barplot(data=titanic_df, x='Sex', y='Survived', hue='Age_cat')
```

![image](https://user-images.githubusercontent.com/106129152/203499486-7412e774-e159-414f-952d-b39287f10b62.png)

**2. 포인트 플롯(pointplot)**

막대 그래프와 모양만 다를 뿐 동일한 정보 제공

막대 그래프와 마찬가지로 범주형 데이터에 따른 수치형 데이터의 평균과 신뢰구간을 나타냄

다만 그래프를 점과 선으로 나타냄

```python
sns.pointplot(data=titanic_df, x='Pclass', y='Fare', hue='Age_cat')
```

![image](https://user-images.githubusercontent.com/106129152/203499518-b47cc088-d28a-44ca-a819-03ddce721c22.png)

**3. 박스플롯(boxplot)**

막대그래프나 포인트플롯보다 더 많은 정보를 제공

5가지 요약 수치 : 최솟값, 1사분위수(Q1), 2사분위수(Q2), 3사분위수(Q3), 최댓값

1사분위수(Q1) : 전체 데이터 중 하위 25%에 해당하는 값

2사분위수(Q2): 50%에 해당하는 값

3사분위수(Q3) : 상위 25%에 해당하는 값

사분위 범위수(IQR) : Q3 - Q1

최댓값(Max) : Q3 + (1.5 * IQR)

최솟값(Min) : Q1 - (1.5 * IQR)


```python
sns.boxplot(data=titanic_df, x='Pclass', y='Age')
```

![image](https://user-images.githubusercontent.com/106129152/203499590-3928f82b-8b4b-4995-bdf3-1a74d4f15dc1.png)

**4. 바인올린플롯(violinplot)**

박스플롯과 커널밀도추정 함수 그래프를 합쳐 놓은 그래프

박스플롯에 제공하는 정보를 모두 포함하며, 모양은 커널밀도추정 함수 그래프 형태


```python
sns.violinplot(data=titanic_df, x='Pclass', y='Age')
```

![image](https://user-images.githubusercontent.com/106129152/203499670-c4d3f127-e13c-4b1c-a13c-860016364b8e.png)

```python
sns.violinplot(data=titanic_df, x='Pclass', y='Age', hue='Sex', split=True)
```

![image](https://user-images.githubusercontent.com/106129152/203499689-80a8661d-4ef6-4f7f-8c8c-6d3203f9d886.png)

**5. 카운트플롯(countplot)**

카운트플롯은 범주형 데이터의 개수를 확인할 때 사용하는 그래프

주로 범주형 피처나 범주형 타깃값의 분포가 어떤지 파악하는 용도로 사용

카운트플롯을 사용하면 범주형 데이터의 개수를 파악할 수 있음

```python
sns.countplot(data=titanic_df, x='Pclass')
# titanic_df['Pclass'].value_counts()의 시각화나 다름없음
```

![image](https://user-images.githubusercontent.com/106129152/203499717-1201a9fa-2023-47ac-b457-62eb1eaf5be9.png)

y축에 데이터를 넣으면 수평 그래프로 나타난다. (값은 동일)

```python
sns.countplot(data=titanic_df, y='Pclass')
```

![image](https://user-images.githubusercontent.com/106129152/203499737-f5240c8f-57dc-4aea-93a8-d43450095f92.png)

**6. 파이 그래프(pie)**

범주형 데이터별 비율을 알아볼 때 사용하기 좋은 그래프

seaborn에서 파이 그래프를 지원하지 않아 matplotlib을 사용

```python
data = titanic_df['Pclass'].value_counts()
data.plot(kind='pie', autopct='%.2f%%')
```

![image](https://user-images.githubusercontent.com/106129152/203499767-44b5b69e-f69e-4290-8b74-d5240880c647.png)

### 데이터 관계 시각화

**1. 히트맵(heatmap)**

데이터 간 관계를 색상으로 표현한 그래프

비교해야 할 데이터가 많을 때 주로 사용

```python
corr = titanic_df.corr()

plt.figure(figsize=(8, 8))
sns.heatmap(corr, annot=True, fmt='.2f', cmap='YlGnBu', linewidth=0.5)
```

![image](https://user-images.githubusercontent.com/106129152/203499797-27518860-64be-4e19-9e47-fb4608448e9b.png)

**2. 산점도(scatterplot)**

산점도는 두 데이터의 관계를 점으로 표현하는 그래프

```python
sns.scatterplot(data=titanic_df, x='Age', y='Fare', hue='Sex')
# 데이터의 상관관계가 뚜렷하지 않음
```

![image](https://user-images.githubusercontent.com/106129152/203499814-ba01c49f-81f4-451a-af0e-98ed6b11a45f.png)

```python
sns.regplot(data=titanic_df, x='Age', y='Fare')
```

![image](https://user-images.githubusercontent.com/106129152/203499847-0eea9316-299a-4b0b-b35f-0086271e9a75.png)

### seaborn에서 subplots 이용하기

```python
figure, axes = plt.subplots(nrows=2, ncols=2)
sns.regplot(data=titanic_df, x='Age', y='Fare', ax=axes[0][0])
```

![image](https://user-images.githubusercontent.com/106129152/203499865-b8c7c36a-6c88-48da-a0f5-e6ef011a6f89.png)

→ 이런 식으로도 사용이 가능하다.

****(1) subplots을 이용하여 주요 category성 컬럼의 건수를 시각화****

```python
cat_columns = ["Survived", "Pclass", "Sex", "Embarked", "Age_cat"]

figrue, axes = plt.subplots(nrows=1, ncols=len(cat_columns), figsize=(22, 4))

for index, column in enumerate(cat_columns):
    sns.countplot(data=titanic_df, x=column, ax=axes[index] )
    if (index == 4):
        print(axes[4].get_xticklabels())
        axes[4].set_xticklabels(axes[4].get_xticklabels(), rotation=90)
```

![image](https://user-images.githubusercontent.com/106129152/203499889-7f387319-ad1b-4b84-88c5-4bf20639aa64.png)

****(2) subplots을 이용하여 주요 category성 컬럼별로 컬럼값에 따른 생존율 시각화****

```python
cat_columns = ["Pclass", "Sex", "Embarked", "Age_cat"]

figrue, axes = plt.subplots(nrows=1, ncols=len(cat_columns), figsize=(22, 4))

for index, column in enumerate(cat_columns):
    sns.barplot(data=titanic_df, x=column, y="Survived", ax=axes[index])
```

![image](https://user-images.githubusercontent.com/106129152/203499978-edcbffc2-7d1a-45bb-a21a-c33e9e7453d4.png)
