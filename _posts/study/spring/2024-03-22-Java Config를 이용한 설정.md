---
categories: [Study, Spring]
---

## **Java Config를 이용한 설정**


<br>
**들어가기 전에**

---

Java Config와 어노테이션을 이용해 스프링에서 사용하는 빈을 정의하고 DI하는 방법에 대해 알아보도록 한다.


<br>
**학습 목표**

---

1. JavaConfig형태의 설정파일의 내용을 이해할 수 있다.
2. @ComponentScan, @Component, @Autowired 어노테이션의 쓰임새에 대해 이해한다.


<br>
**핵심 개념**

---

- AnnotationConfigApplicationContext
- @Configuration
- @ComponentScan
- @Component
- @Autowired


<br>
**Java config를 이용한 설정을 위한 어노테이션**

---

**@Configuration**

- 스프링 설정 클래스를 선언하는 어노테이션

**@Bean**

- bean을 정의하는 어노테이션

**@ComponentScan**

- @Controller, @Service, @Repository, @Component 어노테이션이 붙은 클래스를 찾아 컨테이너에 빈으로 등록

**@Component**

- 컴포넌트 스캔의 대상이 되는 애노테이션 중 하나로써 주로 유틸, 기타 지원 클래스에 붙이는 어노테이션

**@Autowired**

- 주입 대상이되는 bean을 컨테이너에 찾아 주입하는 어노테이션


<br>
**Java Config를 이용해 설정하기**

---

**ApplicationConfig.java**

```java
package kr.or.connect.diexam01;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class ApplicationConfig {
	@Bean
	public Car car(Engine e) {
		Car c = new Car();
		c.setEngine(e);
		return c;
	}
	
	@Bean
	public Engine engine() {
		return new Engine();
	}
	
	
}

```

- @Configuration 은 스프링 설정 클래스라는 의미를 가진다. JavaConfig로 설정을 할 클래스 위에는 @Configuration가 붙어있어야 한다.
- ApplicationContext중에서 AnnotationConfigApplicationContext는 JavaConfig클래스를 읽어들여 IoC와 DI를 적용하게 된다.
- 이때 설정파일 중에 @Bean이 붙어 있는 메소드들을 AnnotationConfigApplicationContext는 자동으로 실행하여 그 결과로 리턴하는 객체들을 기본적으로 싱글턴으로 관리를 하게 된다.
- ApplicationContext는 파라미터를 받아들이지 않는 빈 생성 메서드를 먼저 실행해서 반환받은 객체를 관리한다. 그리고나서 파라미터에 생성된 객체들과 같은 타입의 객체가 있을 경우에 파라미터에 전달해서 객체를 생성한다. 빈은 클래스 이름의 첫글자를 소문자로 바꾼 이름을 기본으로 한다.


<br>
ApplicationContextExam03.java 

- 설정 파일을 읽어 실제 실행시켜주는 자바 파일 생성

```java
package kr.or.connect.diexam01;

import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class ApplicationContextExam03 {

	public static void main(String[] args) {
		// 이전까지 클래스 패스에서 설정을 읽어들였기 때문에 ClassPathXmlApplicationContext를 이용했다면, 이번엔 설정을 가지고 있는 클래스 파일을 읽어들여야 한다. 
		ApplicationContext ac = new AnnotationConfigApplicationContext(ApplicationConfig.class); // 빈을 생성해서 가진다. 
		
		Car car = (Car)ac.getBean(Car.class);
		car.run();

	}

}

```

- ApplicationConfig의 메서드명과 동일하게 설정해야 객체를 얻을 수 있다.

![이미지](/assets/img/study/spring/Java_Config%EB%A5%BC_%EC%9D%B4%EC%9A%A9%ED%95%9C_%EC%84%A4%EC%A0%95(1).png)

![이미지](/assets/img/study/spring/Java_Config%EB%A5%BC_%EC%9D%B4%EC%9A%A9%ED%95%9C_%EC%84%A4%EC%A0%95(2).png)


- 파라미터로 요청하는 class 타입으로 지정 가능하다. ApplicationContext가 관리하는 객체 중에서 해당 클래스 타입이 존재하면 해당 객체를 반환해준다.
    
    Car car = ac.getBean(Car.class);
    


<br>
ApplicationContext2.java

```java
package kr.or.connect.diexam01;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan("kr.or.connect.diexam01") // 컴포넌트 스캔 패키지를 지정해주면, 사용자가 일일이 알려주지 않아도 어노테이션 붙어있는 것들을 찾아내서 등록해준다.  
public class ApplicationConfig2 {

	
}

```

