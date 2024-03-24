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

**MVC Model 1 아키텍처**

![이미지](/assets/img/study/spring/Spring_MVC(1).png)

- 클라이언트의 요청을 JSP가 받아서 처리하고, Java Bean을 사용하여 데이터베이스와 상호작용하여 결과를 생성한다.
- 이 방식은 JSP에 Java 코드와 HTML이 혼합되어 유지보수가 어렵다.


<br>
**MVC Model 2 아키텍처**

![이미지](/assets/img/study/spring/Spring_MVC(2).png)

- 클라이언트의 요청을 서블릿이 받아서 처리하고, Java Bean을 사용하여 데이터베이스와 상호작용하여 결과를 생성한다.
- 서블릿은 요청과 데이터를 처리하는 컨트롤러(Controller) 역할을 수행하고, JSP는 모델의 결과를 보여주게 하는 뷰(View) 역할을 수행하여 로직과 뷰를 분리한다.


<br>
**MVC Model2 발전형태**

![이미지](/assets/img/study/spring/Spring_MVC(3).png)

- 모든 클라이언트 요청을 하나의 프론트 컨트롤러(Front Controller) 서블릿이 받는다. 이 서블릿은 단 하나만 존재한다.
- 프론트 컨트롤러는 실제 처리를 컨트롤러(Controller) 클래스에게 위임한다.
- 이렇게 함으로써 모든 요청을 하나의 서블릿에서 처리할 수 있으며, 컨트롤러 클래스는 Java Bean을 사용하여 결과를 생성하고, 결과를 모델(Model)에 담아서 프론트 컨트롤러에게 반환한다.
- 프론트 컨트롤러는 알맞은 뷰(View)에게 모델을 전달하여 결과를 출력한다.


<br>
**Spring Web Module** - Model2 MVC 패턴을 지원하는 Spring Module

![이미지](/assets/img/study/spring/Spring_MVC(4).png)

- Spring MVC:
    - 위에서 설명한 Model2 아키텍처의 발전된 형태가 Spring 프레임워크의 Web 모듈에 구현되어 있다.
    - 이 모델은 Spring MVC로 알려져 있으며, 클라이언트의 요청을 컨트롤러가 받아서 처리하고, 결과를 모델에 담아서 뷰에 전달하여 출력한다.


<br>
**내용 정리**

---

- Model 1 아키텍처에서는 JSP가 View와 Controller의 역할을 혼합하여 수행하기 때문에 유지보수가 어렵다.반면에 Model 2 아키텍처에서는 Controller 기능을 분리하여 디자인과 개발을 구조화하고, 역할과 책임을 명확히 할 수 있다. 또한, 프론트 컨트롤러(Front Controller)를 통해 모든 요청을 한 곳에서 처리하기 때문에 작업이 수월해지며, 파일 구조가 변경되더라도 URL을 유지할 수 있어서 유연성이 높다.

- '프런트 컨트롤 디자인 패턴(Front Controller Design Pattern)'은 웹 애플리케이션에서 사용되는 디자인 패턴 중 하나이다. 프런트 컨트롤러는 클라이언트로부터 들어오는 모든 요청을 중앙 집중적으로 처리하는 컨트롤러이다. 이렇게 하나의 컨트롤러가 모든 요청을 받아들이면, **요청을 처리하기 전에 필요한 전처리 작업**을 수행하거나, **요청을 분석하여 적절한 핸들러(Controller)로 라우팅**하는 역할을 수행한다.
    
    이 패턴은 다음과 같은 장점을 제공한다.
    
    1. 일관된 전처리 작업: 프런트 컨트롤러에서 인증, 권한 확인, 로깅 등과 같은 전처리 작업을 수행할 수 있다.
    2. 중복 코드 제거: 프런트 컨트롤러에서 공통적으로 필요한 로직을 구현함으로써 각각의 핸들러에서 중복 코드를 제거할 수 있다.
    3. 애플리케이션 흐름 관리: 모든 요청을 중앙에서 관리하므로 애플리케이션의 흐름을 쉽게 파악하고 관리할 수 있다.
    
    따라서 프런트 컨트롤 디자인 패턴은 웹 애플리케이션의 구조를 간결하고 유지보수하기 쉽도록 만들어준다.


<br>
## **2) Spring MVC구성요소** - 구성요소와 동작 이해


