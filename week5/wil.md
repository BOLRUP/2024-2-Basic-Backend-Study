# Week5 WIL
## 1. 장고 Model과 ORM
### 장고 Model로 테이블 만드는 방법
장고에서 테이블을 만들려면 모델 클래스를 정의하고 이를 마이그레이션(migration)하여 데이터베이스에 반영한다.
1. **모델 클래스 정의**  
   `models.Model`을 상속받아 모델 클래스를 정의한다. 클래스의 각 필드는 데이터베이스 컬럼에 매핑된다.
   ```python
   from django.db import models

   class Student(models.Model):
       id = models.CharField(max_length=7)
       name = models.CharField(max_length=20)
       address = models.TextField()
       birth_date = models.DateField()
   ```
2. **마이그레이션**: 모델을 정의한 후, 이를 데이터베이스에 반영하기 위해 마이그레이션 명령어를 실행한다.
   - `python manage.py makemigrations`: 모델 변경 사항을 기록
   - `python manage.py migrate`: 마이그레이션을 데이터베이스에 적용
---
### 장고 ORM 메서드들의 기능 정리
장고 ORM(Object-Relational Mapping)은 SQL을 작성하지 않고도 데이터베이스와 상호작용할 수 있게 한다.
1. **`Class.objects.get()`**
   - 단일 객체를 조회할 때 사용하며, 조회 조건을 만족하는 객체가 없거나 두 개 이상일 경우 오류 발생
   ```python
   student = Student.objects.get(id="C111xxx")
   ```
2. **`Class.objects.all()`**
   - 모든 객체를 조회하여 QuerySet으로 반환
   ```python
   students = Student.objects.all()
    ```
3. **`Class.objects.filter()`**
   - 특정 조건을 만족하는 객체들만 조회하여 QuerySet으로 반환합니다.
   ```python
   students = Student.objects.filter(address__contains= '마포구')
   ```
---
## 2. 자주 쓰이는 HTML 태그 정리
- **`<h1>` / `<h2>` / `<h3>`**: 제목을 생성하는 태그로, 숫자가 작을수록 폰트 크기가 크다
- **`<p>`**: 문단을 생성해 텍스트 단락을 만든다
- **`<a href="URL">`**: 하이퍼링크 태그로, `href` 속성에 링크 주소를 넣어 클릭 시 이동할 페이지를 지정한다
- **`<ul>` / `<ol>`**: 목록 태그로, `<ul>`은 순서 없는 목록, `<ol>`은 순서 있는 목록이다. 각 항목은 `<li>`로 감싼다
- **`<div>`**: 레이아웃을 나누기 위해 사용하는 태그로, CSS와 함께 사용된다
- **`<form>` / `<input>`**: 데이터를 입력받고 전송하는 태그다
---
## 3. 장고 Template 문법
장고 템플릿은 HTML 파일에서 동적 컨텐츠를 렌더링하기 위한 문법을 제공한다
1. **변수 출력**  
   파이썬 변수를 출력하려면 중괄호 두 개(`{{ }}`)로 감싼다
   ```html
   <p>Hello, {{ name }}!</p>
   ```
2. **조건문**  
   `{% if %}`와 `{% endif %}`를 사용해 조건에 따라 HTML을 출력한다
   ```html
    {% if student %}
    <p>{{student.name}}</p>
    {% endif %}
   ```
3. **반복문**  
   `{% for %}`와 `{% endfor %}`를 사용해 리스트의 각 항목을 출력할 수 있다
   ```html
    <ol>
    {% for student in student_list %}
        <li>{{student.name}}</li>
    {% endfor %}
    </ol>
   ```