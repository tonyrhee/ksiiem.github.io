---
categories: [study, Spring]
---

## **1) Spring JDBC 소개**

<br>
**들어가기 전에**

---

- JDBC를 이용해서 프로그래밍을 하게 되면 반복적인 코드가 많이 발생한다. 이러한 반복적인 코드는 개발자의 생산성을 떨어트리는 주된 원인이 된다. 이러한 문제를 해결하기 위해 등장한 것이 Spring JDBC이다.


<br>
**학습 목표**

---

1. Spring JDBC에 대한 개념을 이해한다.
2. Spring JDBC의 핵심 클래스와 인터페이스에 대해 이해한다.


<br>
**핵심 개념**

---

- JdbcTemplate
- RowMapper


<br>
**Spring JDBC**

---

- JDBC 프로그래밍을 보면 반복되는 개발 요소가 있다. 이러한 반복적인 요소는 개발자를 지루하게 만든다.
- 개발하기 지루한 JDBC의 모든 저수준 세부사항을 스프링 프레임워크가 처리해준다. 개발자는 필요한 부분만 개발하면 된다.


<br>
**Spring JDBC - 개발자가 해야할 일은?**

---

| 동작 | 스프링 | 어플리케이션 개발자 |
| --- |: --- :|: --- :|
| 연결 파라미터 정의 |  | o |
| 연결 오픈 | o |  |
| SQL 문 지정 |  | o |
| 파라미터 선언과 파라미터 값 제공 |  | o |
| 스테이트먼트(statement) 준비와 실행 | o |  |
| (존재한다면) 결과를 반복하는 루프 설정 | o |  |
| 각 이터레이션에 대한 작업 수행 |  | o |
| 모든 예외 처리 | o |  |
| 트랜잭션 제어 | o |  |
| 연결, 스테이트먼트(statement), 리절트 셋(resultset) 닫기 | o |  |


<br>
**Spring JDBC 패키지 - 추상화 프레임워크**

---

**org.springframework.jdbc.core**

- JdbcTemplate 클래스 및 관련 Helper 객체 제공(JDBC 템플릿의 다양한 콜백 인터페이스를 포함한다.)

**org.springframework.jdbc.datasource**

- DataSource를 쉽게 접근하기 위한 유틸 클래스, 트랜젝션매니져 및 다양한 DataSource 구현을 제공
- Java EE 컨테이너 외부에 수정되지 않고 운영되는 JDBC 코드와 테스트에서 사용할 수 있는 여러가지 간단한 데이터 소스 구현체를 포함한다.

**org.springframework.jdbc.object**

- RDBMS 조회, 갱신, 저장 등을 스레드 세이프하고 재사용 가능한 객체로 나타내는 클래스를 포함

**org.springframework.jdbc.support**

- jdbc.core 및 jdbc.object를 사용하는 JDBC 프레임워크를 지원
- SQL Exception 변환 기능과 약간의 유틸리티 클래스를 제공


<br>
**JDBC Template**

---

- org.springframework.jdbc.core에서 가장 중요한 클래스이다. 리소스 생성, 해지를 처리해서 연결을 닫는 것을 잊어 발생하는 문제 등을 피할 수 있도록 한다.
- 스테이먼트(Statement)의 생성과 실행을 처리힌다. SQL 조회, 업데이트, 저장 프로시저 호출, ResultSet 반복호출 등을 실행한다.
- JDBC 예외가 발생할 경우 org.springframework.dao패키지에 정의되어 있는 일반적인 예외로 변환시킨다.

**JdbcTemplate select 예제1**

```java
// 열의 수 구하기 - 해당 테이블의 데이터 조회
int rowCount = this.jdbcTemplate.queryForInt("select count(*) from t_actor");
```

**JdbcTemplate select 예제2**

```java
// 변수 바인딩 사용하기
int countOfActorsNamedJoe = this.jdbcTemplate.queryForInt("select count(*) from t_actor where first_name = ?", "Joe");
```

