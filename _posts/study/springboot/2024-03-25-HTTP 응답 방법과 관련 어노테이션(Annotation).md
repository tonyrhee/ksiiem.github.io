---
categories: [Study, SpringBoot]
---

## HTTP 응답 방법 3가지

---

스프링에서 응답 데이터를 만드는 방법은 크게 세 가지로 나눌 수 있다.

### 1. **정적 리소스**:
- 스프링 부트는 클래스 패스 내에 있는 특정 디렉토리(**`/static`**, **`/public`**, **`/resources`**, **`/META-INF/resources`**)에 위치한 정적 리소스를 제공한다.

  이러한 디렉토리에 정적 리소스를 위치시키면, 스프링 부트는 해당 리소스를 정적으로 제공한다. 따라서 웹 애플리케이션에서 이러한 디렉토리에 리소스를 저장하면, 클라이언트가 요청할 때 해당 리소스를 서비스할 수 있다.

- 정적 리소스는 서버에서 변경 없이 그대로 제공되며, HTML, CSS, JavaScript와 같은 정적 파일을 웹 브라우저에 제공할 때 사용된다.
- **`src/main/resources`** 디렉토리는 리소스를 보관하는 곳이며, 클래스 패스의 시작 경로이다.
- 예를 들어, **`src/main/resources/static/test/index.html`** 경로에 파일이 존재한다면, 해당 파일은 웹 브라우저에서 **`http://localhost:8080/test/index.html`**과 같이 실행할 수 있다.

### 2. **뷰 템플릿 사용**:
- 뷰 템플릿을 통해 HTML을 동적으로 생성하고 응답으로 반환한다.
- 스프링 부트는 기본적으로 **`/src/main/resources/templates`** 경로를 제공한다.
- 뷰 템플릿을 사용하여 HTML을 동적으로 생성하고, 이를 웹 브라우저에 제공할 때 주로 사용된다.


<br>
**스프링 MVC에서 동적인 HTML 파일을 렌더링하는 예제**

---

**1) hello.html 파일 작성**:

- **`resources/templates`** 경로에 있는 **`hello.html`** 파일은 동적으로 생성된다.(Thymeleaf 템플릿 엔진을 사용)
- **`${data}`**는 Thymeleaf의 표현식으로, 해당 위치에 모델 객체에서 전달된 데이터를 출력한다.

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
	<head>
		<meta charset="UTF-8">
	  <title>Title</title>
	</head>
	<body>
		<p th:text="${data}">empty</p>	
	</body>
</html>
```

**2) 컨트롤러 메소드 작성**:

- **`response-view`** 경로로 GET 요청이 들어오면 해당 메소드가 실행된다.
- 메소드 내에서는 **`Model`** 객체를 사용하여 **`data`**라는 속성에 "hello!"라는 값을 추가한다.
- 이후에는 "hello"라는 문자열을 반환한다. 이 문자열은 뷰의 이름을 나타낸다. 스프링은 이 뷰 이름을 통해 해당하는 템플릿 파일(`**hello.html**`)을 찾아서 렌더링한다.

```java
@GetMapping("/response-view")
	public String responseViewV2(Model model) {
		model.addAttribute("data", "hello!");
		return "hello";
	}
```

이렇게 하면 스프링 MVC는 **`hello.html`** 파일을 찾아서 해당하는 데이터를 넣어 렌더링하고, 그 결과를 클라이언트에게 응답으로 전송한다.

### **3. HTTP 메시지 사용**:

- HTTP API를 제공하는 경우, HTML 대신에 데이터를 전달해야 한다. 이때는 HTTP 메시지의 바디에 데이터를 실어서 보낸다. 문자열 또는 객체를 반환하는 방식으로 데이터를 HTTP 응답으로 전달한다.
- 반환 값이 문자열인 경우, 문자 내용이 직접 HTTP 응답의 바디에 담겨 전송된다.
- 반환 값이 객체인 경우, 객체의 값이 JSON 형식으로 변환되어 HTTP 응답의 바디에 담겨 전송된다.

**HTTP 응답 관련 어노테이션**

---

- **@ResponseBody**: 메소드에서 반환되는 데이터가 HTTP 응답의 바디에 직접 작성되도록 지정한다.
- **@RestController**: 해당 컨트롤러가 REST API(HTTP API)를 제공하는 경우에 사용되며, 모든 핸들러 메소드에 자동으로 @ResponseBody가 적용된다. 즉, 이 어노테이션은 @Controller와 @ResponseBody를 합친 것과 동일한 역할을 한다.
- 즉, @Controller 어노테이션은 반환 값이 String이면 해당 String을 뷰 이름으로 사용하여 뷰를 찾고, 렌더링된 뷰를 반환한다. 반면에 @RestController 어노테이션은 반환 값이 HTTP 응답의 본문으로 직접 전달된다. 따라서 @RestController를 사용하는 경우에는 반환 값이 HTTP 응답의 본문에 직접 쓰여지며, 뷰를 찾거나 렌더링하는 과정이 필요하지 않다.
- 이와 함께, 반환하는 데이터 형식에 따라 적절한 HttpMessageConverter가 선택되어 작동한다. 문자열인 경우에는 **`StringHttpMessageConverter`**, 객체인 경우에는 **`MappingJackson2HttpMessageConverter`**가 사용된다. 그리고 **`@ResponseStatus`** 어노테이션을 사용하여 응답의 HTTP 상태 코드를 지정할 수 있다.

**HTTP 메시지 사용 예제**

---

- HTTP API를 제공할 때는 HTML 대신에 데이터를 전달해야 한다. 이를 위해 HTTP 메시지의 본문(body)에 JSON과 같은 형식으로 데이터를 실어 보낸다.
- String을 반환할 경우, 해당 문자열이 그대로 HTTP 응답의 본문(body)으로 전송된다.

```java
@ResponseBody
@GetMapping("/response-body-string")
public String responseBody() {
	return "OK";
}
```

- 객체를 반환할 경우, 해당 객체의 내용이 JSON 형식으로 변환되어 HTTP 응답의 본문에 담겨 전송된다.

```java
@ResponseStatus(HttpStatus.OK)
@ResponseBody
@GetMapping("/response-body-json")
public HelloData responseBodyJson() {
	HelloData helloData = new HelloData();
	helloData.setUsername("hyun");
	helloData.setAge(20);
	return helloData;
}
```

정리하자면, 스프링에서는 다양한 방법을 통해 HTTP 응답을 생성하고 제공할 수 있으며, 이는 클라이언트 요청의 성격과 목적에 따라 선택되어야 한다.


<br>
**참고 자료**

---

- [https://hstory0208.tistory.com/entry/Spring-HTTP-응답-방법과-관련-어노테이션Annotation?category=1054975](https://hstory0208.tistory.com/entry/Spring-HTTP-%EC%9D%91%EB%8B%B5-%EB%B0%A9%EB%B2%95%EA%B3%BC-%EA%B4%80%EB%A0%A8-%EC%96%B4%EB%85%B8%ED%85%8C%EC%9D%B4%EC%85%98Annotation?category=1054975)