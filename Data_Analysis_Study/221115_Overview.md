> 부트캠프 5주차 2022년 11월 15일

- **데이터 분석 개요**
    
    
    **Step 1: 질문하기 (Ask questions)**
    
    데이터가 주어진 상태에서 질문을 할 수도 있고, 
    
    질문에 답할 수 있는 데이터를 수집할 수도 있다.
    
    **Step 2: 데이터 랭글링 (Wrangle data)**
    
    데이터 랭글링 : 원자료(raw data)를 보다 쉽게 접근하고 분석할 수 있도록 데이터를 정리하고 통합하는 과정 (참고. 위키피디아)
    
    세부적으로는 데이터의 수집(gather), 평가(assess), 정제(clean) 작업으로 나눌 수 있다.
    
    **Step 3: 데이터 탐색 (Exploratory Data Analysis)**
    
    데이터의 패턴을 찾고, 관계를 시각화 하는 작업을 통해 데이터에 대한 직관을 극대화 한다.
    
    → 시각화가 상당히 중요하고, 통계 지식이 필요하다.
    
    **Step 4: 결론 도출 또는 예측 (Draw conclusions or make predictions)**
    
    Step 3에서 분석한 내용을 근거로 질문에 대한 답과 결론을 도출할 수 있다.
    
    머신러닝 또는 통계 추정 과정을 거치게 되면 예측을 만들어 낼 수도 있다.
    
    → 예측 : 과거의 데이터를 가지고 미래를 짐작하는 것.
    
    **Step 5: 결과 공유 (Communicate the results)**
    
    보고서, 이메일, 블로그 등 다양한 방법을 통해 발견한 통찰들을 공유할 수 있다.
    