<br>
**들어가기 전에**

---

Spring MVC에서 가장 핵심적인 역할을 수행하는 DispatcherServlet이 어떤 순서로 동작하는지 살펴보도록 한다. 이를 통해서 Spring MVC에서 사용되는 컴포넌트들에 대해 알아보도록 한다.


<br>
**학습 목표**

---

1. DispatcherServlet이 어떤 순서로 동작하는지 이해한다.
2. DispatcherServlet에서 사용되는 컴포넌트(객체)들이 어떤 것들이 있는지 안다.


<br>
**핵심 개념**

---

- DispatcherServlet
- HandlerMapping
- HandlerAdapter
- ViewResolver


<br>
**Spring MVC 기본 동작 흐름**

---

![이미지](/assets/img/study/spring/Spring_MVC(5).png)


Spring MVC는 다음과 같은 컴포넌트들로 구성되며, 다음과 같은 순서로 동작한다.

1. **Dispatcher Servlet (디스패처 서블릿):**
    - 클라이언트로부터 들어오는 모든 요청을 받는 서블릿이다.
2. **Handler Mapping (핸들러 매핑):**
    - Dispatcher Servlet이 요청을 처리할 컨트롤러와 메서드를 결정하기 위해 사용된다.
    - 요청 URL과 어떤 컨트롤러, 어떤 메서드가 매핑되는지 알려주는 역할을 한다.
    - 개발자가 설정한 URL 매핑 정보를 기반으로 동작한다.
3. **Handler Adapter (핸들러 어댑터):**
    - Dispatcher Servlet이 결정한 컨트롤러와 메서드를 실행하는 역할을 한다.
4. **Controller (컨트롤러):**
    - 요청에 대해 실행되는 비즈니스 로직을 담당하는 부분이다.
    - Handler Adapter에 의해 실행된다.
    - 요청에 따라 적절한 데이터를 Model에 담아 반환한다.
5. **Model (모델):**
    - 컨트롤러가 처리한 결과 데이터를 담는 객체이다.
    - 컨트롤러가 반환한 데이터를 View에 전달하기 위해 사용된다.
6. **View Resolver (뷰 리졸버):**
    - 컨트롤러가 반환한 view name을 기반으로 실제로 사용될 View를 결정한다.
    - View의 경로를 해석하고 해당하는 View 객체를 반환한다.
7. **View (뷰):**
    - 사용자에게 결과를 표시하는 역할을 한다.
    - 뷰 리졸버에 의해 선택된 View를 사용하여 클라이언트에게 응답을 생성한다.


<br>
## **2) Spring MVC구성요소(2)** - 구성요소와 동작 이해


<br>
**DispatcherServlet**

---

- 프론트 컨트롤러 (Front Controller)
- 클라이언트의 모든 요청을 받은 후 이를 처리할 핸들러에게 넘기고 핸들러가 처리한 결과를 받아 사용자에게 응답 결과를 보여준다.
- DispathcerServlet은 여러 컴포넌트를 이용해 작업을 처리한다.

**DispatcherServlet 내부 동작흐름**

![이미지](/assets/img/study/spring/Spring_MVC(6).png)


내부 동작 흐름을 요약하면 다음과 같다:

1. **요청의 선처리:**
    - 클라이언트로부터의 요청이 Dispatcher Servlet에 도착하면, 요청에 대한 선처리 작업이 수행된다.
2. **HandlerExecutionChain 결정:**
    - Handler Mapping을 통해 클라이언트 요청에 대한 처리를 담당할 컨트롤러와 메서드를 결정한다.
3. **HandlerExecutionChain 실행:**
    - 결정된 HandlerExecutionChain은 컨트롤러와 메서드를 실행한다.
    - 실행 과정에서 예외가 발생하면 예외 처리를 수행하고, 예외가 발생하지 않으면 뷰를 렌더링한다.
4. **뷰 렌더링:**
    - 컨트롤러의 처리 결과를 적절한 View로 전달하여 렌더링한다.
    - View는 클라이언트에게 반환될 HTML, JSON, XML 등의 응답을 생성한다.
5. **요청 처리 종료 및 응답:**
    - 요청 처리가 완료되면 응답이 클라이언트에게 반환되고, 요청 처리를 종료한다.

