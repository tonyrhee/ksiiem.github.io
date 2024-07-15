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

