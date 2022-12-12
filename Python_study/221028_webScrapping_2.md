> 부트캠프 2주차 2022년 10월 28일

## 웹 스크래핑 응용(2)
*10/27의 응용 파트 이어서 계속!*   

```python
import requests
from bs4 import BeautifulSoup

user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36"

headers = {"User-Agent" : user_agent}
response = requests.get("https://comic.naver.com/webtoon/weekday", headers)
response.raise_for_status()

soup = BeautifulSoup(response.text, 'lxml')

# 인기 급상승 웹툰 10위 목록 뽑아오기
ranks = soup.select('ol#realTimeRankFavorite>li>a')
for rank in ranks:
    print(rank.text)

'''
외모지상주의-415화 빅딜 잡기 [05]
나 혼자 만렙 뉴비-66화. 각자의 일상
광마회귀-61화
갓 오브 하이스쿨-569화-마지막화
어쩌다보니 천생연분-38화 개미와 베짱이
역대급 영지 설계사-65화
개를 낳았다-시즌2 120화
1초-177화 도화선
대학원 탈출일지-69화-임시 사수(2)
데드퀸-111화
'''
```
→ Select 메서드로 CSS 선택자를 사용해 간단하게 목록을 뽑아올 수 있다!    

- ***마루는 강쥐*의 제목과 링크, 평균 평점 가져오기**
    - 한 페이지 데이터 파싱
```python
url = "https://comic.naver.com/webtoon/list?titleId=796152&weekday=tue"

user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36"

headers = {"User-Agent" : user_agent}
response = requests.get(url, headers)
response.raise_for_status()

soup = BeautifulSoup(response.text, 'lxml')
```
find 사용의 경우 :
```python
# 제목, 링크
tds = soup.find_all('td', {'class':'title'})
for td in tds:
    a = td.find('a')
    print(a.get_text())
    print('https://comic.naver.com'+a['href'])

# 평균 평점
divs = soup.find_all('div', {'class':'rating_type'})
total_rate = 0
for div in divs:
    strong = div.find('strong')
    rate = float(strong.text)
    total_rate += rate
print("\n평균 평점 : ", total_rate/len(divs))
```
select 사용의 경우 :
```python
a_s = soup.select('td.title a')
strongs = soup.select('div.rating_type strong')
total_rate = 0

for a, strong in zip(a_s, strongs): # a_s : 제목, 링크, 평점
    title = a.text
    link = a['href']
    print(title)
    print("https://comic.naver.com"+link)
    rate = float(strong.text)
    total_rate += rate
    
print("\n평균 평점 : ", total_rate/len(divs))
```
      
여러 페이지 데이터 파싱
```python
for page in (1, 2): # 이 웹툰은 2페이지까지만 있어서 이렇게 했지만, 그 이상일 경우 range를 사용!
    url = "https://comic.naver.com/webtoon/list?titleId=796152&weekday=tue&page={}".format(page)
    user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36"

    headers = {"User-Agent" : user_agent}
    response = requests.get(url, headers)
    response.raise_for_status()

    soup = BeautifulSoup(response.text, 'lxml')
    
    # select 사용
    a_s = soup.select('td.title a')
    strongs = soup.select('div.rating_type strong')
    total_rate = 0

    for a, strong in zip(a_s, strongs): # a_s : 제목, 링크, 평점
        title = a.text
        link = a['href']
        print(title)
        print("https://comic.naver.com"+link)
        rate = float(strong.text)
        total_rate += rate

    print("{} page".format(page))
    print("\n평균 평점 : ", total_rate/len(strongs),"\n")
    print('*'*100,'\n')
```
   
- **다음(daum.net)에서 2021년 영화순위 검색**
    
1. 2021년도의 이미지 링크를 출력
```python
url = "https://search.daum.net/search?w=tot&q=2021%EB%85%84%EC%98%81%ED%99%94%EC%88%9C%EC%9C%84&DA=MOR&rtmaxcoll=MOR"

user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36"

headers = {"User-Agent" : user_agent}
response = requests.get(url, headers)
response.raise_for_status()

soup = BeautifulSoup(response.text, 'lxml')

imgs = soup.select('#morColl .mg_cont .wrap_thumb img.thumb_img')
for img in imgs:
    link = img['src']
    print(link)
```
   
