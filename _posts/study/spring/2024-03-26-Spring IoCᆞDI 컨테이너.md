---
categories: [study, Spring]
---
**들어가기 전에**

---

스프링 프레임워크의 핵심 개념 중의 하나인 IoC와 DI에 대해 학습하도록 한다.

**학습 목표**

---

1. 컨테이너에 대한 개념을 이해한다.
2. IoC에 대한 개념을 이해한다.
3. DI에 대한 개념을 이해한다.

### **컨테이너(Container)**

---

- 컨테이너는 보통 인스턴스의 생명주기를 관리하며, 생성된 인스턴스에게 추가적인 기능을 제공한다.
- 예를 들어, Servlet을 실행해주는 **WAS는 Servlet 컨테이너를 가지고 있다**고 말한다. WAS는 웹 브라우저로부터 **서블릿 URL에 해당하는 요청을 받으면, 서블릿을 메모리에 올린 후 실행**한다.
- 개발자가 서블릿 클래스를 작성했지만, 실제로 메모리에 올리고 실행하는 것은 WAS가 가지고 있는 Servlet 컨테이너이다.
- Servlet컨테이너는 동일한 서블릿에 해당하는 요청을 받으면, 또 메모리에 올리지 않고 기존에 메모리에 올라간 서블릿을 실행하여 그 결과를 웹 브라우저에게 전달한다.


### **IoC(Inversion of Control)**

---

- IoC란 Inversion of Control의 약어이다. inversion은 사전적 의미로는 '도치, 역전'이다. 보통 IoC를 제거의 역전이라고 번역한다.
- 개발자는 프로그램의 흐름을 제어하는 코드를 작성한다. 그런데, 이 흐름의 제어를 개발자가 하는 것이 아니라 다른 프로그램이 그 흐름을 제어하는 것을 loC라고 말한다.
- **컨테이너가 코드 대신 오브젝트의 제어권을 갖고 있어** IoC(제어의 역전)이라 한다.
- 예를 들어, 서블릿 클래스는 개발자가 만들지만, 그 서블릿의 메소드를 알맞게 호출하는 것은 WAS이다.
- 이렇게 개발자가 만든 어떤 클래스나 메소드를 다른 프로그램이 대신 실행해주는 것을 제어의 역전이라고 한다.

### **DI(Dependency Injection)**

---

- DI는 Dependency Injection의 약자로, 의존성 주입이란 뜻을 가지고 있다.
- DI는 **클래스 사이의 의존 관계를** **빈(Bean)설정 정보를 바탕으로 컨테이너가 자동으로 연결**해주는 것을 말한다.

**1) DI가 적용 안 된 예**

- 개발자가 직접 인스턴스를 생성한다.

```java
class 엔진 {

}

class 자동차 {
     엔진 v5 = new 엔진();
}
```

![이미지](/assets/img/study/spring/Spring_IoC%E1%86%9EDI_%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88(1).png)


**2)Spring에서 DI가 적용된 예**

- 엔진 type의 v5변수에 아직 인스턴스가 할당되지 않았다. 컨테이너가 v5변수에 인스턴스를 할당해주게 된다.
- 약속된 어노테이션을 이용해 선언만 하면 스프링 컨테이너가 빈 객체를 생성해 주입해준다.

```java
@Component
class 엔진 {

}

@Component
class 자동차 {
     @Autowired
     엔진 v5;
}
```

![이미지](/assets/img/study/spring/Spring_IoC%E1%86%9EDI_%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88(2).png)

**Spring에서 제공하는 lOC/DI 컨테이너**

---

- **BeanFactory**: loC/DI에 대한 **기본 기능**을 가지고 있다.
- **ApplicationContext**: BeanFactory의 모든 기능을 포함하며, 일반적으로 BeanFactory보다 추천된다. 트랜잭션처리, AOP등에 대한 처리를 할 수 있다. BeanPostProcessor, BeanFactoryPostProcessor 등을 자동으로 등록하고, 국제화 처리, 애플리케이션 이벤트 등을 처리할 수 있다.
    - BeanPostProcessor: 컨테이너의 기본로직을 오버라이딩하여 인스턴스화와 의존성 처리 로직 등을 개발자가 원하는 대로 구현할 수 있도록 한다.
    - BeanFactoryPostProcessor: 설정된 메타 데이터를 커스터마이징 할 수 있다.

- 스프링 프레임워크는 DI Container라고도 말한다. 스프링 프레임워크 이외에도 DI Container는 존재한다.
    - PicoContainer: DI 기능에 집중한 작은 컨테이너 프레임워크로서, 큰 오버헤드가 없이 단순하게 구성할 수 있다. 비교적 작은 프로젝트에 적합하다.
    - Guice: Guice 또한 단순하게 구성할수 있으며 Annotation, Generics 등의 기능을 적극적으로 사용한다는 특징이 있다. 무엇보다 큰 장점은 속도가 빠르다는 것이다.