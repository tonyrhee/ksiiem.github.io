---
categories: [study, Spring]
---

### **REST**

---

- REST: REpresentational State Transfer
    - 하나의 URI는 하나의 고유한 Resource를 대표하도록 설계
    - 특정 URI(Uniform Resource Identifier)는 그에 상응하는 데이터를 의미 → 데이터에 대한 처리는 HTTP 방식(GET, POST, PUT, DELETE 등)과 같은 추가적인 정보를 통해서 결정
    - REST 서비스 특징: 특정 URI를 통해서 사용자가 원하는 정보를 제공하는 방식
        - RESTful:
        - RESTful API: REST 방식으로 제공되는 외부 연결 URI
- REST와 HTTP methods
    - GET: 리소스 또는 리소스 컬렉션을 얻어옴
    - POST: 리소스 생성
    - PUT: 리소스 업데이트
    - DELETE: 리소스 삭제

### **REST: RequestMapping & RequestMethod**

---

![이미지](/assets/img/study/spring/RESTful_Web_Service_with_Spring_MVC(1).png)

- HTTP 메소드는 클라이언트와 서버 간의 통신에서 사용되는 표준화된 방법이다. 주요 HTTP 메소드에는 GET, POST, PUT, DELETE 등이 있다.
    - **GET**: 서버로부터 데이터를 요청한다. 주로 데이터를 조회할 때 사용된다.
    - **POST**: 서버로 데이터를 보낸다. 주로 데이터를 생성하거나 수정할 때 사용된다.
    - **PUT**: 서버에 데이터를 전송하여 리소스를 생성 또는 수정한다. 일반적으로 리소스의 전체 업데이트에 사용된다.
    - **DELETE**: 서버에서 특정 리소스를 삭제한다.
- 그 외에도 HEAD, OPTIONS, PATCH 등의 메소드가 있다.
    1. **HEAD**: 이 메소드는 GET 메소드와 비슷하지만, 서버는 응답으로 본문(body)을 반환하지 않는다. 대신에 응답 헤더만을 반환하여 리소스의 메타데이터(헤더 정보)를 확인할 수 있다. 주로 리소스가 변경되었는지 확인하기 위해 사용된다.
    2. **OPTIONS**: 이 메소드는 서버에서 지원되는 HTTP 메소드를 확인하거나 리소스가 요청된 URL에서 지원되는 메소드를 확인하기 위해 사용된다. CORS(Cross-Origin Resource Sharing)와 관련된 요청에서 자주 사용된다.
    3. **PATCH**: 이 메소드는 리소스의 부분적인 업데이트를 수행하기 위해 사용된다. PUT 메소드와 유사하지만, PUT은 리소스 전체를 대체하는 데 사용되고, PATCH는 리소스의 일부만 업데이트한다. 주로 부분적인 업데이트가 필요한 경우에 사용된다.

### **Spring REST Annotation**

---

- **@ResponseBody**
    - 메소드 또는 메소드의 리턴 타입에 사용하는 어노테이션
        - @Controller 어노테이션이 있는 클래스에서 정의된 메소드 (리턴 타입)에 @ResponseBody 어노테이션을 사용하면, 클라이언트로 JSP가 아닌 **데이터 자체가 서비스** 됨
    - Spring MVC의 기본 처리 방식(Controller → JSP)과 달리, 메소드가 리턴하는 데이터를 스프링의 MessageConverter가 가공해서 클라이언트(브라우저)에게 전달
    - Spring 3 버전부터 지원
- **@RestController**
    - Controller 클래스에서 사용되는 어노테이션
    - JSP와 같은 View를 만들어 내는 것이 목적이 아닌, **REST 방식의 데이터 처리를 위한 클래스**임을 선언하는 어노테이션
    - @RestController의 모든 콘트롤러 메소드들은, @ResponseBody 어노테이션 없이, 뷰가 아닌 데이터 자체를 클라이언트(브라우저)에게 서비스(리턴)하는 메소드가 됨

### **REST & Ajax**

---

- **Ajax(Asynchronous JavaScript And XML)**
    - 요청(request)과 응답(response)가 비동기적(asynchronous)으로 이루어지는 통신 방식
    - 클라이언트(브라우저)는 서버에게 요청을 보내고, 응답을 기다리지 않고 다른 작업을 처리함. 응답을 받았을 때 그에 대한 처리(화면 업데이트 등)을 함
    - **JavaScript 라이브러리** 중 하나
    - 자바스크립트를 통해서 서버에 request, response
    - JavaScript를 사용하여 **클라이언트, 서버 간**의 **통신**, 즉 비동기적으로 XML 데이터를 주고 받는다.
    
    ![이미지](/assets/img/study/spring/RESTful_Web_Service_with_Spring_MVC(2).png)

    