2. 2021년 ~ 2011년도까지의 이미지 링크 출력
```python
for page in range(2021, 2010, -1):
    url = "https://search.daum.net/search?w=tot&q={}%EB%85%84%EC%98%81%ED%99%94%EC%88%9C%EC%9C%84&DA=MOR&rtmaxcoll=MOR".format(page)
    user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36"

    headers = {"User-Agent" : user_agent}
    response = requests.get(url, headers)
    response.raise_for_status()

    soup = BeautifulSoup(response.text, 'lxml')
    
    imgs = soup.select('#morColl .mg_cont .wrap_thumb img.thumb_img')
    
    print("20{}년".format(page))
    for img in imgs:
        link = img['src']
        print(link)
```
   
3. 해당 링크 이미지를 요청해서 파일로 저장 
```python
for page in range(2021, 2010, -1):
    url = "https://search.daum.net/search?w=tot&q={}%EB%85%84%EC%98%81%ED%99%94%EC%88%9C%EC%9C%84&DA=MOR&rtmaxcoll=MOR".format(page)
    user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36"

    headers = {"User-Agent" : user_agent}
    response = requests.get(url, headers)
    response.raise_for_status()

    soup = BeautifulSoup(response.text, 'lxml')
    
    imgs = soup.select('#morColl .mg_cont .wrap_thumb img.thumb_img')
    
    for i, img in enumerate(imgs): # 30장의 imgs 
        link = img['src']
        img_res = requests.get(link, headers)
        response.raise_for_status()
        
        with open('./imgs/{}_movie_rank{}.jpg'.format(page, i+1),'wb') as fd:
            fd.write(img_res.content)
```
   
## 셀레니움
***웹페이지 테스트 자동화를 할 수 있는 프레임워크***

셀레니움 사용시 완전한 형태의 웹 페이지 소스를 볼 수 있기 때문에 스크래핑할 때 유용하다.