- **Case Study**
    
    
    참고 : **Kaggle**, 즉 캐글은 예측 모델 분석 대회 플랫폼으로 공부에 정말 도움이 되는 사이트다.
    
    캐글에 관해서는 아래의 링크를 참고하면 좋다! 
    
    이 글을 보고 캐글 필사라는 것에 대해 알게 되었고, 앞으로의 계획에 추가하게 되었다.
    
    [데이터 과학 및 캐글 입문자를 위한 캐글 필사 알아보기](https://modulabs.co.kr/blog/data-science-kaggle/)
    
    **Bike Sharing Demand**
    
    - 도시 자전거 공유 시스템 사용 예측
    - [캐글](https://www.kaggle.com/)의 [Bike Sharing Demand](https://www.kaggle.com/c/bike-sharing-demand)에서 `train.csv`와 `test.csv`를 다운로드
    - 두 파일을 각각 datasets 디렉토리에 bike_train.csv bike_test.csv로 저장
    
    **datetime** : hourly date + timestamp
    
    **season** : 1 = 봄, 2 = 여름, 3 = 가을, 4 = 겨울
    
    **holiday**: 1 = 토, 일요일의 주말을 제외한 국경일 등의 휴일, 0 = 휴일이 아닌 날
    
    **workingday**: 1 = 토, 일요일의 주말 및 휴일이 아닌 주중, 0 = 주말 및 휴일
    
    **weather**:
    
    - 1 = 맑음, 약간 구름 낀 흐림
    - 2 = 안개, 안개 + 흐림
    - 3 = 가벼운 눈, 가벼운 비 + 천둥
    - 4 = 심한 눈/비, 천둥/번개
    
    **temp**: 온도(섭씨)
    
    **atemp**: 체감온도(섭씨)
    
    **humidity**: 상대습도
    
    **windspeed**: 풍속
    
    **casual**: 사전에 등록되지 않는 사용자가 대여한 횟수
    
    **registered**: 사전에 등록된 사용자가 대여한 횟수
    
    **count**: 대여 횟수
    
    **Step 1: 질문하기 (Ask questions)**
    
    *예시*
    
    질문 1) 어떤 기상 정보가 자전거 대여량에 영향을 미치는가?
    
    질문 2) 어떤 날짜(요일, 달, 계절 등)에 대여량이 많고 적은가?
    
    질문 3) 언제 프로모션을 하면 좋은가?
    
    **Step 2: 데이터 랭글링 (Wrangle data)**
    
    - **데이터 적재**
        
        ```python
        # pandas 모듈 import
        import pandas as pd
        ```
        
    - **데이터 평가**
        
        ```python
        # 데이터프레임 = pd.read_csv(파일명)
        bike = pd.read_csv('./datasets/bike_train.csv')
        ```
        
        → **csv (comma-separated values) :** 몇 가지 필드를 쉼표(,)로 구분한 텍스트 데이터 및 텍스트 파일.
        
        ```python
        type(bike)
        # pandas.core.frame.DataFrame
        ```
        
        ```python
        bike.head() # 데이터를 훑어볼 수 있음
        ```
        
        ![image](https://user-images.githubusercontent.com/106129152/201863358-dbb3138d-0e1f-4eb1-88a7-8777a8f99c6c.png)
        
        head 함수를 사용하면 위의 사진처럼 출력된다.
        
        ```python
        bike.info() # 데이터 타입, 데이터 누락건수, 컬럼수, 샘플수 등을 알 수 있음
        ```
        
        ```
        <class 'pandas.core.frame.DataFrame'>
        RangeIndex: 10886 entries, 0 to 10885
        Data columns (total 12 columns):
         #   Column      Non-Null Count  Dtype
        ---  ------      --------------  -----
         0   datetime    10886 non-null  object
         1   season      10886 non-null  int64
         2   holiday     10886 non-null  int64
         3   workingday  10886 non-null  int64
         4   weather     10886 non-null  int64
         5   temp        10886 non-null  float64
         6   atemp       10886 non-null  float64
         7   humidity    10886 non-null  int64
         8   windspeed   10886 non-null  float64
         9   casual      10886 non-null  int64
         10  registered  10886 non-null  int64
         11  count       10886 non-null  int64
        dtypes: float64(3), int64(8), object(1)
        memory usage: 1020.7+ KB
        ```
        
        위 결과를 통해 10886개의 행, 누락된 데이터 없음, 12개의 컬럼, float 타입 3개, int 타입 8개, object 타입 1개, 사용된 메모리 등의 정보를 알 수 있다.
        
    
    - **데이터 정제** (누락된 값 처리, 잘못된 데이터 타입)
        
        이 csv 파일의 날짜 정보가 담겨져 있는 datetime이 object 타입으로 되어있다.
        
        용이한 데이터 사용을 위해 int 타입으로 바꾸려고 한다.
        
        ```python
        # bike 데이터프레임에서 datetime이란 열의 값
        bike['datetime'] # bike.datetime 와 동일
        ```
        
        ```
        0        2011-01-01 00:00:00
        1        2011-01-01 01:00:00
        2        2011-01-01 02:00:00
        3        2011-01-01 03:00:00
        4        2011-01-01 04:00:00
                        ...
        10881    2012-12-19 19:00:00
        10882    2012-12-19 20:00:00
        10883    2012-12-19 21:00:00
        10884    2012-12-19 22:00:00
        10885    2012-12-19 23:00:00
        Name: datetime, Length: 10886, dtype: object
        ```
        
        ```python
        # object 타입이었던 datetime이 아래 함수를 통해 datetime 타입으로 바뀜
        bike['datetime'] = bike['datetime'].apply(pd.to_datetime)
        
        # 컬럼 추가
        bike['year'] = bike['datetime'].apply(lambda x : x.year)
        bike['month'] = bike['datetime'].apply(lambda x : x.month)
        bike['hour'] = bike['datetime'].apply(lambda x : x.hour)
        bike['dayofweek'] = bike['datetime'].apply(lambda x : x.dayofweek) # 요일
        ```
        
        다시 info() 함수를 사용해서 확인해보면, object 타입이 datetime 타입으로 바뀌고, 8개였던 int 타입이 12개로 늘어난 것을 확인할 수 있다.
        
        ```
        <class 'pandas.core.frame.DataFrame'>
        RangeIndex: 10886 entries, 0 to 10885
        Data columns (total 16 columns):
         #   Column      Non-Null Count  Dtype
        ---  ------      --------------  -----
         0   datetime    10886 non-null  datetime64[ns]
         1   season      10886 non-null  int64
         2   holiday     10886 non-null  int64
         3   workingday  10886 non-null  int64
         4   weather     10886 non-null  int64
         5   temp        10886 non-null  float64
         6   atemp       10886 non-null  float64
         7   humidity    10886 non-null  int64
         8   windspeed   10886 non-null  float64
         9   casual      10886 non-null  int64
         10  registered  10886 non-null  int64
         11  count       10886 non-null  int64
         12  year        10886 non-null  int64
         13  month       10886 non-null  int64
         14  hour        10886 non-null  int64
         15  dayofweek   10886 non-null  int64
        dtypes: datetime64[ns](1), float64(3), int64(12)
        memory usage: 1.3 MB
        ```
        
    
    ****Step 3: 데이터 탐색 (Exploratory Data Analysis)****
    
    - **질문 1에 대한 분석** : 기상정보(온도, 체감온도, 풍속, 습도)와 자전거 대여량의 관계
        - (1) 산점도로 확인
            
            ```python
            # plot = pandas의 시각화 메서드
            bike.plot(kind='scatter', x='temp', y='count', alpha=0.3) # scatter : 산점도, 두 변수의 관계를 보여주는 자료 표시 방법
            ```
            
            ![image](https://user-images.githubusercontent.com/106129152/201863452-d2ee1543-fc70-4d86-b122-1d41f41e19a3.png)
            
            ```python
            # matplotlib
            import matplotlib.pyplot as plt
            
            fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(14,8))
            axes[0][0].scatter(bike['temp'], bike['count'], alpha = 0.3) # 온도에 따른 사용량 추이
            axes[0][1].scatter(bike['atemp'], bike['count'], alpha = 0.3) # 체감온도에 따른 사용량 추이
            axes[1][0].scatter(bike['humidity'], bike['count'], alpha = 0.3) # 습도에 따른 사용량 추이
            axes[1][1].scatter(bike['windspeed'], bike['count'], alpha = 0.3) # 풍속에 따른 사용량 추이
            ```
            
            ![image](https://user-images.githubusercontent.com/106129152/201863659-2bb63b7a-df7b-4236-9d4c-dd557b0abe55.png)
            
        - (2) 상관계수 (산점도를 통해 나온 결과를 수치화된 데이터로 알려줌)
            
            ```python
            # 상관계수 연산, correlation을 뜻하는 corr함수를 이용하면 각 컬럼간의 양상을 확인할 수 있다. (-1, 1 사이의 결과)
            bike.corr()
            ```
            
            컬럼이 많아 잘렸지만, 이런 식으로 결과가 출력된다.
            
            ![image](https://user-images.githubusercontent.com/106129152/201863705-9a87cacb-2967-4034-a038-50ff34c56edb.png)
            
    
    **분석 결과**
    
    → 기상 정보 중 온도와 체감온도가 자전거 대여 수량에 영향을 미칠 것으로 보임 (산점도, 상관계수)
    
    - **질문 2에 대한 분석** : year, month, hour, dayofweek 특성에 따른 자전거 대여량이 어떻게 달라지는지 분석
        
        ```
        <참고>
        year, month, hour, dayofweek : **범주**형 데이터
        count(자전거 대여량) : **수치**형 데이터
        범주형 데이터 값에 따라 수치형 데이터가 어떻게 달라지는지 파악할 때 막대 그래프(barplot) 유용
        ```
        
        ```python
        import seaborn as sns
        
        fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(14,8))
        sns.barplot(data=bike, x='year', y='count', ax=axes[0][0])
        sns.barplot(data=bike, x='month', y='count', ax=axes[0][1])
        sns.barplot(data=bike, x='hour', y='count', ax=axes[1][0])
        sns.barplot(data=bike, x='dayofweek', y='count', ax=axes[1][1])
        ```
        
        ![image](https://user-images.githubusercontent.com/106129152/201863750-59abe06e-6272-4906-ad31-dc91c5f78cba.png)
        
        **분석 결과**
        
        - 연도별 평균 대여량은 2011년도보다 2012년도에 더 많음
        - 월별 평균 대여량은 6월이 가장 많고, 7~10월에도 많음. 1월에 대여량이 가장 적음
        - 시간대별 평균 대여량은 오전 8시 전후와 오후 5~6시 부근에 많음
    
    ****Step 4: 결론 도출 또는 예측 (Draw conclusions or make predictions)****
    
    → 질문 1, 질문 2에 대한 분석결과를 확인
    
    - 온도에 따른 자전거 대여량의 변화가 예상되므로 이에 맞는 재고 관리 전략 수립
    - 시기별(연도, 월, 시간대)로 대여량의 변화가 예상되므로 이에 맞는 프로모션 전략 수립
    
    ****Step 5: 결과 공유 (Communicate the results)****
    
    → 자전거 대여량을 예측할 때 고려해야 할 중요한 특성(기상정보, 시기)을 설명하는 보고서, PPT등을 준비
    
    *참고 링크 : [산점도와 상관관계](https://ko.khanacademy.org/math/statistics-probability/describing-relationships-quantitative-data/introduction-to-scatterplots/a/scatterplots-and-correlation-review) , [matplotlib 사용법 기초](https://engineer-mole.tistory.com/215) , [pandas corr 함수](https://steadiness-193.tistory.com/97) , [seaborn을 통한 그래프 만들기](https://continuous-development.tistory.com/153?category=736681)*