이러한 과정을 거쳐 Dispatcher Servlet은 클라이언트의 요청을 처리하고, 컨트롤러의 실행 결과를 적절한 View로 전달하여 응답을 생성한다. 이를 통해 웹 애플리케이션의 요청 처리 과정이 원활하게 이루어지며, 예외 상황에 대한 처리도 효과적으로 이루어진다.


<br>
**요청 선처리 작업시 사용된 컴포넌트**

---

**org.springframework.web.servlet.LocaleResolver**

- 지역 정보를 결정해주는 전략 오브젝트이다.
- 디폴트인 AcceptHeaderLocalResolver는 HTTP 헤더의 정보를 보고 지역정보를 설정해준다.

**org.springframework.web.servlet.FlashMapManager**

- FlashMap객체를 조회(retrieve) & 저장을 위한 인터페이스
- RedirectAttributes의 addFlashAttribute메소드를 이용해서 저장한다.
- 리다이렉트 후 조회를 하면 바로 정보는 삭제된다.

**org.springframework.web.context.request.RequestContextHolder**

- 일반 빈에서 HttpServletRequest, HttpServletResponse, HttpSession 등을 사용할 수 있도록 한다.
- 해당 객체를 일반 빈에서 사용하게 되면, Web에 종속적이 될 수 있다.

**org.springframework.web.multipart.MultipartResolver**

- 멀티파트 파일 업로드를 처리하는 전략

**DispatcherServlet 내부 동작흐름 상세 - 요청 선처리 작업**

![이미지](/assets/img/study/spring/Spring_MVC(7).png)


DispatcherServlet은 요청을 선처리하는 작업을 수행한다. 이 과정에서는 다음과 같은 일련의 작업들이 이루어진다:

1. **지역화(Localization) 처리:**
    - DispatcherServlet이 요청을 선처리하는 작업 중 하나로, Spring MVC는 지역화를 지원하여 사용자가 원하는 언어로 화면을 보여줄 수 있다.
    - 사용자의 브라우저에서 전송된 헤더 정보를 통해 사용자의 언어 설정을 확인하고, 이를 기반으로 Locale을 결정한다. Locale은 언어, 국가 등의 정보를 포함하고 있어 언어 설정에 따라 다른 지역화된 내용을 제공할 수 있다.
    - 결정된 Locale을 기반으로 각 요청에 맞는 지역화된 콘텐츠를 제공합니다.
2. **RequestContextHolder를 사용한 요청 저장:**
    - DispatcherServlet은 현재 요청을 스레드 로컬 객체인 RequestContextHolder에 저장한다.
    - 이를 통해 컨트롤러의 메서드에서 HttpServletRequest와 HttpServletResponse와 같은 Spring이 관리하는 객체를 쉽게 사용할 수 있다.
3. **FlashMap 복원:**
    - FlashMap은 Spring 3에서 추가된 기능으로, redirect로 값을 전달할 때 사용된다.
    - URL에 파라미터를 전달하는 것보다 더 간결하고 효율적으로 값을 전달할 수 있다.
    - FlashMap을 사용하면 redirect될 때 한 번만 값을 유지할 수 있다.
4. **파일 업로드 처리:**
    - 파일 업로드를 위해서는 특수한 형태의 Request 객체가 필요하다.
    - 멀티 파트 요청이 들어오면 DispatcherServlet은 MultipartResolver를 사용하여 멀티 파트를 처리한다.
    - 이를 통해 파일 정보를 읽어들이고, 필요한 경우에는 업로드된 파일을 처리할 수 있다.

이와 같은 선처리 작업을 통해 DispatcherServlet은 요청을 적절히 처리하고, 개발자가 웹 애플리케이션을 보다 효과적으로 구현할 수 있도록 지원한다.


<br>
**요청 전달시 사용된 컴포넌트**

---

**org.springframework.web.servlet.HandlerMapping**

- HandlerMapping구현체는 어떤 핸들러가 요청을 처리할지에 대한 정보를 알고 있다.
- 디폴트로 설정되는 있는 핸들러매핑은 BeanNameHandlerMapping과 DefaultAnnotationHandlerMapping 2가지가 설정되어 있다.

**org.springframework.web.servlet.HandlerExecutionChain**