- **REST(Representational State Transfer)**
    - HTTP URL과 방식(method: GET, POST 등)을 통해서 서버로부터 데이터를 전송받을 수 있는 방식
- **Web Application 구현**
    - **Ajax를 이용하여 REST API를 호출**
    - REST API의 결과 데이터를 브라우저가 처리해서 화면 업데이트

### **HTTP Client-Server 통신**

---

![이미지](/assets/img/study/spring/RESTful_Web_Service_with_Spring_MVC(3).png)


1. 웹 브라우저는 웹 서버에게 요청(request)을 전송
2. 웹 서버는 클라이언트의 요청을 처리 후 응답(response)을 클라이언트에게 전송
3. 웹 브라우저는 서버의 응답(response)을 받을 때까지 대기하다가 응답을 받은 후 화면을 업데이트

### **Ajax 통신 방식**

---

![이미지](/assets/img/study/spring/RESTful_Web_Service_with_Spring_MVC(4).png)


1. 웹 브라우저는 웹 서버에게 요청(request)을 보냄
    - 브라우저는 응답(response)을 기다리지 않고, 다른 처리(요청)을 할 수 있음
2. 웹 서버는 요청에 대한 처리를 한 후 클라이언트에게 응답(response)을 보냄
3. 웹 브라우저는 응답이 도착했을 때 화면을 업데이트 함
    - 보통 화면의 일부만 갱신

### **Ajax: Asynchronous JavaScript And XML**

---

![이미지](/assets/img/study/spring/RESTful_Web_Service_with_Spring_MVC(5).png)


### XMLHttpRequest Functions

---

- open(method, url, async)
    - 요청(request) 타입을 지정
    - readyState의 상태가 OPENED로 변경된다.
        - method: 요청 타입 - GET/POST
        - url: 서버(파일) 위치
        - async: 비동기 방식 사용 여부 - true/false
- send()
    - GET 방식으로 요청을 서버로 전송
- send(string)
    - POST 방식으로 요청을 서버로 전송
        - string: 요청 파라미터 이름과 값
- setRequestHeader(header, value)
    - 요청에 HTTP 헤더를 덧붙임
        - header: header 이름
        - value: header 값

### XMLHttpRequest Properties

---

- onreadystatechange
    - readyState 속성이 변경될 때 호출 될 함수를 정의
- readyState
    - XMLHttpRequest의 readyState 프로퍼티는 XMLHttpRequest 객체의 상태를 보여준다.
    - readyState 프로퍼티의 값이 변경될 때마다 readystatechange 이벤트가 실행되므로 해당 이벤트에서 readyState 프로퍼티의 값을 확인하는 것이 좋다.
    
    | 값 | 상태  | 설명 |
    | --- | --- | --- |
    | 0 | UNSENT | request not initialized - XMLHTTPRequest 객체는 생성되었지만 open() 메소드가 호출되지 않았다. 초기 상태이므로 readystatechange 이벤트는 실행되지 않는다. |
    | 1 | OPENED | server connection established - open() 메소드가 호출되었다. |
    | 2 | HEADERS_RECEIVED | request received -send() 메소드가 호출되었다. |
    | 3 | LOADING | processing request - 응답을 로드 중이다. |
    | 4 | DONE | request finished and response is ready - 요청 완료되었다. |
    
    ```jsx
    onst data = JSON.stringify({
      title: "foo",
      body: "bar",
      userId: 1
    });
    
    const xhr = new XMLHttpRequest();
    
    xhr.onreadystatechange = () => {
      if (xhr.readyState === xhr.HEADERS_RECEIVED) {
        console.log("HEADERS_RECEIVED");
      } else if (xhr.readyState === xhr.LOADING) {
        console.log("LOADING");
      } else if (xhr.readyState === xhr.DONE) {
        console.log("DONE");
      }
    };
    
    xhr.open("POST", "https://jsonplaceholder.typicode.com/posts");
    xhr.send(data);
    ```
    
    ![이미지](/assets/img/study/spring/RESTful_Web_Service_with_Spring_MVC(6).png)

    
    - send() 메소드가 호출되면 readyState의 상태가 HEADERS_RECEIVED로 변경되며 응답 데이터를 받을 준비가 된다.
    - send() 메소드를 호출하면 요청을 보냄과 동시에 데이터를 받으므로 redayState가 LOADING으로 변경된다.
    - 모든 데이터를 응답받으면 readyState가 DONE로 변경된다.
    
    ```jsx
    const data = JSON.stringify({
      title: "foo",
      body: "bar",
      userId: 1
    });
    
    const xhr = new XMLHttpRequest();
    
    xhr.onreadystatechange = () => {
      if (xhr.readyState === xhr.HEADERS_RECEIVED) {
        console.log("HEADERS_RECEIVED");
        xhr.abort();
      } else if (xhr.readyState === xhr.LOADING) {
        console.log("LOADING");
      } else if (xhr.readyState === xhr.DONE) {
        console.log("DONE");
      }
    };
    
    xhr.open("POST", "https://jsonplaceholder.typicode.com/posts");
    xhr.send(data);
    출처: https://developer-talk.tistory.com/843 [DevStory:티스토리]
    ```
    
    ![이미지](/assets/img/study/spring/RESTful_Web_Service_with_Spring_MVC(7).png)

    
    - send() 메소드를 호출하면 readyState가 HEADERS_RECEIVED로 변경된다. 이때, abort() 메소드를 호출하면 요청이 중단되므로 readyState가 LOADING으로 변경되지 않고 DONE로 변경된다.
