---
title: "JSP & Servelt"
date: 2017-10-20 08:26:28 -0400
categories: jekyll update
---

# JSP 입문

## JSP란?

### JSP란?

- **Java Server Page의 약자로 html기반에 JAVA코드를 블록화하여 삽입한 것**

### JSP동작구조

- 웹 브라우저에 URL을 입력한다
- DNS 서버로부터 입력한 URL을 변환한 IP 주소를 받는다.
- 받은 IP 주소의 웹 서버 8080 포트에 JSP페이지를 요청한다.
- 웹 서버가 요청 내용을 분석하고 **서블릿 컨테이너**에 요청을 넘겨 처리한다.
- 화면에 보일 내용을 HTML 문서 형태로 웹 브라우저에 전송한다.

![Untitled](/assets/img/2022-11-18-JSP-&-Servelt/Untitled.png)

## Servelt이란?

### Servelt이란?

- 자바를 사용하여 웹을 만들기 위해 필요한 기술
- 클라이언트가 어떠한 요청을 하면 그에 대한 결과를 다시 전송해주어야하는데, 이러한 역할을 하는 자바 프로그램
- Contatiner가 이해할 수 있게 구성된 순수 자바 코드로만 이루어진 것

### Servelt 특징

- 클라이언트의 요청에 대해 동적으로 작동하는 웹 어플리케이션 컴포넌트
- html을 사용하여 요청에 응답한다.
- Java Thread를 이용하여 동작한다.
- MVC 패턴에서 Controller로 이용된다.
- HTTP 프로토콜 서비스를 지원하는 javax.servlet.http.HttpServlet 클래스를 상속받는다.
- UDP보다 처리 속도가 느리다.
- HTML 변경 시 Servlet을 재컴파일해야 하는 단점이 있다.

### Servelt 동작 방식

![Untitled](JSP%20&%20Servelt%208e10c1f5685243158dc2535efe9fbcf9/Untitled%201.png)

1. 사용자(클라이언트)가 URL을 입력하면 HTTP Request가 Servlet Container로 전송합니다.
2. 요청을 전송받은 Servlet Container는 HttpServletRequest, HttpServletResponse 객체를 생성합니다.
3. web.xml을 기반으로 사용자가 요청한 URL이 어느 서블릿에 대한 요청인지 찾습니다.
4. 해당 서블릿에서 service메소드를 호출할 후 클라이언트의 **GET, POST**여부에 따라 doGET() 또는 doPost()를 호출합니다.
5. doGet() 또는 doPost() 메소드는 동적 ㅍ이지를 생성한 후 HttpServletResponse객체에 응답을 보냅니다.
6. 응답이 끝나면 HttpServletRequest, HttpServletResponse 두 객체를 소멸시킵니다.

### ****Servlet 생명주기****

![Untitled](JSP%20&%20Servelt%208e10c1f5685243158dc2535efe9fbcf9/Untitled%202.png)

- 클라이언트의 요청이 들어오면 컨테이너는 해당 서블릿이 메모리에 있는지 확인하고, 없을 경우 init()메소드를 호출하여 적재합니다. init()메소드는 처음 한번만 싱행되기 때문에, 서블릿의 쓰레드에 공통적으로 사용해야하는 것이 있다면 오버라이딩하여 구현하면 됩니다. 실행 중 서블릿이 변경될 경우, 기존 서블릿을 파괴하고 init()을 통해 새로운 내용을 다시 메모리에 적재합니다.
- init()이 호출된 후 클라이언트의 요청에 따라서 service()메소드를 통해 요청에 대한 응답이 doGet()가 doPost()로 분기됩니다. 이때 서블릿 컨테이너가 클라이언트의 요청이 오면 가장 먼저 처리하는 과정으로 생성된 HttpServeltRequest, HttpServletResponse에 의해 request와 response객체가 제공됩니다.
- 컨테이너가 서블릿에 종료 요청을 하며 destroy()메소드가 호출되는데 마찬가지로 한번만 실행되며, 종료시에 처리해야하는 작업들은 destroy()메소드를 오버라이딩하여 구현하면 됩니다.

### Servlet Container(서블릿 컨테이너)

![Untitled](JSP%20&%20Servelt%208e10c1f5685243158dc2535efe9fbcf9/Untitled%203.png)

- 서블릿을 관리해주는 컨테이너
- 클라이언트의 요청(Request)을 받아주고 응답(response)할 수 있게, 웹서버와 소켓으로 통신
- 대표적인 예로 톰캣(Tomcat)

### Servlet Container  역할

- 웹서버와의 통신 지원
- 서블릿 생명주기(Life Cycle) 관리
- 멀티쓰레드 지원 및 관리
- 선언적인 보안 관리

## JSP 내장객체

### JSP 내장객체

- 기본적인 요청과 응답, 화면 출력, 세션, 페이지와 어플리케이션 등 모든 웹 프로그래밍에 있어 필수적인 기능
- **JSP 내에서 선언하지 않고 사용할 수 있는 객체**

![Untitled](JSP%20&%20Servelt%208e10c1f5685243158dc2535efe9fbcf9/Untitled%204.png)

