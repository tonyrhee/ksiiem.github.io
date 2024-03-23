---
categories: [study, Spring]
---

## **1) Spring MVC란?**


<br>
**들어가기 전에**

---

Spring 프레임워크에서 웹 어플리케이션 작성을 위해 제공하는 Web MVC모듈에 대해 알아보도록 한다.


<br>
**학습 목표**

---

1. MVC Model 1과 MVC Model 2 구조의 차이점에 대해 이해한다.
2. 발전된 형태의 MVC Model2 구조에 대해 이해한다.


<br>
**핵심 개념**

---

- MVC Model 1
- MVC Model 2
- Spring MVC


<br>
**MVC란?**

---

- MVC는 Model-View-Controller의 약자이다. 원래는 제록스 연구소에서 일하던 트뤼그베 린즈커그가 처음으로 소개한 개념으로, 데스트톱 어플리케이션용으로 고안되었다.
- Model: 모델은 뷰가 렌더링하는데 필요한 데이터이다. 예를 들어 사용자가 요청한 상품 목록이나, 주문 내역이 이에 해당한다.
- View: 웹 애플리케이션에서 뷰(View)는 실제로 보이는 부분이며, 모델을 사용해 렌더링을 한다. 뷰는 JSP, JSF, PDF, XML등으로 결과를 표현한다.
- Controller: 컨트롤러는 사용자의 액션에 응답하는 컴포넌트이다. 컨트롤러는 모델을 업데이트하고, 다른 액션을 수행한다.


<br>
**MVC(Model-View-Controller) 아키텍처를 자바 웹 프로그래밍에서 어떻게 변형하여 사용하는가?**

---

- MVC Model 1 아키텍처

![이미지](/assets/img/study/spring/Spring_MVC(1).png)

- 클라이언트의 요청을 JSP가 받아서 처리하고, Java Bean을 사용하여 데이터베이스와 상호작용하여 결과를 생성한다.
- 이 방식은 JSP에 Java 코드와 HTML이 혼합되어 유지보수가 어렵다.


<br>
- MVC Model 2 아키텍처

![이미지](/assets/img/study/spring/Spring_MVC(2).png)

- 클라이언트의 요청을 서블릿이 받아서 처리하고, Java Bean을 사용하여 데이터베이스와 상호작용하여 결과를 생성한다.
- 서블릿은 요청과 데이터를 처리하는 컨트롤러(Controller) 역할을 수행하고, JSP는 모델의 결과를 보여주게 하는 뷰(View) 역할을 수행하여 로직과 뷰를 분리한다.


<br>
- MVC Model2 발전형태

![이미지](/assets/img/study/spring/Spring_MVC(3).png)

- 모든 클라이언트 요청을 하나의 프론트 컨트롤러(Front Controller) 서블릿이 받는다. 이 서블릿은 단 하나만 존재한다.
- 프론트 컨트롤러는 실제 처리를 컨트롤러(Controller) 클래스에게 위임한다.
- 이렇게 함으로써 모든 요청을 하나의 서블릿에서 처리할 수 있으며, 컨트롤러 클래스는 Java Bean을 사용하여 결과를 생성하고, 결과를 모델(Model)에 담아서 프론트 컨트롤러에게 반환한다.
- 프론트 컨트롤러는 알맞은 뷰(View)에게 모델을 전달하여 결과를 출력한다.


<br>
- Spring Web Module - Model2 MVC 패턴을 지원하는 Spring Module

![이미지](/assets/img/study/spring/Spring_MVC(4).png)

- Spring MVC:
    - 위에서 설명한 Model2 아키텍처의 발전된 형태가 Spring 프레임워크의 Web 모듈에 구현되어 있다.
    - 이 모델은 Spring MVC로 알려져 있으며, 클라이언트의 요청을 컨트롤러가 받아서 처리하고, 결과를 모델에 담아서 뷰에 전달하여 출력한다.