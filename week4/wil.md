# Week4 WIL
## 1. 데이터베이스의 개념과 종류
### 데이터베이스의 개념
- 데이터베이스(Database)는 데이터의 집합으로, 여러 사람이 공유하며 사용할 수 있도록 체계적으로 관리되는 데이터 저장소이다. 
- 데이터베이스는 데이터를 구조적으로 저장하고, 효율적으로 접근하며 관리하는 데 도움을 준다. 이를 통해 데이터의 무결성, 일관성, 보안성을 유지할 수 있다.
### 데이터베이스의 종류
1. **관계형 데이터베이스(RDBMS: Relational Database Management System)**  
   데이터를 테이블의 형태로 저장하고, 각 테이블은 열(Column)과 행(Row)으로 구성된다. SQL(Structured Query Language)을 사용해 데이터를 조작한다.
   - 예: MySQL, PostgreSQL, Oracle, MS SQL Server
2. **비관계형 데이터베이스(NoSQL: Not Only SQL)**  
   정형화된 테이블 구조 대신 문서, 키-값, 그래프 등 다양한 형태로 데이터를 저장한다. 대용량 데이터 처리 및 분산 환경에서 유연하게 확장 가능하다는 장점이 있다.
   - 예: MongoDB, Redis, Cassandra

## 2. RDBMS의 특성
### RDBMS(Relational Database Management System) 특성
1. **ACID 특성**
   - **Atomicity(원자성)**: 트랜잭션이 모두 완료되거나 전혀 실행되지 않는 것을 보장
   - **Consistency(일관성)**: 트랜잭션 전후에 데이터베이스가 일관성 있는 상태를 유지하도록 보장
   - **Isolation(격리성)**: 동시에 실행되는 트랜잭션들이 서로에게 영향을 미치지 않도록 함
   - **Durability(지속성)**: 트랜잭션이 완료되면 그 결과가 영구적으로 저장
2. **데이터의 정규화**: 데이터를 중복 없이 효율적으로 저장하기 위해 데이터베이스 테이블을 분리하는 과정입니다. 이를 통해 데이터의 무결성을 유지하고, 데이터 중복을 방지할 수 있음
3. **SQL 사용**: SQL을 사용해 데이터를 조회, 삽입, 수정, 삭제하는 등 다양한 작업을 수행
4. **관계성**: 테이블 간의 관계를 정의하여, 여러 테이블에 분산된 데이터를 연결할 수 있습니다. 외래 키(Foreign Key)를 사용해 테이블 간의 관계를 정의

## 3. 장고 Model과 사용법
### 장고 Model의 개념
장고(Django)에서 모델(Model)은 데이터베이스의 구조를 정의하는 클래스이다. 장고의 ORM(Object-Relational Mapping)을 통해 SQL을 작성하지 않고도 파이썬 코드로 데이터베이스를 다룰 수 있다.
### 장고 Model 사용법
1. **모델 정의**: `models.Model` 클래스를 상속받아 데이터베이스 테이블에 대응하는 모델을 정의한다. 각 필드는 데이터베이스 컬럼에 해당한다.
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
3. **모델 필드 타입**: 장고에서는 다양한 필드 타입을 지원한다. 예를 들어, `CharField`, `TextField`, `DateField`, 등이 있다.
4. **모델 메소드**: 모델 클래스에 커스텀 메소드를 정의해 더 복잡한 로직을 추가할 수 있다