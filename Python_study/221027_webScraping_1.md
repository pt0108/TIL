> 부트캠프 2주차 2022년 10월 27일   

## 웹 크롤링의 기초 개념
- **웹 크롤링 vs 웹 스크래핑**
    
    **웹 크롤러(Web Crawler) :** 웹 사이트에 있는 수많은 정보 가운데 우리가 원하는 정보를 수집하는 프로그램
    
    **웹 크롤링(Web Crawling) :** 웹 크롤러를 이용해 데이터를 수집하는 행위
    
    **웹 스크래핑(Web Scraping) :** 웹 사이트에서 원하는 정보를 추출하는 것은 웹 크롤링과 동일함. 그러나 전체 사이트의 데이터가 아닌 원하는 정보 일부만을 추출
    

- **웹 크롤링 프로세스**
    
    ① 정보를 얻고자 하는 웹 사이트에 접속해 웹 페이지를 확인한다.
    
    ② 키보드의 F12 키 또는 개발자 도구로 들어가 원하는 정보의 위치를 확인하고 분석한다.
    
    ③ 파이썬 코드를 작성해 접속한 웹 페이지의 html 코드를 불러온다.
    
    ④ 불러온 데이터에서 원하는 정보를 가공한 후 추출한다.
    
    ⑤ 추출한 정보를 csv나 데이터베이스 등 다양한 형재로 저장하거나 가공하고 시각화한다.
    
