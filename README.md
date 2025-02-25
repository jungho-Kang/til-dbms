# 데이터베이스 모델링 및 ERD 및 MySQL 활용하기

- MySQL (DBMS 8.x)
  - RDBMS를 다룬다 (Relation : 관계)

## 1. 요구사항 분석

- 회의 참석 (회의록)
- 회의록 검토 후 각 사항을 요구사항 분석 (요구사항 정의서, 업무 지시서)

## 2. 요구사항 분석을 하는 이유

- 각 내용의 속성을 찾고 분류
- 분류된 내용을 모아서 Entity 생성
- Entity 사이의 관계를 찾는다
- 요구사항 정의서 작성

### 2.1. 요구사항 분석 예

- 고객은 고객코드, 고객명, 전화번호, 이메일, 주소(기본주소, 상세주소), 지역, 가입일로 되어있다
- 고객은 지역별로 관리되도록 한다
- 지역은 지역코드와 지역명으로 되어 있고 지역명은 대한민국의 지역코드 (02:서울특별시)를 이용한다
- 한 지역에는 여러 고객이 있을 수 있다
- 제품은 제품코드, 제품명, 제품색상, 가격으로 되어있다
- 하나의 제품은 여러 색상을 가질 수가 있다
- 고객은 등록된 제품을 구매 할 수 있다
- 한 명의 고객은 여러 제품을 구매 할 수 있고, 하나의 제품은 여러 고객이 구매 할 수 있다
- 고객이 제품을 구매 시 구매수량과 구매일자를 기록한다

### 2.2. 요구사항 정의서 또는 업무 기술서 (회사마다 포맷이 다르다)

![Image](https://github.com/user-attachments/assets/06dae24b-8245-4b54-ad06-1e8b3642d36f)

### 2.3. 속성(Attribute) 찾기 후 Entity 정의하기

- DB 설계 전문가는 Entity 정의 후 속성을 선별해 나간다
- 신입 DB 설계자는 Attribute 선별 후 Entity를 정의함

#### 2.3.1. 먼저 Entity 항목정리

- 명사 소문자 추천

![Image](https://github.com/user-attachments/assets/8f911e14-740f-4367-a86e-7c47f1c12f14)

#### 2.3.2. Entity 사이의 관계정리

- 동사 소문자 추천

![Image](https://github.com/user-attachments/assets/76533446-4416-4d77-97ae-c8bb43cdb881)

## 3. ERD 그리기

### 3.1. 개념적 모델링

- E-R 다이어그램(Entity-Relationship-Diagram)
- https://app.diagrams.net/

![Image](https://github.com/user-attachments/assets/109183c8-ee0e-402b-9688-50b3e8db5d02)

- 고객

![Image](https://github.com/user-attachments/assets/f41b7fb7-64b9-4021-8055-7dc76a1fa495)

- 고객 PK 후보

![Image](https://github.com/user-attachments/assets/7f635a08-a141-480b-8200-af64e17c6263)

- 지역

![Image](https://github.com/user-attachments/assets/20041eaf-5eb6-4095-9a8f-82bfcb001bb8)

- 제품

![Image](https://github.com/user-attachments/assets/fd02f402-06cc-4070-880a-e37f5d5e15cd)

### 3.2. Relation 표현하기

- 개체와 개체가 맺고 있는 연관성을 표현

![Image](https://github.com/user-attachments/assets/d6cfe638-56ae-44aa-bb58-bf4282181965)

#### 고객은 제품을 구매한다

![Image](https://github.com/user-attachments/assets/9681cad5-2925-4dbe-83d5-5ac86455778c)
![Image](https://github.com/user-attachments/assets/94ddaaa1-1f6c-4fa7-b365-6e5defe6d76a)

## 4. Logical Data Modeling(논리적 모델링)

- 개념적 스키마를 표 형식 또는 테이블 형식으로 표현함
- Entity의 속성 데이터 타입, 길이, null 허용여부, 기본값, 제약 조건등을 세부적으로 작성 후 문서화
- 즉 `테이블정의서`를 생성함 (도구는 다양합니다)

![Image](https://github.com/user-attachments/assets/9cb8ee4e-bfb8-4c35-bb58-0ff55efee5b3)

## MySQL 설치

- https://dev.mysql.com/downloads/installer/