***→ 정말 정리가 잘된 사이트 : [Python Slenium 사용법](https://greeksharifa.github.io/references/2020/10/30/python-selenium-usage/)***

**<사용 예>**

자바 스크립트가 동적으로 만든 데이터를 스크래핑할 때

사이트의 다양한 HTML 요소에 클릭, 키보드 입력 등 이벤트를 줄 때

**<사용 방법>**

셀레니움을 사용하려면 사용중인 웹 브라우저의 드라이버 파일을 다운로드해야한다. 

우선, chrome://version/ 에서 크롬 버전을 확인하고, [이곳](https://chromedriver.chromium.org/downloads)에서 크롬 버전와 운영체제에 맞는 드라이버를 다운로드 한다. 드라이버의 압축을 푼 뒤 exe 파일을 현재 작업 디렉토리에 카피한다.

- **Selenium 설치**
    
    아나콘다로 예를 들면, 아나콘다 프롬프트를 실행한 후
    
    `conda install selenium` 를 입력해서 설치하면 된다.
    

*참고 → [https://www.selenium.dev/documentation/webdriver](https://www.selenium.dev/documentation/webdriver)*

   
![image](https://user-images.githubusercontent.com/106129152/200752653-4afbc8cd-5bea-4321-9ab0-a40bc1ead434.png)
```python
import selenium
from selenium import webdriver
```
간단하게 몇 가지 작동 예시를 보자면
```python
driver = webdriver.Chrome() # driver가 있는 path를 넣어줄 수 있음

driver.get("http://naver.com") # naver 실행
driver.back() # 뒤로 가기
driver.forward() # 앞으로 가기
driver.refresh() # 새로고침
driver.close() # browser 종료
driver.quit() # browser, driver 종료
```
   
- Element를 찾는데 필요한 함수들
```pyhon
from selenium.webdriver.common.keys import Keys

driver = webdriver.Chrome()
driver.get("http://naver.com")
elem = driver.find_element_by_id('query')
elem.send_keys("파이썬")
elem.send_keys(Keys.ENTER)
```
→ 크롬 브라우저 실행 > naver.com 접속 > 검색창에 “파이썬” 입력 > ENTER 실행   
   
find_element_by_tag_name
```python
# find_element_by_tag_name 을 통해 a tag에 접근
# href 정보까지도 조회

elem = driver.find_element_by_tag_name('a')
elem.get_attribute('href')
```
   
find_elements_by_tag_name
```python
# 여러 tag를 가져올 때는 find_elements_by_tag_name

elems = driver.find_elements_by_tag_name('a')
for elem in elems:
    print(elem.get_attribute('href'))
```
   
find_element_by_name
```python
driver = webdriver.Chrome()
driver.get("http://naver.com")

elem = driver.find_element_by_name('query')
elem.send_keys("파이썬")

elem = driver.find_element_by_id('search_btn')
elem.click()

driver.back()

elem = driver.find_element_by_name('query')
elem.send_keys("파이썬")
```
   
find_element_by_xpath
```python
elem = driver.find_element_by_xpath('//*[@id="search_btn"]')
elem.click()
```
→ xpath는 개발자 도구에서 원하는 요소를 우클릭하면 copy할 수 있다.   

## 셀레니움 Workshop
***Workshop 1***

네이버 로그인
```python
import time

options = webdriver.ChromeOptions()
options.add_argument('user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36')

driver = webdriver.Chrome(options=options)

# 네이버 사이트 이동
driver.get("http://naver.com")

# 로그인 버튼
elem = driver.find_element_by_css_selector('a.link_login')
elem.click()

# id/pw 입력
elem = driver.find_element_by_id('id')
elem.send_keys("xxxx")
time.sleep(2)

elem = driver.find_element_by_id('pw')
elem.send_keys("yyyy")
time.sleep(1)

#로그인 버튼
elem = driver.find_element_by_id("log.login")
elem.click()

# 종료
driver.quit()
```
   
***Workshop 2***

구글 이미지 검색
```python
options = webdriver.ChromeOptions()
options.add_argument('user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36')

driver = webdriver.Chrome(options=options)

# 구글 이미지검색 사이트 이동
driver.get("https://www.google.co.kr/imghp?hl=ko&tab=ri&ogbl")

# 검색
keyword = '딸기'
elem = driver.find_element_by_name('q')
elem.send_keys(keyword)
elem.submit() # elem.send_keys(Keys.ENTER) 와 동일

# 작은 이미지 클릭
image_elem= driver.find_element_by_css_selector('img.rg_i.Q4LuWd')
image_elem.click()

# 오른쪽에 있는 큰 이미지의 주소를 획득
image_elem = driver.find_element_by_xpath('//*[@id="Sva75c"]/div/div/div[3]/div[2]/c-wiz/div/div[1]/div[1]/div[3]/div/a/img')
image_url = image_elem.get_attribute('src')
print(image_url)

# 이미지 주소로 request 해서 응답받은 이미지를 저장
import requests

user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36 Edg/106.0.1370.47"

headers = {"User-Agent" : user_agent}
response = requests.get(image_url, headers)
response.raise_for_status()

with open('./strawberry/1.jpg', 'wb') as fd:
            fd.write(response.content)

# 종료
driver.quit()
```
## 셀레니움 Workshop(2) - *(10/31 학습 내용)*

- 이미지 여러장 저장
```python
import selenium
from selenium import webdriver
import time
```
```python
options = webdriver.ChromeOptions()
options.add_argument('user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36')

driver = webdriver.Chrome(options=options)

# 구글 이미지검색 사이트 이동
driver.get("https://www.google.co.kr/imghp?hl=ko&tab=ri&ogbl")

# 검색
keyword = '감자'
elem = driver.find_element_by_name('q')
elem.send_keys(keyword)
elem.submit() # elem.send_keys(Keys.ENTER) 와 동일

# 작은 이미지 클릭
image_elems= driver.find_elements_by_css_selector('img.rg_i.Q4LuWd')

count = 1
for image_elem in image_elems:
    image_elem.click()
    time.sleep(2)

    # 오른쪽에 있는 큰 이미지의 주소를 획득
    image_elem = driver.find_element_by_xpath('//*[@id="Sva75c"]/div/div/div[3]/div[2]/c-wiz/div/div[1]/div[1]/div[3]/div/a/img')
    image_url = image_elem.get_attribute('src')
    print(image_url)

    # 이미지 주소로 request 해서 응답받은 이미지를 저장
    import requests

    user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36 Edg/106.0.1370.47"

    headers = {"User-Agent" : user_agent}
    response = requests.get(image_url, headers)
    response.raise_for_status()

    with open('./potato/{}.jpg'.format(count), 'wb') as fd:
                fd.write(response.content)
    count += 1
    if count > 10:
        break

# 종료
driver.quit()
```
- 사용자의 Scroll 반영
```python
options = webdriver.ChromeOptions()
options.add_argument('user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36')

driver = webdriver.Chrome(options=options)

# 구글 이미지검색 사이트 이동
driver.get("https://www.google.co.kr/imghp?hl=ko&tab=ri&ogbl")

# 검색
keyword = '감자'
elem = driver.find_element_by_name('q')
elem.send_keys(keyword)
elem.submit() # elem.send_keys(Keys.ENTER) 와 동일

# Java Script의 Scroll 기능을 통해서 더 많은 이미지 로딩
prev_height = driver.execute_script('return document.body.scrollHeight')
print(prev_height)

while True:
    driver.execute_script('window.scrollTo(0, document.body.scrollHeight)') 
    time.sleep(1)
    curr_height = driver.execute_script('return document.body.scrollHeight')
    print(curr_height)
    if prev_height == curr_height:
        break
    prev_height = curr_height

# 작은 이미지 클릭
image_elems= driver.find_elements_by_css_selector('img.rg_i.Q4LuWd')

count = 1
for image_elem in image_elems:
    image_elem.click()
    time.sleep(2)

    # 오른쪽에 있는 큰 이미지의 주소를 획득
    image_elem = driver.find_element_by_xpath('//*[@id="Sva75c"]/div/div/div[3]/div[2]/c-wiz/div/div[1]/div[1]/div[3]/div/a/img')
    image_url = image_elem.get_attribute('src')
    print(image_url)

    # 이미지 주소로 request 해서 응답받은 이미지를 저장
    import requests

    user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36 Edg/106.0.1370.47"

    headers = {"User-Agent" : user_agent}
    response = requests.get(image_url, headers)
    response.raise_for_status()

    with open('./potato/{}.jpg'.format(count), 'wb') as fd:
                fd.write(response.content)
    count += 1
    if count > 30:
        break

# 종료
driver.quit()
```

## Workshop
### 구글 무비
[https://play.google.com/store/movies/top](https://play.google.com/store/movies/top)

스크롤된 모든 데이터에 대해 가격이 할인된 영화만 출력

출력 양식 : 영화제목, 할인전/후 가격, 링크
```python
# 1. 첫 화면 접속

options = webdriver.ChromeOptions()
options.add_argument('user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36')

driver = webdriver.Chrome(options=options)

driver.get("https://play.google.com/store/movies/top")

# 2. 페이지 스크롤
# Java Script의 Scroll 기능을 통해서 더 많은 이미지 로딩

prev_height = driver.execute_script('return document.body.scrollHeight')
print(prev_height)

while True:
    driver.execute_script('window.scrollTo(0, document.body.scrollHeight)') 
    time.sleep(1)
    curr_height = driver.execute_script('return document.body.scrollHeight')
    print(curr_height)
    if prev_height == curr_height:
        break
    prev_height = curr_height

# 3. 필요한 정보 가져오기 위해 구문 분석

soup = BeautifulSoup(driver.page_source, 'lxml')

# print(soup.prettify())

movies = soup.select('div.VfPpkd-EScbFb-JIbuQc.UVEnyf')

print(len(movies))

count = 0
for movie in movies:
    # 영화제목
    title = movie.select_one('div.Epkrse')
    title = title.text

    # 할인 전 가격
    original_price= movie.select_one('span.SUZt4c.P8AFK')
    if original_price: 
        original_price = original_price.text

    else: # 할인 전 가격이 없으면 세일하는 항목이 아님
        continue
        
    # 할인 후 가격
    discount_price= movie.select_one('span.VfPpfd.VixbEe')
    discount_price = discount_price.text


    # 링크 정보
    link = movie.select_one('a.Si6A0c.ZD8Cqc')
    link = 'https://play.google.com' + link['href']

    print('제목 : ', title)
    print('할인 전 가격 : ', original_price)
    print('할인 후 가격 : ', discount_price)
    print('링크 : ', link)
    print('-'*100)
    count += 1
    
print(count)
```
→ 이런식으로 120개의 영화 중에서 할인 중인 영화 24개의 정보만 출력되었다.
