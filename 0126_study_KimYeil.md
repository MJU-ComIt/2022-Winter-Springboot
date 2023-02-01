0126 스프링 강의
---
chap 01~08
## 1. 원격 프로그램 실행

- 원격으로 webApp을 실행하기 위해서는 브라우저와 톰캣과 같은 WAS가 있어야 함
- @Controller를 통해 프로그램을 등록하고,  
	@RequestMapping을 통해 URL과 프로그램을 연결한다
- 인스턴스 메서드 임에도 객체 생성을 하지 않고도 메서드 호출이 가능한 이유는 
	톰캣 내부에서 스프링이 reflectionAPI를 통해 객체를 생성하는 과정이 있기에 가능

## 2. HTTP 요청과 응답

### 1) HttpServletRequest
- URL을 요청하면 톰캣이 HttpServletRequest 객체를 만들고, 요청 정보를 담는다 
- 정보를 담은 객체를 Main 메서드의 매개변수로 전달하고, HttpServletRequest 를 
	사용하여 요청 정보에 대해 얻을 수 있다
	
### 2) HttpServletRequest와 HttpServletResponse
- HttpServletRequest의 getScheme( ), getServerName( )...등 여러 함수를 통해 해당 URL의 요청 정보를 얻을 수 있다
- QueryString은 값을 전달할 때 사용하는 것으로 name = value 형식인 문자열이다
- HttpServletResponse은 출력할 때 사용하며 브라우저로 바로 입력하는 방식이다

### 3) 리소스의 종류
- 리소스에는 동적 리소스와 정적 리소스 두 가지가 있다
- 동적 리소스는 실행할 때마다 결과가 변하는 리소스로 프로그램의 결과, 스트리밍 서비스 같은 것들이 있고,
- 정적 리소스는 이미지처럼 변하지 않고 그대로 있는 리소스이다

## 3. 클라이언트와 서버

### 1) 클라이언트와 서버란?
- Client는 서비스를 요청하는 애플리케이션이고, 
- Server는 서비스를 제공하는 애플리케이션으로 역할에 따라 구분한다
- Client가 서버 주소인 URL을 요청하면 Server는 text문서 문자열인 html로 응답하고, 	브라우저가 화면에 출력하는 것이다

###  2) 서버의 종류
- 어떤 서비스를 제공하는 지에 따라 서버가 다르다
- Ex) Email Server, File Server, Web Server

### 3) 서버의 포트
- 1대의 PC에서 하나의 IP 주소를 가지고 여러 서버를 이용하기 위해서는 포트번호가 필요하다. 포트번호를 통해 서버를 구분하는 것이다

### 4) 웹 애플리케이션(WAS)
- 웹 애플리케이션을 서비스하는 서버이다
- 애플리케이션은 프로그램을 의미하고, 서버에 프로그램을 설치하여 클라이언트가 사용할 수 있도록 한다

### 5) Tomcat의 내부 구조
- 사용자가 8080 포트로 요청하면 기다리고 있는 쓰레드가 처리한다
- 톰캣 내부는 Server, Service, Engine, Host, Context, Servelet 순으로 구성되어 있다
- Server에 기다리고 있는 쓰레드가 있고, Service에는 프로토콜 종류에 따라서 달라지는 Connector가 있고 Engine에게 전달한다
- Engine에는 Host가 존재하며 보통 하나의 서버에 하나의 Host가 있다
- Host 안에는 여러 개의 Context가 있을 수 있고, Context 하나가 바로 하나의 웹 애플리케이션이다

##  4. HTTP 요청과 응답-이론

### 1) 프로토콜
- 서로 간의 통신을 위한 약속, 규칙
- 주고받을 데이터에 대한 형식을 정의한 것

### 2) HTTP(Hyper Text Transfer Protocol)
- 텍스트 기반의 프로토콜로, 단순하고 읽기 쉽다
- 상태를 유지하지 않는 특징으로 클라이언트의 정보 저장 X
	--> 이를 보완하기 위해서 쿠키와 세션을 사용
- 커스텀 헤더를 추가하는 것과 같이 확장이 가능하다

### 3) HTTP 메시지
- 헤더와 바디로 구성되어 있다
- HTTP는 요청 메시지를 자동으로 구성하여 서버에 전달하고, 서버가 응답하는 응답 메시지에도 헤더와 바디로 구성하여 전달된다

### 4) 응답 메시지
- 1xx: Information
- 2xx: Success
- 3xx: Redirect (다른 URL 요청)
- 4xx: Client Error (클라이언트 잘못)
- 5xx: Server Error (서버 처리 중 오류)

### 5) 요청 메시지 & HTTP 메서드 (GET, POST)
- 요청 메서드로 GET과 POST
-  GET 
   - 서버에서 정보를 얻어오기 위함, 바디 X, 헤더로만 구성
   - 쿼리 스트링을 통해 데이터를 전달 (소용량 유리)
   - URL에 노출되므로 보안에 취약
   - 데이터 공유에 유리
   - Ex) 검색엔진
   
  - POST
    - 서버에 정보를 제공, 헤더와 바디로 구성, 내용은 바디에 작성
    - 전송 데이터 크기의 제한 X (대용량 유리)
    - HTTP와 TLS를 합친 HTTPS를 사용한 경우 보안에 유리
    - 데이터 공유는 불리
    - Ex) 글쓰기, 회원관리

## 5. 텍스트 파일 vs 바이너리 파일
- 텍스트 파일: 문자만으로 저장되어 있는 파일  -> 숫자를 문자로 변환 후 쓴다
- 바이너리 파일: 문자와 숫자가 저장되어 있는 파일 ->  데이터 있는 그대로 읽고 쓴다

## 6. MIME (Multipurpose Internet Mail Extensions)
- 텍스트 기반의 프로토콜에 바이너리 데이터를 전송하기 위해서 만들어짐
- HTTP의 Content-type 헤더에 데이터의 타입을 명시하는 방식으로 사용
- 타입 예시) text, image, audio, video, application
- Ex) HTML을 작성하기 위해 setContentType(“text/html’)과 같이 명시

## 7. BASE 64 (64진법)
- 바이너리 데이터를 텍스트 데이터로 변환할 때 사용
- 64개의 심볼을 사용(0 ~ 1, A ~ Z, a ~ z, +, /)
- 데이터의 크기가 커지는 단점이 있음