- status
    - HTML 메시지 코드
        - 200: “OK”
        - 403: “Forbidden”
        - 404: “Page not found”
- statusText
    - status-text를 리턴(예: OK, Not found, …)

### **Axios**

---

- Axios는 Node.js와 브라우저를 위한 Promise 기반 HTTP 클라이언트이다. Axios는 브라우저와 Node.js 환경에서 모두 사용할 수 있도록 설계되어 있다.
- 브라우저에서는 XMLHttpRequest 객체를 생성하여 HTTP 요청을 생성하여 처리하고, Node.js 환경에서는 내장된 http 모듈을 사용하여 HTTP 요청을 생성하여 처리한다.
- Promise API를 지원하여 비동기적인 요청 처리를 간편하게 할 수 있다.
- 요청 및 응답 인터셉트를 통해 HTTP 요청 전송 전이나 응답 수신 후에 데이터를 처리할 수 있다.
- 요청 및 응답 데이터 변환을 자동으로 처리하여 개발자가 별도의 작업 없이도 데이터를 쉽게 다룰 수 있다.
- 요청 취소 기능을 제공하여 긴 응답 시간이 필요 없는 요청을 중단할 수 있다.
- JSON 데이터 자동 변환을 지원하여 응답 데이터를 자동으로 JSON 형태로 변환한다.
- XSRF(크로스 사이트 요청 위조)를 방지하기 위한 클라이언트 사이드 지원을 제공한다.
- HTTP Methods를 사용할 수 있어서 다양한 종류의 요청을 처리할 수 있다.

```jsx
// 지정된 ID를 가진 유저에 대한 요청
axios.get('/user?ID=12345')
	.then(function (response) {
		// 성공 핸들링
		console.log(response);
	})
	.catch(function (error) {
		// 에러 핸들링
		console.log(error);
	})
	.finally(function () {
		// 항상 실행되는 영역
	});
```

```jsx
// async/await 사용을 원한다면, 함수 외부에 `async` 키워드를 추가
// async/await는 ECMAScript 2017 문법
async function getUser() {
	try {
	 const response = await axios.get('/user?ID=12345');
	 console.log(response);
	} catch (error) {
		console.error(error);
	}
}

getUser();
```


<br>
**브라우저와 Node.js에서의 요청 생성과 처리**

---

요청 생성은 브라우저와 Node.js에서 모두 이루어지지만, 각 환경에서의 요청 처리는 해당 환경의 특성에 맞춰 다르게 이루어진다.

1. **브라우저**:
    - **XMLHttpRequest(XHR)** 객체를 사용하여 HTTP 요청을 생성한다. 이 객체는 브라우저의 JavaScript 코드에서 사용된다.
    - 브라우저에서는 XHR 객체를 사용하여 서버로 요청을 보내고, 서버에서의 응답을 받는다. 이 과정은 주로 비동기적으로 이루어진다.
    - 브라우저에서의 요청 처리는 JavaScript 코드로 작성된 콜백 함수 또는 Promise를 사용하여 이루어진다. 요청이 성공하면 콜백 함수가 실행되어 응답을 처리하거나 Promise의 resolve 메서드가 호출되어 응답을 처리한다.
