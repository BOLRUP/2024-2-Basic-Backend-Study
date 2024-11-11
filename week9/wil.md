# Week9 WIL
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
## 2. form 태그와 사용법
HTML의 `<form>` 태그는 사용자로부터 데이터를 입력받아 서버에 전송하는 역할을 한다.
### `<form>` 태그 사용법
1. **기본 구조**
   - `<form>` 태그는 여러 `<input>`, `<button>`, `<select>`, `<textarea>` 등의 태그로 구성되어 있다.
   ```html
   <form action="/questions/create" method="post">
    {% csrf_token %}
    <input name="subject" type="text" placeholder="제목" required></textarea>
    <input name="content" type="text" placeholder="내용" required></textarea>
    <button type="submit">등록</button>
   </form>
   ```
2. **주요 속성**
   - **action**: 폼이 전송될 URL을 지정한다.
   - **method**: 폼 데이터를 전송할 HTTP 메서드를 지정한다 (`GET` 또는 `POST`).
3. **CSRF 보호**
   - `{% csrf_token %}`: Django에서 POST 요청 시 CSRF(Cross-Site Request Forgery) 공격을 방지하기 위해 사용된다.
4. **전송 방식에 따른 동작**
   - **GET**: 폼 데이터를 URL의 쿼리 스트링으로 전송하며, 보통 조회용 폼에서 사용된다.
   - **POST**: 폼 데이터를 본문(body)에 담아 전송하며, 보안이 필요한 데이터 전송에 적합하다.
5. **input 태그 종류**
   - `<input name="subject">`: 제목 입력 필드
   - `<input name="content">`: 내용 입력 필드
   - `<button type="submit">`: 폼 데이터를 서버로 전송