- HandlerExecutionChain구현체는 실제로 호출된 핸들러에 대한 참조를 가지고 있다.
- 즉, 무엇이 실행되어야 될지 알고 있는 객체라고 말할 수 있으며, 핸들러 실행전과 실행후에 수행될 HandlerInterceptor도 참조하고 있다.

**org.springframework.web.servlet.HandlerAdapter**

- 실제 핸들러를 실행하는 역할을 담당한다.
- 핸들러 어댑터는 선택된 핸들러를 실행하는 방법과 응답을 ModelAndView로 변화하는 방법에 대해 알고 있다.
- 디폴트로 설정되어 있는 핸들러어댑터는 HttpRequestHandlerAdapter, SimpleControllerHandlerAdapter, AnnotationMethodHanlderAdapter 3가지이다.
- @RequestMapping과 @Controller 애노테이션을 통해 정의되는 컨트롤러의 경우 DefaultAnnotationHandlerMapping에 의해 핸들러가 결정되고, 그에 대응되는 AnnotationMethodHandlerAdapter에 의해 호출이 일어난다.

**DispatcherServlet 내부 동작흐름 상세 - 요청 전달**

![이미지](/assets/img/study/spring/Spring_MVC(8).png)


요청 전달 단계에서는 다음과 같은 과정이 이루어진다:

1. **HandlerMapping을 통한 HandlerExecutionChain 결정:**
    - DispatcherServlet은 요청을 처리할 적절한 컨트롤러(Handler)를 결정하기 위해 HandlerMapping에게 요청을 위한 HandlerExecutionChain을 요청한다.
    - HandlerMapping은 요청된 URL을 기반으로 적절한 컨트롤러와 메서드를 찾아서 HandlerExecutionChain을 반환한다.
2. **HandlerExecutionChain 존재 여부 확인:**
    - HandlerMapping은 요청된 URL에 해당하는 HandlerExecutionChain을 발견했는지 여부를 확인한다.
    - 만약 HandlerExecutionChain이 발견되지 않았다면, 이는 요청된 페이지가 존재하지 않음을 의미하므로, 서버는 HTTP 404 에러를 반환한다.
3. **HandlerAdapter 결정:**
    - HandlerExecutionChain이 존재하는 경우, DispatcherServlet은 해당 요청을 처리할 HandlerAdapter를 결정한다.
    - HandlerAdapter는 컨트롤러가 실제로 요청을 처리할 수 있는 어댑터이다.
4. **HandlerAdapter의 존재 여부 확인:**
    - 만약 적절한 HandlerAdapter가 발견되지 않았다면, 이는 서버의 오류로 간주되며 ServletException이 발생한다.
    - 서버가 요청을 처리할 수 있는 HandlerAdapter를 찾을 수 없는 경우에는 일반적으로 개발자가 설정 오류를 수정해야 한다.
5. **요청 처리:**
    - HandlerAdapter가 결정되고, HandlerExecutionChain이 존재하는 경우, 해당 HandlerAdapter를 사용하여 요청을 처리한다.
    - HandlerAdapter는 컨트롤러의 메서드를 실행하고, 그 결과를 DispatcherServlet에 반환한다.
    - 요청 처리 과정에서 문제가 없으면 요청이 성공적으로 처리되고, 결과를 클라이언트에 응답한다.

이와 같은 요청 전달 단계를 통해 DispatcherServlet은 요청된 URL에 대해 적절한 컨트롤러를 찾고, 이를 실행하여 요청을 처리한다. 만약 요청된 페이지나 HandlerAdapter를 찾을 수 없는 경우에는 서버가 적절한 오류를 반환한다.



<br>
**요청 처리시 사용된 컴포넌트**

---

**org.springframework.web.servlet.ModelAndView**

- ModelAndView는 Controller의 처리 결과를 보여줄 view와 view에서 사용할 값을 전달하는 클래스이다.

**org.springframework.web.servlet.RequestToViewNameTranslator**

- 컨트롤러에서 뷰 이름이나 뷰 오브젝트를 제공해주지 않았을 경우 URL과 같은 요청정보를 참고해서 자동으로 뷰 이름을 생성해주는 전략 오브젝트이다. 디폴트는 DefaultRequestToViewNameTranslator이다.

**DispatcherServlet 내부 동작흐름 상세 - 요청 처리**

![이미지](/assets/img/study/spring/Spring_MVC(9).png)


