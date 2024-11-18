# Week10 WIL
## 1. HTTP Method
HTTP 메서드는 클라이언트와 서버 간의 데이터를 전송하는 방식이다. 주요 메서드로는 `GET`, `POST`, `PUT`, `DELETE` 등이 있고, 각 메서드는 고유의 목적과 특성을 가지고 있다.
### GET 메서드의 특징
- **데이터 조회**: GET 메서드는 서버에서 데이터를 가져오는 데 사용된다. URL에 데이터를 포함해 요청하기 때문에, 보안이 필요한 데이터 전송에는 적합하지 않다.
- **URL에 데이터 포함**: 데이터를 쿼리 스트링으로 URL에 추가하고, 이는 주소창에 노출된다.
- **멱등성**: 동일한 요청을 여러 번 보내도 서버 상태는 변하지 않는다.
- **캐싱 가능**: GET 요청은 브라우저나 프록시 서버에서 캐싱할 수 있다.
- **주로 사용되는 상황**: 페이지를 로드하거나 특정 데이터를 조회할 때 사용된다.

예시:
```http
GET /questions/create?subject=질문3 HTTP/1.1
Host: localhost:8000
```
### POST 메서드의 특징
- **데이터 전송**: POST 메서드는 서버에 데이터를 전송하여 리소스를 생성하거나 업데이트할 때 사용된다. 폼 데이터를 서버에 전송하거나 파일 업로드를 할 때 자주 사용된다.
- **데이터가 URL에 포함되지 않음**: 데이터를 HTTP 요청 본문(body)에 포함하기 때문에 URL에 노출되지 않아 보안성이 좋다.
- **비멱등성**: 동일한 POST 요청을 반복하면 서버의 상태가 변경될 수 있다.
- **캐싱 불가능**: 기본적으로 POST 요청은 캐싱되지 않는다.
- **주로 사용되는 상황**: 사용자 정보 제출, 게시글 작성 등 데이터를 서버에 저장해야 할 때 사용된다.

예시:
```http
POST /questions/create HTTP/1.1
Host: macdonald:8000

subject=질문3
content=질문내용3
```
---
## 2. DB 내용을 수정, 삭제, 검색하는 방법
### **1. DB 내용 수정 (Update)**
1. **수정할 객체 가져오기**
   - 객체를 수정하려면 먼저 `get()` 또는 `filter()`로 해당 객체를 가져온다.
2. **필드 값 수정**
   - 객체의 필드를 업데이트한 후 `save()` 메서드를 호출해 변경 내용을 저장한다.
3. **예시 코드**
   ```python
   # 특정 객체 가져오기
   question = Question.objects.get(id=question_id)

   # 필드 값 수정
   question.subject = request.POST["subject"]
   question.content = request.POST["content"]

   # 저장
   question.save()
   ```
---
### **2. DB 내용 삭제 (Delete)**
1. **단일 객체 삭제**
   - 삭제할 객체를 가져온 뒤 `delete()` 메서드를 호출한다.
   ```python
   # 특정 객체 가져오기
   question = Question.objects.get(id=question_id)
   
   # 삭제
   question.delete()
   ```
---
### **3. DB 내용 검색 (Read)**
1. **단일 객체 검색**
   - `get()` 메서드를 사용해 특정 조건을 만족하는 단일 객체를 가져온다.
   - **주의**: 조건에 맞는 객체가 없거나 2개 이상이면 오류가 발생한다.
   ```python
   question = Question.objects.get(id=1)  # id가 1인 객체 검색
   ```
2. **여러 객체 검색**
   - `filter()` 메서드를 사용해 특정 조건을 만족하는 객체의 QuerySet을 가져온다.
   ```python
   questions = Question.objects.filter(subject="질문 1")  # 제목이 '질문 1'인 객체 검색
   ```
3. **조건 없는 모든 객체 검색**
   - `all()` 메서드를 사용하면 모든 객체를 QuerySet으로 반환한다.
   ```python
   questions = Question.objects.all()  # 모든 Question 객체 검색
   ```

4. **추가 검색 조건**
   - **`contains`**: 특정 문자열을 포함하는 객체 검색
     ```python
     Question.objects.filter(subject__contains="검색어")  # 제목에 '검색어' 포함
     ```
   - **`icontains`**: 대소문자를 구분하지 않고 특정 문자열 포함 여부 검색
     ```python
     Question.objects.filter(subject__icontains="검색어")  # 제목에 '검색어' 포함
     ```
5. **OR 조건 검색**
    - 여러 조건을 OR로 연결하려면 `Q` 객체와 `|` 연산자를 사용한다.
    - OR 조건으로 검색한 결과는 `distinct()`를 사용해 중복된 결과를 제거할 수 있다.
    ```python
    questions = (
    Question.objects.filter(subject__icontains=keyword) |
    Question.objects.filter(content__icontains=keyword)
    ).distinct()
    ```