- **클라이언트 서버 개념**
    
    
    ![image](https://user-images.githubusercontent.com/106129152/200739992-40a26592-7394-4b73-a6c1-c62f40f82685.png)
    
- **HTTP 통신의 이해**

    ![image](https://user-images.githubusercontent.com/106129152/200740027-b0197313-00b3-4d02-b91c-7c2dead6cc7c.png)
      
      
## 웹 페이지의 구성 요소들
*참고 사이트 : [https://www.w3schools.com/](https://www.w3schools.com/)*

*→ 이번 파트 내용은 이미 잘 알고 있는 내용들이기 때문에 상세하게 적지는 않았다! 완전한 수업 내용을 다시 보고 싶으면 주피터 파일 확인.*

- **HTML**
    
    웹페이지의 뼈대
```HTML
<!doctype html>
<html>
   <head>
       <meta charset="utf-8">
       <title> 기초 스크래핑 </title>
   </head>
   <body>
       <div>
           <h1> 스크래핑을 해봅시다! </h1>
           <h2> - 2022.10.27 </h2>
       </div>
   </body>
</html>
```
```
<!doctype html> : 문서타입이 HTML 문서라는 의미   
<html> : HTML 문서의 시작과 끝을 의미, 작성하고자 하는 모든 웹 문서는 <html> 태그 사이에 있어야 함   
<head> : 웹브라우저가 문서를 해석하는데 필요한 정보들을 입력하는 곳   
<title> : 웹브라우저의 제목 표시줄에 표시   
<body> : 웹페이지에서 보게 될 주요 정보들   
```
     
- 속성 추가
```
<img> 태그의 경우는 속성을 추가해서 이미지의 가로길이, 세로길이 등으로 이미지의 크기를 조정할 수 있음.
<img src="./image/image01.jpg, width="200", height="100">

<a> 태그의 경우도 연결할 링크 정보 등을 넣을 수 있음.
<a href="http://google.com"> Google </a>
```
   
- 종료 태그가 없는 태그들
```
<br>, <img>, <link>, <input>, ...
```
   
- 자주 사용하는 HTML 태그들
```
<h1> 제목 </h1> : 가장 큰 폰트 사용 (주로 제목을 쓸 때 사용)
<p> 문단 </p> : 줄바꿈 없는 한 문단
<li> 목록, 리스트 </li> : 목록을 만들 때 사용
<table> 표 </table>, <tr>, <td>, <th> : 표를 만들 때 사용
<div> </div> : 레이아웃 구분할 때 사용, 블록 단위 부분 공간 정의 (일종의 사각형이라고 생각하면 됨)
<span> </span> : 레이아웃 구분할 때 사용, 줄 단위 부분 공간 정의
```
   
- **HTML의 계층 구조**
    
    → Tree 형태의 부모 자식 관계로 이해   
    
- **CSS**
    
    문서의 스타일을 꾸며주는 기능
    
- **JavaScript**
    
    컨텐츠를 동적으로 바꿔주는 기능
       
       
## BeautifulSoup 라이브러리
→ 크롤링 하는 데 필요한 함수를 한 데 모아 놓은 라이브러리
```python
from bs4 import BeautifulSoup
```
문서를 해석하는 것을 “파싱”이라고 하는데, BeautifulSoup를 이용해서 파싱 후 생성된 객체를 아래와 같이 변수에 담으면 된다.
```python
BeautifulSoup(파싱할 대상 문서, 구문 분석 엔진)
```
   
구문을 분석할 엔진에는 html.parser, lxml등 여러가지가 있는데, 오늘 수업에서는 ‘***lxml***’을 사용했다.

- **lxml이란?**
    
    → **구문분석기**
    
    형식을 정확히 지키지 않은 HTML 코드를 분석할 때 html.parser 보다 낫다.
    
    닫히지 않은 태그, 계층 구조가 잘못된 태그, `<head>`나 `<body>` 태그가 없는 등의 문제에서 멈추지 않고 알아서 수정하고, 속도가 빠르다는 장점이 있다.

   
**find 와 select의 차이**

**find** 메소드는 태그를 이용하여 원하는 부분을 추출한다.

**select** 메소드는 **CSS Selector** 로 태그를 찾아 반환한다.

`soup.select_one(**"div > p"**)` (div의 하위 p 찾기)

`soup.select(**"#link1 ~ .sister"**)` (id랑 class 선택자로 찾기)

위와 같이 select는 CSS 선택자를 사용해서 더 직관적인 방법으로 찾을 수 있다!   

- 속성의 값 보기
```python
soup.a.attrs # 해당 태그(a태그)의 속성 전체를 확인할 수 있음
# {'href': 'http://www.naver.com', 'class': ['portal'], 'id': 'naver'}

soup.p.attrs
# {'id': 'title'}

soup.a['href']
# 'http://www.naver.com'

soup.a['class']
# ['portal']

soup.a['id']
# 'naver'
```
   
→ [**웹 크롤링 BeautifulSoup**](https://velog.io/@jisu0807/%EC%9B%B9%ED%81%AC%EB%A1%A4%EB%A7%81-BeautifulSoup%EC%97%90%EC%84%9C-find%EC%99%80-select-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)   

## 웹 스크래핑 응용(1)
   
- **requests 모듈**
    
    *→ 참고 : [https://realpython.com/python-requests/](https://realpython.com/python-requests/)*
```python
import requests

response = requests.get('http://google.com')
response.status_code
# 200
```
여기서 200은 [*http 상태 코드*](https://developer.mozilla.org/ko/docs/Web/HTTP/Status)인데, 응답에 성공했다는 뜻이다.   

- 응답받은 페이지가 성공적이지 않을 때
```python
response = requests.get('https://search.daum.net/searc?w=tot&q=2021%EB%85%84%EC%98%81%ED%99%94%EC%88%9C%EC%9C%84&DA=MOR&rtmaxcoll=MOR')

if response.status_code == 200:
    pass
else:
    print("status error", response.status_code)
# status error 404
```
```python
response = requests.get('https://search.daum.net/searc?w=tot&q=2021%EB%85%84%EC%98%81%ED%99%94%EC%88%9C%EC%9C%84&DA=MOR&rtmaxcoll=MOR')
response.raise_for_status()
```
```python
HTTPError                                 Traceback (most recent call last)
InputIn [6], in <cell line: 2>()      1 response = requests.get('https://search.daum.net/searc?w=tot&q=2021%EB%85%84%EC%98%81%ED%99%94%EC%88%9C%EC%9C%84&DA=MOR&rtmaxcoll=MOR')
----> 2 response.raise_for_status()

File~\anaconda3\lib\site-packages\requests\models.py:960, in Response.raise_for_status(self)    957     http_error_msg = u'%s Server Error:%s for url:%s' % (self.status_code, reason, self.url)
    959if http_error_msg:
--> 960raise HTTPError(http_error_msg, response=self)

HTTPError: 404 Client Error: Not Found for url:https://search.daum.net/searc?w=tot&q=2021%EB%85%84%EC%98%81%ED%99%94%EC%88%9C%EC%9C%84&DA=MOR&rtmaxcoll=MOR
```
→ raise_for_status() 메소드를 사용하면 위와 같이 출력된다.
```
response = requests.get('http://google.com')
response.raise_for_status()
with open("mygoogle.html", 'w', encoding='utf-8') as fd: # utf-8 : unicode 인코딩 방식
    fd.write(response.text)
```
   
- **User Agent**
    
    URL을 Request하는 Client의 종료를 싣어 보낸다.
    
    같은 URL을 Request 하더라도 모바일 디바이스와 PC가 받는 데이터가 다른 이유.
    
    Crawler 같은 자동화 프로그램이 서버에 접근하면 여러 문제가 생길 수 있으므로 차단할 필요가 있다. 이 부분을 마치 Browser가 요청하듯이 바꿀 수 있는 방법이 User Agent를 조정하는 것이다.
    
    Google에서 user agent string으로 검색하면 [해당 사이트](https://www.whatismybrowser.com/detect/what-is-my-user-agent/)에서 현재 브라우저의 User Agent를 표시해준다! Client마다 서버로 보내는 정보가 다르다는 것을 확인할 수 있다.   
 ```python
 user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36"

headers = {"User-Agent" : user_agent}
response = requests.get("http://google.com", headers)
response.raise_for_status()
with open("mygoogle2.html", 'w', encoding='utf-8') as fd: # utf-8 : unicode 인코딩 방식
    fd.write(response.text)
 ```
   

## Workshop
네이버 웹툰의 연재 중인 웹툰 제목을 전부 출력해보자!
```python
from bs4 import BeautifulSoup

user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36"

headers = {"User-Agent" : user_agent}
response = requests.get("https://comic.naver.com/webtoon/weekday", headers)
response.raise_for_status()

soup = BeautifulSoup(response.text, 'lxml')
```
→ 웹에서 데이터를 받아 soup를 만든다.
```python
titles = soup.select('a.title')
for title in titles:
    print(title.text)
```
→ a 태그의 title 클래스 전부를 titles 에 담는다. 그리고 반복문을 사용해서 titles의 값을 title에 담고, title.text를 출력하면 연재중인 모든 웹툰의 제목이 나온다.   