요청 처리 단계에서는 다음과 같은 과정이 이루어진다:

1. **인터셉터 확인 및 실행:**
    - HandlerExecutionChain이 결정되면, DispatcherServlet은 해당 핸들러에 대해 사용 가능한 인터셉터(필터)가 있는지 확인한다.
    - 인터셉터는 핸들러 실행 전 또는 후에 요청을 가로채어 필요한 전처리 또는 후처리를 수행한다.
    - 만약 사용 가능한 인터셉터가 존재한다면, preHandle 메서드가 호출되어 요청을 처리하고, 그 후 핸들러가 실행된다.
2. **핸들러 실행 및 ModelAndView 객체 반환:**
    - 핸들러(Controller 또는 메서드)가 실행된 후에는 ModelAndView 객체를 반환한다.
    - ModelAndView 객체는 뷰의 이름과 모델 데이터를 포함하고 있다.
    - 만약 핸들러가 결과를 직접 반환하지 않고 ModelAndView 객체를 생성하여 반환한다면, DispatcherServlet은 이를 처리한다.
3. **RequestToViewNameTranslator 작동:**
    - ModelAndView 객체에 뷰의 이름이 지정되어 있지 않은 경우, RequestToViewNameTranslator가 동작한다.
    - 이 Translator는 요청의 URL을 기반으로 뷰의 이름을 결정하여 ModelAndView 객체에 설정한다.
4. **인터셉터 후처리 및 뷰 렌더링:**
    - postHandle 메서드를 사용하여 인터셉터가 핸들러 실행 후에 수행해야 할 작업을 정의한다.
    - 인터셉터 후처리가 완료되면, DispatcherServlet은 뷰 렌더링을 위해 적절한 뷰를 선택하고 모델 데이터를 뷰에 전달한다.
    - 선택된 뷰는 ModelAndView 객체에 지정된 뷰의 이름을 기반으로 결정된다.

Spring은 Servlet API에 종속되지 않도록 하기 위해 ModelAndView와 같은 컴포넌트를 제공하여 모델 데이터를 전달한다. 이러한 방식은 HttpServletRequest와 같은 Servlet API에 의존하지 않고도 모델 데이터를 효율적으로 전달할 수 있도록 한다.

따라서 요청 처리 단계에서는 인터셉터를 사용하여 전/후처리 작업을 수행하고, 핸들러 실행 후에는 ModelAndView를 통해 뷰의 이름과 모델 데이터를 전달하여 적절한 뷰를 렌더링한다. 만약 적절한 뷰가 없을 경우에는 RequestToViewNameTranslator가 동작하여 뷰의 이름을 결정한다.


<br>
**예외 처리시 사용된 컴포넌트**

---

**org.springframework.web.servlet.handlerexceptionresolver**

- 기본적으로 DispatcherServlet이 DefaultHandlerExceptionResolver를 등록한다.
- HandlerExceptionResolver는 예외가 던져졌을 때 어떤 핸들러를 실행할 것인지에 대한 정보를 제공한다.

**DispatcherServlet 내부 동작흐름 상세 - 예외처리**

![이미지](/assets/img/study/spring/Spring_MVC(10).png)

1. **예외 발생:**
    - 핸들러(Controller 또는 메서드)가 실행되는 과정에서 예외가 발생할 수 있다.
2. **HandlereExceptionResolver 호출:**
    - DispatcherServlet은 발생한 예외를 처리하기 위해 등록된 모든 HandlerExceptionResolver에게 문의한다.
    - HandlerExceptionResolver는 등록된 예외 처리 전략에 따라 예외를 처리하고, 적절한 ModelAndView를 반환한다.
3. **예외 처리 및 재개 또는 예외 재던지기:**
    - 만약 HandlerExceptionResolver가 적절한 ModelAndView 객체를 반환했다면, DispatcherServlet은 해당 ModelAndView를 사용하여 요청 처리를 계속한다.
    - 하지만 HandlerExceptionResolver가 ModelAndView 객체를 반환하지 않으면, DispatcherServlet은 발생한 예외를 다시 상위로 전파한다.
    - 이 경우 예외는 Servlet 컨테이너로 전달되어 기본 예외 처리 메커니즘에 따라 처리된다.

