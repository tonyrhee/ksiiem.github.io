---
title: "[Web] HTTP status code"
categories: [Study, Web]
---

- **HTTP(Hypertext Transfer Protocol)**는 웹 서버와 웹 클라이언트 사이에서 데이터를 주고받기 위해 사용하는 통신 방식으로 **TCP/IP 프로토콜** 위에서 동작한다. 즉, 우리가 웹을 이용하려면 웹 서버와 웹 클라이언트는 각각 TCP/IP 동작에 필수적인 IP 주소를 가져야 한다는 의미이다.
- HTTP란 이름대로라면 하이퍼텍스트(Hypertext)만 전송할 수 있어 보이지만, 실제로는 HTML이나 XML과 같은 하이퍼텍스트뿐 아니라 이미지, 음성, 동영상, Javascript, PDF와 각종 문서 파일 등 컴퓨터에서 다룰 수 있는 데이터라면 무엇이든 전송할 수 있다.
- 예를 들어 우리가 웹 브라우저의 주소창에 https://www.naver.com을 입력하고 Enter를 누르면 웹 클라이언트와 웹 서버 사이에 HTTP 연결이 맺어지고 웹 클라이언트는 웹 서버에 HTTP 요청 메시지를 보낸다. 웹 서버는 요청에 따른 처리를 진행한 후에 그 결과를 웹 클라이언트에 HTTP 응답 메시지로 보낸다. 이처럼 요청 메시지와 응답 메시지가 반복적으로 오가므로 우리는 웹을 사용할 수 있는 것이다.

![이미지](/assets/img/study/web/http_status_code/(1).png)

- **서버에서의 처리 결과**는 응답 메시지의 상태 라인에 있는 **상태 코드(status code)**를 보고 파악할 수 있다. 웹서비스에서 반환되는 상태 코드는 세 자리 숫자로 되어 있는데 첫 번째 숫자는 HTTP 응답의 종류를 구분하는 데 사용하며 나머지 2개의 숫자는 세부적인 응답 내용 구분을 위한 번호이다.
    - **1XX: Informational(정보 제공)**
        - 임시 응답으로 현재 클라이언트의 요청까지는 처리되었으니 계속 진행하라는 의미이다. HTTP 1.1 버전부터 추가되었습니다. 요청을 받았으며 프로세스를 계속 진행한다.
    - **2XX: Success(성공)**
        - 클라이언트의 요청이 서버에서 성공적으로 처리되었다는 의미이다.
    - **3XX: Redirection(리다이렉션)**
        - 완전한 처리를 위해서 추가 동작이 필요한 경우이다. 주로 서버의 주소 또는 요청한 URI의 웹 문서가 이동되었으니 그 주소로 다시 시도하라는 의미이다.
    - **4XX: Client Error(클라이언트 에러)**
        - 없는 페이지를 요청하는 등 클라이언트의 요청 메시지 내용이 잘못된 경우를 의미하며, 요청을 처리할 수 없다.
    - **5XX: Server Error(서버 에러)**
        - 서버 사정으로 메시지 처리에 문제가 발생한 경우이다. 서버의 부하, DB 처리 과정 오류, 서버에서 익셉션이 발생하는 경우를 의미한다.

### **☑️ 1XX: Informational(정보 제공)**

![이미지](/assets/img/study/web/http_status_code/(2).png)

### **☑️ 2XX: Success(성공)**

![이미지](/assets/img/study/web/http_status_code/(3).png)

### **☑️ 3XX: Redirection(리다이렉션)**

![이미지](/assets/img/study/web/http_status_code/(4).png)

![이미지](/assets/img/study/web/http_status_code/(5).png)

### **☑️ 4XX: Client Error(클라이언트 에러)**

![이미지](/assets/img/study/web/http_status_code/(6).png)

### **☑️ 5XX: Server Error(서버 에러)**

![이미지](/assets/img/study/web/http_status_code/(7).png)


<br>
**참고 자료**

---

- <https://hongong.hanbit.co.kr/http-%EC%83%81%ED%83%9C-%EC%BD%94%EB%93%9C-%ED%91%9C-1xx-5xx-%EC%A0%84%EC%B2%B4-%EC%9A%94%EC%95%BD-%EC%A0%95%EB%A6%AC/>