---
categories: [Programmers, SQL, Oracle, Lv.2]
tags: [Programmers, SQL, Oracle, Lv.2] 
---

<https://school.programmers.co.kr/learn/courses/30/lessons/59414>{:target="_blank"}

![문제](/assets/img/programmers/sql/oracle/lv.2/DATETIME%EC%97%90%EC%84%9C_DATE%EB%A1%9C_%ED%98%95_%EB%B3%80%ED%99%98(1).png)

- 문제 풀이

```sql
-- TO_CHAR 함수를 사용하여 시각(시-분-초)을 제외한 날짜(년-월-일)만 표시
SELECT ANIMAL_ID, NAME, TO_CHAR(DATETIME, 'YYYY-MM-DD') AS "날짜"
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```


<br>
- **`TO_CHAR`** 함수는 일반적으로 데이터베이스에서 날짜, 숫자 등을 문자열로 변환하는 데 사용되는 함수 중 하나이다. 이 함수는 날짜 또는 숫자 값을 특정 포맷의 문자열로 변환한다.
    
    ```sql
    TO_CHAR(expression, format)
    ```
    
    - **`expression`**: 변환하려는 값 (날짜, 숫자 등)
    - **`format`**: 출력되는 문자열의 형식
    
    ```sql
    SELECT TO_CHAR(SYSDATE, 'YYYY-MM-DD HH24:MI:SS') AS formatted_date
    FROM dual;
    ```
    
    - **`SYSDATE`**는 현재 날짜와 시간을 반환하는 Oracle 함수이다.
    - **`'YYYY-MM-DD HH24:MI:SS'`**는 출력하고자 하는 문자열의 형식을 나타낸다. 여기서 **`YYYY`**는 연도, **`MM`**은 월, **`DD`**는 일, **`HH24`**는 24시간 형식의 시간, **`MI`**는 분, **`SS`**는 초를 나타낸다.
    - 결과는 현재 날짜와 시간을 'YYYY-MM-DD HH24:MI:SS' 형식으로 변환한 문자열이 된다.

<br>
- 실행 결과

![실행 결과](/assets/img/programmers/sql/oracle/lv.2/DATETIME%EC%97%90%EC%84%9C_DATE%EB%A1%9C_%ED%98%95_%EB%B3%80%ED%99%98(2).png)