예외 처리 단계에서는 예외 발생 시 HandlerExceptionResolver에게 처리를 요청하고, 해당 예외를 처리할 수 있는 Resolver를 찾아서 처리합니다. 처리된 결과에 따라 요청 처리를 재개하거나 예외를 다시 던지게 된다.


<br>
**뷰 렌더링 과정시 사용된 컴포넌트**

---

**org.springframework.web.servlet.ViewResolver**

- 컨트롤러가 리턴한 뷰 이름을 참고해서 적절한 뷰 오브젝트를 찾아주는 로직을 가진 전략 오프젝트이다.
- 뷰의 종류에 따라 적절한 뷰 리졸버를 추가로 설정해줄 수 있다.

**DispatcherServlet 내부 동작흐름 상세 - 뷰 렌더링 과정**

![이미지](/assets/img/study/spring/Spring_MVC(11).png)


뷰 렌더링 과정은 다음과 같다:

1. **뷰 렌더링 요청:**
    - Handler가 요청을 처리하고 ModelAndView 객체를 반환한다.
    - ModelAndView에는 뷰 이름(일반적으로 문자열)과 렌더링에 필요한 모델 데이터가 포함된다.
2. **ViewResolver의 검색:**
    - DispatcherServlet은 반환된 뷰 이름을 사용하여 등록된 ViewResolver를 찾는다.
    - 뷰 이름을 해석하고 실제 View 객체를 생성하기 위해 ViewResolver의 구현체를 찾는다.
3. **View 객체 생성:**
    - ViewResolver는 뷰 이름을 해석하여 해당하는 View 객체를 생성한다.
    - 생성된 View 객체는 뷰의 렌더링을 담당한다.
4. **렌더링 수행:**
    - 생성된 View 객체는 ModelAndView에 포함된 모델 데이터를 사용하여 뷰를 렌더링한다.
    - 모델 데이터는 뷰의 템플릿(예: JSP, Thymeleaf)에 전달되어 동적인 콘텐츠를 생성한다.
5. **렌더링된 결과 반환:**
    - View 객체는 뷰를 렌더링한 결과를 반환한다.
    - 일반적으로는 HTML 또는 다른 마크업 언어로 구성된 페이지가 생성된다.
6. **요청 처리 계속 진행:**
    - 뷰가 성공적으로 렌더링되면 DispatcherServlet은 렌더링된 결과를 응답으로 클라이언트에게 반환한다.
    - 클라이언트는 렌더링된 페이지를 받고 화면에 표시하게 된다.

뷰 렌더링 과정에서는 뷰 이름을 해석하고 해당하는 ViewResolver를 통해 실제 View 객체를 생성하여 렌더링을 수행한다. 렌더링된 결과는 클라이언트에게 반환되어 요청 처리가 완료된다. 만약 ViewResolver가 뷰를 찾지 못하면 ServletException이 발생하여 요청 처리가 중단된다. 


<br>
**DispatcherServlet 내부 동작흐름 상세 - 요청 처리 종료**

![이미지](/assets/img/study/spring/Spring_MVC(12).png)


1. **인터셉터의 afterCompletion 메서드 호출:**
    - HandlerExecutionChain이 존재하면 해당 인터셉터의 afterCompletion 메서드가 호출된다.
    - 인터셉터의 afterCompletion 메서드는 요청 처리가 완전히 종료된 후에 실행되는 메서드로, 주로 리소스 정리나 로깅 등의 작업을 수행한다.
2. **RequestHandlerEvent 발생:**
    - HandlerExecutionChain이 존재하지 않거나 인터셉터의 afterCompletion 메서드 실행이 완료되면 RequestHandlerEvent가 발생한다.
    - 이 이벤트는 요청 처리가 완료되었음을 알리고, 스프링 애플리케이션 내부에서 추가적인 작업을 수행할 수 있도록 한다.
3. **요청 처리 완료:**
    - RequestHandlerEvent 발생을 통해 요청 처리가 완료된다.
    - 클라이언트에게 응답이 반환되고, 요청과 응답에 관련된 모든 작업이 마무리된다.

스프링은 RequestHandlerEvent가 발생했을 때 이를 감지하고 추가적인 작업을 수행할 수 있도록 이벤트 리스너를 등록할 수 있다. 이를 통해 요청 처리가 완료된 후에 특정한 동작을 수행할 수 있다.