### JSP 내장객체 특징

- 내장 객체는 jsp 페이지가 실행될 때 컨테이너가 자동으로 생성해준다. 별도로 선언하거나 객체로 생성하지 않아도 즉시 사용할 수 있는데 그 이유는 jsp의 실행 과정에서 찾을 수 있다.
- jsp는 실행될 때 자바 파일인 서블릿으로 변환되어 컴파일된다. 이 변환 과정에서 jspService()메서드가 생성이 되고 이 메서드안에 관련 코드가 삽입이된다.
- 내장 객체의 참조 변수를 컨테이너가 생성하는 부분이다.
    - 컨테이너가 미리 선언해놓은 참조 변수를 이용해 사용한다.
    - 별도의 객체 생성 없이 각 내장 객체의 메서드를 사용할 수 있다.
    - JSP문서 안의 <% 스크립틀릿 %> 과 <%= 표현식 %> 에서만 사용할 수 있다.
    - <%! 선언부 %> 에서는 즉시 사용하는 건 불가능하고, 매개변수로 전달받아 사용할 수는 있다.

### JSP 내장 객체 9가지

- **request** : 클라이언트의 http 요청정보를 저장하고 있는 객체
- **response** : 클라이언트의 요청에 대한 응답 정보를 저장하고 있는 객체
- **session** : 클라이언트가 서버에 접속했을 때 세션정보를 저장한 객체
- **pageContext** : 응답 페이지 실행에 필요한 Context정보를 저장한 객체
- **out** : 응답 페이지 전송을 위한 출력 stream
- **application** : 동일한 컨텍스트 정보를 저장하고 있는 객체
- **config** : 특정 페이지의 서블릿 설정 정보를 저장하고 있는 객체
- **page** : 특정 페이지의 서블릿 객체(인스턴스화된 객체)
- **exception** : 예외 처리를 위한 객체

![Untitled](JSP%20&%20Servelt%208e10c1f5685243158dc2535efe9fbcf9/Untitled%205.png)

## JSP 액션태그(include vs forward)

- **include**
    - **다른 페이지의 실행 결과를 현재 페이지에 포함시킬 때 사용**
    - <jsp:include page="포함될 페이지" flust="true" />
        - page 속성 : 현재 페이지에 결과가 포함될 페이지명
        - flush 속성 : 포함될 페이지로 제어가 이동될 때, 현재 포함하는 페이지가 지금까지 출력 버퍼에 저장한 결과를 처리하는 방법 결정

![Untitled](JSP%20&%20Servelt%208e10c1f5685243158dc2535efe9fbcf9/Untitled%206.png)

- **forward**
    - **현재 JSP 페이지에서 다른 페이지로 이동하는 태그**
    - JSP 컨테이너는 현재 JSP 페이지에서 forward 액션 태그를 만나면 그 전까지 출력 버퍼에 저장되어 있던 내용을 모두 삭제하고 f**orward 액션 태그에 설정된 페이지로 프로그램의 제어가 이동**
    - <jsp:forword page=”이동할 페이지 />

![Untitled](JSP%20&%20Servelt%208e10c1f5685243158dc2535efe9fbcf9/Untitled%207.png)

## JSP 커넥션 풀(Connection Pool)

### 커넥션 풀(Connection Pool)

- 웹 컨테이너(WAS)가 실행되면서 DB와 미리 연결(connection)을 해놓은 객체들을 pool에 저장해두었다가, 클라이언트 요청이 오면 connection을 빌려주고, 처리가 끝나면 다시 connection을 반납받아 pool에 저장하는 방식을 말합니다.
- DataBase Connection Pool로 DBCP라고도 한다.

![Untitled](JSP%20&%20Servelt%208e10c1f5685243158dc2535efe9fbcf9/Untitled%208.png)

### 커넥션 풀을 사용하는 이유

- Java - JDBC 대표적인 예제 소스를 보면 아래와 같은 방식으로 되어있다.

![Untitled](JSP%20&%20Servelt%208e10c1f5685243158dc2535efe9fbcf9/Untitled%209.png)

- 이러한 방식은 매번 사용자가 요청을 할 때마다 드라이버를 로드하고 커넥션 객체를 생성하여 연결하고 종료하기 때문에 비효율적이다.
- 따라서, 서버의 부하를 줄리고 효율성을 증가시키기 위해 커넥션 풀 방식을 사용한다.

### JSP 쇼핑몰 웹 프로젝트에 사용한 DBCP

- webapp > META-INF > context.xml

![Untitled](JSP%20&%20Servelt%208e10c1f5685243158dc2535efe9fbcf9/Untitled%2010.png)

- 상품 DAO

![Untitled](JSP%20&%20Servelt%208e10c1f5685243158dc2535efe9fbcf9/Untitled%2011.png)

## JSP에서 자바빈 사용하기

![Untitled](JSP%20&%20Servelt%208e10c1f5685243158dc2535efe9fbcf9/Untitled%2012.png)

# JSP 프로젝트

[Keyboard Market](https://www.notion.so/Keyboard-Market-a81e2861ac284f8faf511e797a1dad3b)