2. **Node.js**:
    - Node.js 환경에서는 **http 모듈**을 사용하여 HTTP 요청을 생성한다. 이 모듈은 Node.js에 내장되어 있어 별도의 설치가 필요하지 않는다.
    - http 모듈을 사용하여 Node.js에서 HTTP 요청을 생성하고 서버로 보낸다. 이때 요청은 비동기적으로 이루어진다.
    - Node.js에서의 요청 처리는 두 가지 방법으로 이루어진다. 첫 번째 방법은 http 모듈의 메서드를 사용하여 요청을 보낸 후, 요청 객체의 'response' 이벤트를 처리하여 응답을 처리하는 것이다. 두 번째 방법은 Promise나 콜백 함수를 사용하여 비동기적으로 응답을 처리하는 것이다.


### **[비동기 통신] Ajax와 Axios의 차이점?**

---

- Ajax는 JavaScript와 XMLHttpRequest 객체를 사용하여 웹 브라우저와 웹 서버 간에 데이터를 비동기적으로 교환하는 기술이다. 이를 통해 웹 페이지가 다시 로드되지 않고 필요한 데이터만 가져올 수 있어 웹 애플리케이션의 속도와 사용성을 향상시킬 수 있다. 즉, 요청을 한 후에도 해당 요청에 대한 응답을 기다리지 않고 다른 작업을 수행할 수 있다. 최근에는 클라이언트와 서버 간의 리스트 데이터를 주고받을 때 JSON이 많이 사용된다.
- Axios는 웹 애플리케이션에서 사용하는 **AJAX 기반의 API 호출을 단순화하고 향상시키기 위한 JavaScript 라이브러리**이다. Ajax를 사용할 때 발생할 수 있는 불편함을 보완해주는 기능들을 제공한다.
    
    Axios가 제공하는 기능:
    
    1. 구문의 간결성: Axios는 Promise 기반이므로 XMLHttpRequest 객체를 직접 사용할 때보다 비동기 처리에 대한 코드를 더 간결하게 작성할 수 있다.
    2. 에러 처리 항상: Promise 기반으로 작동하기 때문에 비동기 요청을 보낼 때 발생할 수 있는 에러를 간편하게 catch할 수 있다.
    3. JSON 데이터 자동 변환: 응답을 자동으로 JSON 형태로 변환하여 제공한다. 이는 JSON 형식의 데이터를 다룰 때 JSON parsing이나 stringify를 직접 할 필요가 없어 편리하다.
    4. 요청 및 응답 인터셉터: HTTP 요청이 전송되기 전이나 서버로부터 응답을 받기 전에 데이터를 처리할 수 있도록 인터셉터 기능을 제공한다. 이를 통해 전역 오류 처리나 HTTP 헤더 관리 등이 가능하다.
    5. 타임아웃 설정: 긴 응답 시간이 발생할 경우 요청을 자동으로 취소하고 에러를 반환할 수 있다.
    
    이러한 기능들을 통해 Axios는 Ajax를 보다 효율적으로 활용할 수 있도록 도움을 주는 라이브러리이다.
    
    ```
    Axios
    - node.js와 브라우저를 위한 Promise 기반 HTTP 클라이언트
    - 브라우저: XMLHTTPRequests 생성
    - node.js: http 요청 생성
    - Promise API를 지원
    - 요청 및 응답 인터셉트
    - 요청 및 응답 데이터 변환
    - 요청 취소
    - JSON 데이터 자동 변환
    - XSRF를 막기위한 클라이언트 사이드 지원
    - HTTP Methods를 사용
    ```
    

<br>
**참고 자료**

---

- <https://developer-talk.tistory.com/843>
- [https://velog.io/@dusunax/AXIOS란-feat.-React](https://velog.io/@dusunax/AXIOS%EB%9E%80-feat.-React)
- [https://hstory0208.tistory.com/entry/비동기-통신-Ajax와-Axios의-차이점](https://hstory0208.tistory.com/entry/%EB%B9%84%EB%8F%99%EA%B8%B0-%ED%86%B5%EC%8B%A0-Ajax%EC%99%80-Axios%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)
- <https://github.com/JakeOh/20230228_itwill_java140_lab_web/blob/master/Spring_REST.pdf>