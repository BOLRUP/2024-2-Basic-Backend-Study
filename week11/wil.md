# Week11 WIL
## 1. FK(Foreign Key)란?
- **외래 키(Foreign Key)**는 한 테이블의 특정 필드가 다른 테이블의 기본 키(Primary Key)를 참조할 때 사용된다.
- 테이블 간의 관계를 정의하며, 데이터 무결성을 유지하는 데 도움을 준다.
- 장고에서는 `models.ForeignKey`를 사용해 외래 키를 설정한다.
---
## 2. 관계 유형 및 테이블 구현 방법
### **1. 일대일 관계 (One-to-One)**
- **특징**: 한 테이블의 각 행이 다른 테이블의 정확히 한 행과 연결된다.
- **예시**: 학생과 사물함 관계 (학생 한 명당 사물함 하나 배정).
- **장고 모델 구현**:
  ```python
  class Locker(models.Model):
      student = models.ForignKey(Student, on_delete = models.CASCADE, unique = True)
      number = models.CharField(max_length=3)
  ```
  ```python
  class Locker(models.Model):
      student = models.OneToOneField(Student)
      number = models.CharField(max_length=3)
  ```
---
### **2. 일대다 관계 (One-to-Many)**

- **특징**: 한 테이블의 한 행이 다른 테이블의 여러 행과 연결된다.
- **예시**: 질문과 답변의 관계 (질문 하나에 여러 답변이 연결).
- **장고 모델 구현**:
  ```python
  class Answer(models.Model):
      question = models.ForeignKey(Question, on_delete=models.CASCADE)
      content = models.TextField()
      create_date = models.DateTimeField()
  ```
---
### **3. 다대다 관계 (Many-to-Many)**
- **특징**: 한 테이블의 여러 행이 다른 테이블의 여러 행과 연결된다.
- **예시**: 학생과 강의 관계 (학생은 여러 강의를 들을 수 있고, 강의는 여러 학생을 가질 수 있음).
- **장고 모델 구현**:
  ```python
  class Class(models.Model):
      name = models.CharField(max_length=30)
      professer = models.CharField(max_length=20)
      students = models.ManyToManyField(Student)
  ```
---
### 요약
- **일대일 관계**: `OneToOneField`를 사용
- **일대다 관계**: `ForeignKey`를 사용해 관계 설정
- **다대다 관계**: `ManyToManyField`를 사용해 연결
- **`on_delete` 옵션**:
  - **`CASCADE`**: 참조된 객체가 삭제되면 연결된 객체도 삭제
  - **`PROTECT`**: 참조된 객체가 삭제되지 않도록 보호
  - **`SET_NULL`**: 참조된 객체가 삭제되면 `NULL`로 설정
  - **`DO_NOTHING`**: 아무 행동도 취하지 않음