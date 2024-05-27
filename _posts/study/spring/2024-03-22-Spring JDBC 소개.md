---
categories: [Study, Spring]
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
| --- |:---:|:---:|
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


<br>
## **2) Spring JDBC 실습(1) -** 스프링 JDBC를 이용한 DAO 개발


<br>
**학습 목표**

---

1. DTO와 DAO에 대한 개념을 이해한다.
2. Spring JDBC를 이용해 DAO를 작성할 수 있다.


<br>
**핵심 개념**

---

- DTO
- DAO
- NamedParameterJdbcTemplate


<br>
**DTO란?**

---

- DTO란 Data Transfer Object의 약자이다.
- **계층간 데이터 교환**을 위한 자바빈즈이다. 여기서의 계층이란 컨트롤러 뷰, 비지니스 계층, 퍼시스턴스 계층을 의미한다.
- 일반적으로 DTO는 로직을 가지고 있지 않고, 순수한 데이터 객체이다.
- 필드와 getter, setter를 가진다. 추가적으로 toString(), equals(), hashCode()등의 Object 메소드를 오버라이딩 할 수 있다.


<br>
**DTO의 예**

---

```java
public class ActorDTO {
    private Long id;
    private String firstName;
    private String lastName;
    public String getFirstName() {
        return this.firstName;
    }
    public String getLastName() {
        return this.lastName;
    }
    public Long getId() {
        return this.id;
    }
    // ......
}
```


<br>
**DAO란?**

---

- DAO란 Data Access Object의 약자로 데이터를 조회하거나 조작하는 기능을 전담하도록 만든 객체이다.
- 보통 **데이터베이스를 조작하는 기능**을 전담하는 목적으로 만들어진다.


<br>
**ConnectionPool 이란?**

---

- DB 연결은 비용이 많이 든다.
- 커넥션 풀은 미리 커넥션을 여러 개 맺어 둔다. 커넥션이 필요하면 커넥션 풀에게 빌려서 사용한 후 반납한다.
- 즉, 커넥션 풀은 데이터베이스로의 연결을 관리하고, 클라이언트가 요청할 때마다 이미 생성된 커넥션을 제공한다. 이로써 클라이언트는 매번 데이터베이스와의 연결을 설정하고 해제할 필요가 없으며, 더 빠르고 효율적으로 데이터베이스와 통신할 수 있다.
- 커넥션 풀을 사용할 때 중요한 점은 커넥션을 사용한 후 반드시 반환해야 한다는 것이다. 그렇지 않으면 커넥션 풀이 과도하게 사용되거나, 더 이상 사용 가능한 커넥션이 없을 때 시스템이 지연되거나 오류를 발생시킬 수 있다.

![이미지](/assets/img/study/spring/Spring_JDBC(1).png)


<br>
**DataSource란?**

---

- DataSource는 커넥션 풀을 관리하는 목적으로 사용되는 객체이다. DataSource를 이용해 커넥션을 얻어오고 반납하는 등의 작업을 수행한다.
- 커넥션 풀을 관리하기 위해 데이터소스가 사용된다. 데이터소스는 커넥션 풀을 생성하고 관리하며, 클라이언트에게 커넥션을 제공하고 반납하는 작업을 수행한다. 클라이언트는 데이터소스를 통해 커넥션을 얻고 사용한 후, 명시적으로 close() 메서드를 호출하여 커넥션을 반납한다.
    
    이러한 구조를 통해 데이터베이스와의 연결을 효율적으로 관리하고, 성능을 향상시킬 수 있다.
    


<br>
**스프링 JDBC를 이용한 DAO 개발**

---

![이미지](/assets/img/study/spring/Spring_JDBC(2).png)


1. 스프링 컨테이너인 ApplicationContext는 설정 파일인 ApplicationConfig 클래스를 읽어들인다. ApplicationConfig 클래스에는 componentScan 어노테이션을 사용하여 DAO 클래스를 찾도록 설정한다. 이렇게 찾은 DAO 클래스들은 Spring 컨테이너에 의해 관리된다.
2. ApplicationContext는 DBConfig 클래스를 import하고, DBConfig 클래스에서는 데이터 소스와 트랜잭션 매니저 객체를 생성한다. 이 클래스는 데이터베이스와의 연결을 설정하고 관리하는 역할을 수행한다.
3. DAO 클래스들은 필드로 NamedParameterJdbcTemplate과 SimpleJdbcInsert를 가진다. 이 두 객체는 Spring JDBC에서 제공하는 데이터베이스 액세스를 편리하게 해주는 객체이며, 내부적으로 DB 연결을 위해 DataSource 객체를 사용한다. RoleDao 클래스의 생성자에서 이 두 객체를 초기화하고, 초기화된 객체를 활용하여 데이터베이스 액세스 메서드를 구현한다. 
4. Spring JDBC를 사용하는 사용자는 파라미터와 SQL 문을 가장 많이 신경써야 한다. SQL 쿼리는 RoleDaoSqls에 상수로 정의되어 있어 나중에 변경될 경우 편리하게 수정할 수 있다.
5. Role DTO는 한 건의 Role 정보를 저장하고 전달하기 위한 목적으로 사용된다. 
    
    이렇게 구성된 데이터 액세스 계층은 Spring 프레임워크의 기능을 활용하여 데이터베이스와의 효율적인 상호작용을 가능하게 한다. 
    


<br>
**참고 자료**

---

- <https://ejbvn.wordpress.com/category/week-2-entity-beans-and-message-driven-beans/day-09-using-jdbc-to-connect-to-a-database/>
- <https://velog.io/@byeongju/DataSource-cbd8ln4x>