**JdbcTemplate select 예제3**

```java
// String값으로 결과 받기
String lastName = this.jdbcTemplate.queryForObject("select last_name from t_actor where id = ?", new Object[]{1212L}, String.class);
```

**JdbcTemplate select 예제4**

```java
// 한 행 조회하기 - 존재하는 여러 개의 컬럼들을 원하는 객체에 매핑 
Actor actor = this.jdbcTemplate.queryForObject(

  "select first_name, last_name from t_actor where id = ?",

  new Object[]{1212L},

  new **RowMapper**<Actor>() { 
		// RowMapper를 상속받은 이름 없는 객체를 이용해 mapRow() 메소드 오버라이딩 
    public Actor mapRow(ResultSet rs, int rowNum) throws SQLException {
			
			// 해당 ResultSet의 값을 담기 위한 Actor 
      Actor actor = new Actor();

      actor.setFirstName(rs.getString("first_name"));

      actor.setLastName(rs.getString("last_name"));

      return actor;

    }

  });
```

**JdbcTemplate select 예제5**

```java
// 여러 건 조회하기
List<Actor> actors = this.jdbcTemplate.**query**(

  "select first_name, last_name from t_actor",

  new RowMapper<Actor>() {

    public Actor mapRow(ResultSet rs, int rowNum) throws SQLException {

      Actor actor = new Actor();

      actor.setFirstName(rs.getString("first_name"));

      actor.setLastName(rs.getString("last_name"));

      return actor;

    }

  });
```

**JdbcTemplate select 예제6**

```java
// 중복 코드 제거 (1건 구하기와 여러 건 구하기가 같은 코드에 있을 경우) - 별도의 메소드로 추출
public List<Actor> findAllActors() {

  return this.jdbcTemplate.query( "select first_name, last_name from t_actor", new ActorMapper());

}

private static final class ActorMapper implements RowMapper<Actor> {

  public Actor mapRow(ResultSet rs, int rowNum) throws SQLException {

    Actor actor = new Actor();

    actor.setFirstName(rs.getString("first_name"));

    actor.setLastName(rs.getString("last_name"));

    return actor;

  }

}
```

**JdbcTemplate insert 예제**

```java
// INSERT 하기
this.jdbcTemplate.update("insert into t_actor (first_name, last_name) values (?, ?)",  "Leonor", "Watling");
```

**JdbcTemplate update 예제**

```java
// UPDATE 하기
this.jdbcTemplate.update("update t_actor set = ? where id = ?",  "Banjo", 5276L);
```

**JdbcTemplate delete 예제**

```java
// DELETE 하기
this.jdbcTemplate.update("delete from actor where id = ?", Long.valueOf(actorId));
```


<br>
**JdbcTemplate외의 접근방법**

---

**NamedParameterJdbcTemplate**

- JdbcTemplate에서 JDBC statement 인자를 `?`를 사용하는 대신 파라미터명을 사용하여 바인딩하는 것을 지원
- [NamedParameterJdbcTemplate 예제](https://docs.spring.io/spring/docs/current/spring-framework-reference/data-access.html#jdbc-NamedParameterJdbcTemplate)

**SimpleJdbcTemplate**

- JdbcTemplate과 NamedParameterJdbcTemplate 가장 빈번하게 사용되는 작업을 합쳐놓은 템플릿 클래스
- 이제 JdbcTemplate과 NamedParameterJdbcTemplate에 모든 기능을 제공하기 때문에 삭제 예정될 예정(deprecated)
- [SimpleJdbcTemplate 예제](https://www.concretepage.com/spring/simplejdbctemplate-spring-example)

**SimpleJdbcInsert**

- 테이블에 쉽게 데이터 insert 기능을 제공
- [SimpleJdbcInsert 예제](https://www.tutorialspoint.com/springjdbc/springjdbc_simplejdbcinsert.htm)