---
categories: [Programmers, SQL, Oracle, Chat]
tags: [Programmers, SQL, Oracle, chat] 
---

## Sinagong
### book2

> 118-q3

```sql
CREATE TABLE patient (
    id VARCHAR(5) PRIMARY KEY,
    name VARCHAR(10),
    sex CHAR(1),
    phone VARCHAR(20),
    CONSTRAINT sex_ck CHECK(sex='f' or sex='m'),
    CONSTRAINT id_fk FOREIGN KEY(id) REFERENCES doctor(doc_id)
);
```

`sex  속성은 f 또는 m값만 갖도록 한다 (제약조건명: sec_ck)`
`id는 doctor 테치블에 있는 doc_id를 참조한다 (제약조건면: id_fk)`

> 118 q-4

```sql
CREATE TABLE Instrctor (
    id CHAR(5),
    name CHAR(10),
    dept CHAR(15)
    PRIMARY KEY(ID),
    FOREIGN KEY(dept) REFERENCES Department(name)
    ON DELETE SET NULL
    ON UPDATE CASCADE
);
```

`Department테이블에서 튜플이 삭제 되면... `
`Department dept속성이 변경되면 Instructor 의 관련되...`

> 118 q-5

```sql
INSERT job CHAR(20) INTO TABLE patient

ALTER TABLE patient
job CHAR(20);

```
속성을 추가시 `ALTER`

> 118 Q-6

```sql
CREATE VIEW cc('ccid', 'ccname', 'instname')
  FROM Course, Instructor
  Where Course.instructor = Instructor.id;
```
cc 뷰는 ccid, ccname instname속성을 갖는다

cc뷰는 course 테이블의 id name Instructor테이블의 name 속성

힌트 `create select from where` 사용함 그리고 **중요** `Course의 instructor = Instructor.id` 라고 한 지문에 집중!

> 118 q-7

```sql
CREATE TABLE 사원 (
  사원번호 NUMBER(40 PRIMARY KEY,
  사원명 VARCHAR2(10),
  근무지번호 NUMBER(2) (문제1) 근무지
  ON DELETE (문제2)
);
```
1. FOREIGN KEY REFERENCES
2. CASCADE

```sql

```
