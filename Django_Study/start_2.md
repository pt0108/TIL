> 부트캠프 18주차 2023년 2월 16일 ~ 17일

## 관계형 데이터베이스 구현

**Post 테이블**

| postId | author | 작성자명 | 제목 | 내용 | 작성일 | 첨부파일 | 헤더파일 | categoryId | tagId |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |

### 작성자와 글의 관계

- 작성자와 글은 별개의 테이블에서 관리된다.
- 한 명의 작성자는 여러 개의 글을 쓸 수 있으나, 한 개의 글은 여러 명의 작성자가 쓸 수 없다.

**현재 생성된 User 목록**

| userId | author | password | firstName | lastName | 가입일 | 최종 로그인 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | user | playdata1 | Lee | Jaeyoung | 2023/02/16 |  |
| 2 | jjanggu | playdata2 | 신 | 짱구 | 2023/02/16 |  |

이때, 작성자를 [외래키](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.ForeignKey)로 참조한다.

Foreignkey에는 꼭 `on_delete`가 들어가 있어야 한다. → [on_delete 종류](https://vallhalla-edition.tistory.com/60)

```python
# blog - models.py
from django.db import models
from django.contrib.auth.models import User

# CASCADE : User를 삭제하면 현재 테이블의 관련된 모든 데이터 삭제
# author = models.ForeignKey(User, on_delete=models.CASCADE) 

# SET_NULL : User를 삭제하면 모든 데이터는 남겨놓되 User 정보만 삭제
author = models.ForeignKey(User, on_delete=models.SET_NULL, null=True)
```

### 카테고리와 글의 관계

- 하나의 글은 여러 개의 카테고리를 가질 수 있음
- 카테고리는 각 글에 한번씩만 저장됨

![image](https://user-images.githubusercontent.com/106129152/219572791-de1b18f1-d1da-4dec-b3ce-aded93927fee.png)

Category는 장고에서 제공하지 않기 때문에 직접 만들어야 한다.

**카테고리 테이블**

| categoryId | categoryName |
| --- | --- |
| 1 | 경제 |
| 2 | 비즈니스 |
| 3 | 프로그래밍 |
| 4 | 문화 |
| 5 | 생산성 |

**카테고리 클래스 구현**

`SlugField` : url로 통신하는 Django의 통신방식에 걸맞게 입력한 값이 URL화 되도록 자동으로 변경

`allow_unicode=True` : 특수문자 에러처리, 한국어 등 영어 외의 언어도 사용 가능

`unique=True` : 전체 테이블의 해당 categoryName은 1개만 만들어지도록 구현

```python
# blog - models.py

class Category(models.Model):
    categoryName = models.CharField(max_length=30, unique=True) 
    slug = models.SlugField(max_length=30, unique=True, allow_unicode=True)

    def __str__(self):
        return self.name

    def get_absolute_url(self):
        return f'/blog/category/{self.slug}/'

    class Meta:
        verbose_name_plural = 'categories'
```

### 태그와 글의 관계

- 하나의 글은 여러개의 태그를 가짐
- 하나의 태그는 여러개의 글을 가짐
- 다대다 관계

**태그 테이블**

| tagId | tagName |
| --- | --- |
| 1 | PYTHON |
| 2 | DJANGO |

**포스트 태그 테이블**

| post_tag_id | postId | tagId |
| --- | --- | --- |
| 1 | 1 | 1 |
| 2 | 2 | 2 |
| 3 | 3 | 1 |

**태그 클래스 구현**

```python
# blog - models.py

class Tag(models.Model):
    tagName = models.CharField(max_length=30, unique=True) 
    slug = models.SlugField(max_length=30, unique=True, allow_unicode=True)

    def __str__(self):
        return self.tagName

    def get_absolute_url(self):
        return f'/blog/tag/{self.slug}/'
```

참고로, `admin.py`에 이렇게 클래스를 만들어줘야 admin 페이지에서 사용이 가능하다.

```python
# blog - admin.py

from django.contrib import admin
from .models import Post, Category, Tag  # 현재 경로의 models.py 안에 있는 Post를 가져다 쓰겠음 

# Register your models here.
admin.site.register(Post)

class CategoryAdmin(admin.ModelAdmin):
    prepopulated_fields = {'slug':('categoryName', )}

admin.site.register(Category, CategoryAdmin)

class TagAdmin(admin.ModelAdmin):
    prepopulated_fields = {'slug':('tagName', )}

admin.site.register(Tag, TagAdmin)
```

## 페이지네이션

이번에는 장고의 페이지네이션을 사용해보았다.

[Django](https://docs.djangoproject.com/ko/4.1/topics/pagination/#paginating-a-listview)

```python
# views.py
paginate_by = 5 # n개씩 잘라서 data(record)를 전송해주는 속성 (urls.py에서도 가능)
paginate_orphans = 3
```

페이지네이션을 사용하면 아래와 같이 페이지 기능을 사용할 수 있다.

![image](https://user-images.githubusercontent.com/106129152/219572883-4d8cbd7e-24a2-49c3-a52f-6d28d9354748.png)

```python
{% for contact in page_obj %}
    {# Each "contact" is a Contact model object. #}
    {{ contact.full_name|upper }}<br>
    ...
{% endfor %}

<div class="pagination">
    <span class="step-links">
        {% if page_obj.has_previous %}
            <a href="?page=1">&laquo; first</a>
            <a href="?page={{ page_obj.previous_page_number }}">previous</a>
        {% endif %}

        <span class="current">
            Page {{ page_obj.number }} of {{ page_obj.paginator.num_pages }}.
        </span>

        {% if page_obj.has_next %}
            <a href="?page={{ page_obj.next_page_number }}">next</a>
            <a href="?page={{ page_obj.paginator.num_pages }}">last &raquo;</a>
        {% endif %}
    </span>
</div>
```