- 기존 JavaConfig에서 빈을 생성하는 메소드를 모두 제거했다. 단, @Configuration아래에 @ComponentScan이라는 어노테이션을 추가했다.
- @ComponentScan어노테이션은 파라미터로 들어온 패키지 이하에서 @Controller, @Service, @Repository, @Component 어노테이션이 붙어 있는 클래스를 찾아 메모리에 올리고 DI로 주입하도록 한다.
- 이러한 어노테이션이 붙어있지 않은 객체들은 @Bean 어노테이션을 이용해 직접 생성해주는 방식으로 클래스를 관리할 수 있다. Spring JDBC나 다른 라이브러리가 갖고있는 객체들을 사용하는 경우, 해당 라이브러리를 열어서 직접 어노테이션을 붙일 수 없다. 그럴 경우 @Bean 어노테이션을 이용해 빈을 등록하여 편리하게 사용 가능하다.


<br>
Engine.java

- 기존의 Car클래스와 Engine클래스 위에 @Component를 붙이도록 한다.

```java
package kr.or.connect.diexam01;

import org.springframework.stereotype.Component;

@Component
public class Engine {
	public Engine() {
		System.out.println("Engine 초기화");
	}
	
    public void exec() {
    	System.out.println("엔진이 동작합니다.");
    }
}

```

Car.java

```java
package kr.or.connect.diexam01;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class Car {
	@Autowired // 컨테이너에 Engine 타입의 객체가 생성되어 있으면 알아서 주입해준다.(setter 메서드 불필요) 
	private Engine v8; 
	
	public Car() {
		System.out.println("Car 생성자"); // 객체 생성 확인 
	}
	
	public void setEngine(Engine e) {
		this.v8 = e;
	}
	
	public void run() {
		System.out.println("엔진을 이용하여 달립니다.");
		v8.exec(); 
	}
	
//	public static void main(String[] args) {
//		Engine e = new Engine(); // 자동차는 엔진이 필요하다. 
//		Car c = new Car();
//		c.setEngine(e);
//		c.run();
//	}
}

```


<br>
ApplicationContextExam04.java

- 수정된 JavaConfig를 읽어들여 실행하는 클래스를 보도록 한다.

```java
package kr.or.connect.diexam01;

import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class ApplicationContextExam04 {

	public static void main(String[] args) {
		ApplicationContext ac = new AnnotationConfigApplicationContext(ApplicationConfig2.class); // 빈을 생성해서 가진다. 
		
		Car car = (Car)ac.getBean(Car.class);
		car.run();

	}

}

```

- Spring에서 사용하기에 알맞게 @Controller, @Service, @Repository, @Component 어노테이션이 붙어 있는 객체들은 ComponentScan을 이용해서 읽어들여 메모리에 올리고 DI를 주입하도록 하고, 이러한 어노테이션이 붙어 있지 않은 객체는 @Bean어노테이션을 이용하여 직접 생성해주는 방식으로 클래스들을 관리하면 편리하다.

- 다루는 빈의 수가 많아질수록 XML로 설정하는 것보다 **`@ComponentScan`**, **`@Component`**, **`@Autowired`**를 이용하는 것이 유지보수에 더 좋을 것으로 보인다.
1. **XML 설정 vs. 어노테이션 기반 설정**:
    - XML 설정은 빈의 관리와 의존성 주입이 외부에 명시적으로 표현되어 있어서 가독성이 좋고 관리하기 쉽다. 하지만 빈의 수가 많아질수록 XML 파일이 복잡해지고 유지보수가 어려워질 수 있다.
    - 반면에 어노테이션 기반 설정은 자바 코드에 설정이 명시되어 있어서 직관적이고 간단하다. 또한, IDE의 지원을 받아서 리팩토링이나 자동 완성 기능을 활용할 수 있습니다. 하지만 어노테이션 설정만으로는 설정의 전체 구조를 파악하기 어려울 수 있다.
2. **@Autowired의 활용**:
    - **`@Autowired`**를 이용하면 필요한 의존성을 자동으로 주입할 수 있다. 이는 XML 설정에서 직접 의존성을 설정하는 것보다 편리하고 간단하다.
    - **`@Autowired`**를 사용하는 방법에는 필드, 생성자, 세터 메서드에 사용할 수 있다. 필드 주입은 코드의 간결성을 높이지만 의존성이 숨겨져 있어서 가독성이 떨어질 수 있다. 반면에 생성자 주입은 의존성을 명시적으로 드러내어 가독성과 테스트 용이성을 높일 수 있다. 세터 메서드 주입은 선택적인 의존성을 주입할 때 유용하다. 하지만 일부 빈이 누락될 수 있고, 런타임 시점에서 NullPointerException이 발생할 수 있다.