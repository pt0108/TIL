> 부트캠프 18주차 2023년 2월 13일 ~ 15일

장고(Django)는 파이썬으로 만드는 **백엔드 프레임워크**이다.

→ [장고란 무엇인가요?](https://tutorial.djangogirls.org/ko/django/)

[Django](https://docs.djangoproject.com/ko/4.1/howto/custom-model-fields/#introduction)

### 설치 / 환경설정

1. django라는 이름의 가상환경 만들기
    
    ```python
    $ conda create --name django python=3.9
    $ conda activate django
    ```
    
2. django 설치 후 버전 확인
    
    ```python
    $ pip install django
    $ python -m django --version # 4.1.6
    ```
    
3. 깃허브 저장소 연동
    
    ```python
    $ git init
    $ git remote add origin (url 주소)
    $ git remote -v # 저장소와 연동이 잘 되어있는지 확인
    $ git pull origin main
    $ git branch -M main
    $ git add .
    $ git commit -m "include hello.txt"
    $ git status
    $ git push -u origin main
    ```
    
4. 생성 & 실행
    
    ```python
    django-admin startproject (프로젝트명) .
    python manage.py runserver
    ```
    
    실행이 잘 되었다면, 아래와 같은 페이지가 뜨는 것을 확인할 수 있다!
    
    ![image](https://user-images.githubusercontent.com/106129152/218962502-bab20ef5-8aca-4364-bf7b-060c9a200c4d.png)
    
5. DB에 관리자 계정 생성
    
    ```python
    python manage.py migrate
    python manage.py createsuperuser # id admin, pw 1234 임시 설정
    ```
    
    이렇게 설정을 한 후, `manage.py`를 실행했을 때 주는 주소의 /admin 으로 접속하면 로그인 페이지가 뜬다. 성공적으로 로그인을 하면 아래와 같은 페이지가 뜬다!
    
    ![image](https://user-images.githubusercontent.com/106129152/218962542-26e95e83-3b3f-4b24-96c4-639de6b1677e.png)
    
    여기서 후에 업데이트마다 git push를 할 때, 중요한 데이터나 private한 것들은 `.gitignore`으로 설정해둬야한다!
    
    ![image](https://user-images.githubusercontent.com/106129152/218962610-f7c85701-a310-4e68-90b4-882a8b513550.png)
    
6. 앱 생성
    
    ```python
    python manage.py startapp blog
    python manage.py startapp board
    ```
    
    ![image](https://user-images.githubusercontent.com/106129152/218962814-52084597-81eb-40c7-b7fa-483a6c030c4d.png)
    
7. Migrations
    
    ```python
    # board/models.py
    from django.db import models
    
    # Create your models here.
    # models모듈의 Model 클래스를 상속받는 자식클래스 생성
    class Post(models.Model): 
        title = models.CharField(max_length=50)
        content = models.TextField()
        created_at = models.DateTimeField(auto_now_add=True)
    		updated_at = models.DateTimeField(auto_now=True)
        # 작성자 나중에 추가 작성 예정
    ```
    
    마이그레이션을 등록하기 전에 먼저 `settings.py`에 앱을 등록해야 적용이 된다.
    
    ```python
    # django_project/settings.py : django_project 폴더가 몸체
    # 다른 앱들을 만들고 나면 django_project에 등록 필요
    INSTALLED_APPS = [
        "django.contrib.admin",
        "django.contrib.auth",
        "django.contrib.contenttypes",
        "django.contrib.sessions",
        "django.contrib.messages",
        "django.contrib.staticfiles",
        "blog",	
    ]
    ```
    
    ```python
    $ python [manage.py](http://manage.py/) makemigrations  # 마이그레이션할 내용 기록
    $ python manage.py migrate # 등록
    ```
    
    ### 장고 한글 문서
    
    [Django](https://docs.djangoproject.com/ko/4.1/)
    
    ### 템플릿 사이트
    
    [Free Bootstrap Templates](https://startbootstrap.com/templates)
    
    부트스트랩에서 템플릿을 가져오고, 장고 백엔드에서 작업한 내용들을 연결해주는 작업을 했다.
    
    네비게이션바나 푸터 같이 변동사항이 없는 요소들은, 기본틀이라는 느낌으로 조각조각 분리해서 base.html에 연결해주었다. 
    
    ![image](https://user-images.githubusercontent.com/106129152/218962715-8fd9adfa-1dce-44e8-b9be-5e4d1946ee00.png)
    
    ### 명령어
    
    `python manage.py shell` 로 파이썬 인터프리터를 사용할 수 있다.
    
    ```python
    # shell에서 확인해볼 내용
    from 앱.models import 클래스명 
    >>> from blog.models import Post
    
    # 이렇게 뜨면 데이터베이스가 연결이 된겁니다
    #  모델 이름. 오브젝트. 올()
    >>> Post.objects.all()
    <QuerySet []>
    
    # Create
    p1 = Post() # 빈 객체 만들고 속성 따로 넣기
    p2 = Post(title="Second", content="Django")
    # 인스턴스명.save()
    
    Post.objects.create(title="Third", content="django")
    # 저장까지 바로 됨 -> commit까지 완료해주는 Create명령어
    
    # Read
    # 전부다 가져오기
    Post.objects.all()
    
    # 특정조건에 맞춰서 가져오기
    # SELECT * FROM blog_post WHERE id=3;
    Post.objects.filter(조건) 
    Post.objects.get(조건)
    
    # 제목에 '글'이 들어간 포스트 찾기
    # SELECT * FROM blog_post WHERE title LIKE '%글%';
    Post.objects.filter(title__contains='글')
    Post.objects.filter(title__icontains='글')
    
    # 영어로 된 텍스트를 찾을때는 대문자, 소문자 구분 필요
    # contains 대소문자 구분 - SQLITE3에서는 둘다 대소문자 구분안함 -> 원래 DB의 차이 때문
    Post.objects.filter(title__contains='Third') 
    # icontains 대소문자 구분안함
    Post.objects.filter(title__icontains='Third')
    # 꼭 그 문자열을 검색해주는 메소드
    Post.objects.filter(title__exact='Third')
    ```
    
    ```python
    # 해당 검색 결과의 0번 인덱스만 가져옴
    Post.objects.get(title__exact='Third')
    
    # 해당 검색 결과 Object 전체를 가지고 와서 첫번째 객체만 가져오는 방식으로 해결
    Post.objects.filter(title__exact='Third').first()
    
    # 파이썬의 자료형에 따라 상속받은 함수를 사용하는 것이기 때문에 
    # int 형의 경우 gt(greater than), gte, lt(less than), lte 등의 메소드도 사용
    Post.objects.filter(id__gt=3)
    
    # 다중 조건으로 게시글만 가져오기 
    Post.objects.filter(id__in=[3, 6, 9])
    Post.objects.filter(content__in=['Django', 'django', 'jango'])
    
    # Django ORM이 어떤 식으로 SQL문을 만들었는지는 str(객체명.query)를 통해 확인가능
    query = Post.objects.filter(id__gt=3)
    str(query.query)
    
    # 정렬하기: SELECT * FROM Post ORDER BY(created_at)
    Post.objects.all().order_by('created_at')
    
    # 평균, 최소, 최대, 합계
    # View 테이블에 아래와 같이 import Code를 넣어 주고 작성
    from django.db.models import Avg, Max, Min, Sum
    -- SELECT COUNT(PROCESS) FROM POST GROUP BY PROCESS
      
    Post.objects.all().aggregate(Avg('id')) #평균
    Post.objects.all().aggregate(Min('id')) #최소
    Post.objects.all().aggregate(Max('id')) #최대
    Post.objects.all().aggregate(Sum('id')) #합계
    
    # 전체 개수를 확인 
    Post.objects.all().count()
    
    # Update
    # 1) save() 사용 - get
    p3 = Post.objects.get(id=4)
    p3.title = '제목 변경'
    p3.save()
    
    # 2) QuerySet.update() 사용 - create() 처럼 즉시 로딩
    Post.objects.filter(id=4).update(title='제목 2차 변경')
    # 여러개 객체의 내용을 모두 변경 가능
    Post.objects.filter(id__lte=4).update(content='내용 모두 변경')
    
    # 3) QuerySet.bulk_update() 사용 - 여러개의 객체를 완전히 같지 않은 방식으로 변경 가능
    # 다만 즉시로딩이므로 사용에 주의
    posts = Post.objects.all()
    for i, post in enumerate(posts):
        post.content = f"{i} - 내용 각기 변경"
    
    Post.objects.bulk_update(posts, ["content"])
    
    # Delete
    p3.delete()
    Post.objects.filter(id__lte=4).delete()
    ```
    
    새 포스트를 3개 작성
    
    - 제목1 Django
    - 제목2 django
    - 제목3 jango
    
    → Post 안에 넣고 서버를 실행하여 post_list.html에 해당 글이 올라오는지 확인
    
    ```python
    from blog.models import Post
    >>> Post.objects.create(title='제목1', content='Django')
    >>> Post.objects.create(title='제목2', content='django')
    >>> Post.objects.create(title='제목3', content='jango')
    ```
    
    헤더 이미지가 없을 경우 발생하는는 에러를 header_img.url 부분에 조건문을 활용하여 처리
    
    ```html
    {% if post.header_img %}
    <div class="col-lg-6 col-xl-7">
    	<div class="bg-featured-blog" style="background-image: url('{{ post_list.first.header_img.url }}')">
    	</div>
    </div>
    {% endif %}
    <!-- 아무것도 적지 않음으로 이미지를 출력하지 않음! --!>
    ```
    
    오늘 마지막 실습시간까지 포함해서 about 페이지까지 구현해보았다.
