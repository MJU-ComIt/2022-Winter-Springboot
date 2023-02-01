0201 스프링 강의
---
chap 09~12

##  1. OOP(객체지향 프로그래밍)의 5대 설계 법칙 -> SOLID
- 1. Single Responsibility Principle (SRP): 하나의 메서드는 하나의 책임만 진다.
- 2. Open-Closed Principle(OCP): 객체는 확장에겐 개방적, 수정에겐 폐쇄적
- 3. Liskov Substitution Principle(LSP): 자식은 언제나 부모를 대체할 수 있다
- 4. Interface Segregation Principle(ISP): 클라이언트가 자신이 이용하지 않는 메서드에는 의존하지 않아야 한다 -> 클라이언트가 꼭 필요한 메서드만 이용하도록 인터페이스를 나누어 만든다
 - 5. Dependency Inversion Principle(DIP): 객체는 저수준의 모듈보다 고수준의 모듈에 의존해야 한다 -> 저수준은 구체적인 구현된 클래스를 의미하며 고수준은 인터페이스와 같이 추상적인 클래스
 
## 2. 관심사의 분리 (Speration of Concerns)와 MVC패턴
 - 관심사의 분리는 SRP를 지키기 위함
 - 하나의 메서드에 있는 입력, 계산, 출력 3가지 기능을 분리시키는 것과 같다
 - 분리해야 하는 3가지 사항 
   - 1. 관심사 (해야할 작업) 2. 변하는 것과 변하지 않는 것 3. 공통(중복)코드
 
### 1) 입력의 분리
 - HttpServletRequest의 getParameter를 반복하여 받아온 것을 데이터 입력값을 매개변수로 한번에 가져올 수 있다.
 - 이때, 데이터 값을 원하는 타입으로 변환하는 것도 자동으로 해줌
 
### 2)  출력의 분리 - 스프링의 MVC패턴
- 매개변수로 받아온 데이터 값을 바로 출력에 넣을 수도 있지만 별도의 메서드로 분리된 경우에는 접근이 불가하기에 MVC패턴으로
- 입력과 출력을 연결하는 Model ->
입력된 데이터를 Model에 저장하고 출력하는 부분으로 Model을 전달하여 Model에 저장된 값을 출력
- 사용자의 요청이 들어오면 DispatcherServlet이 Model을 사용하여 입력을 처리하고 해당 컨트롤러에게 전달 후 반환된 값을 출력 부분에게 전달 후 다양한 형태의 View를 클라이언트에게 응답

### 3) View로 JSP가 반환 
-   기본적으로 스프링에서 컨트롤러 메서드의 반환 타입이 String인 경우 해당 문자열의 JSP가 반환되는 이유는 스프링에 반환되는 문자열과 같은 View 파일이 있을 경우 접두사와 접미사에 각각 경로와 JSP를 붙여서 반환하기 때문
- 반환 타입이 void인 경우엔 메서드의 RequestMapping의 이름과 같은 View가 반환

### 4) Expression Language
- 값이 출력될 공간을 만들기 위함으로 Model 객체가 가진 데이터 값을 출력
- JSP는 ${Model의 key 값}으로 나타내면 해당 key의 value가 해당 자리에 출력됨

### 5) Model을 사용하여 View 출력
- 매개변수에 Model을 추가하여 DispatcherServlet가 입력을 처리할 때 Model 생성
- 매개변수로 받아온 model에 입력된 데이터 값을 저장 후 View를 반환

### 6) ModelAndView
- Model 대신에 ModelAndView를 활용하여 출력
- 이 경우 메서드의 반환 타입은 ModelAndView
- ModelAndView에 데이터 값을 저장하고, View의 이름을 지정한 뒤 반환하여 사용

## 3.  매개변수 이름 가져오는 방식
- 1. Reflection API
  - getParameters로 해당 메서드의 매개변수 목록 가져오기
  <br>
- 2. Class File
  - 네비게이터로 프로젝트를 탐색하면 Src와 Target 폴더가 있음
  - Src 폴더는 java 파일이고 Target 폴더는 class 파일
  - class 파일을 보면 매개변수를 볼 수 있음

## 4. Map

### 1) Map과 HashMap이란?
- map과 hashMap의 차이는 map은 인터페이스라 객체로 생성이 불가하여 map 컬렉션인 hashMap으로 객체 생성
-  결국, hashMap은 map을 상속하였기에 map의 성질을 그대로 가짐
- map은 key와 value로 이루어진 Entry객체를 저장하는 구조를 가지고 있는 자료구조
- key와 value는 모두 객체로 key는 중복 저장이 불가이지만 value는 중복 저장 가능

### 2) hashMap 메서드
-  생성: 키 타입과 값 타입을 파라미터로 주고 기본 생성자 호출 
ex) HashMap<String, String> map = new  HashMap<String, String>();
- 값 추가: put(key, value) 
- 하나의 값 삭제: remove(key)
- 전체 삭제: clear( )
- 값 출력: get(key)

### 3) 반복 출력
- 반복문으로 entrySet( ) 또는 keySet( )으로 출력
- Iterator 사용
ex) 
Iterator<Entry<String, String>> entries = map.entrySet().iterator()
Iterator<String.> keys = map.keySet().iterator()
- entrySet( )은 key와 value로 이루어지고
- keySet( )은 key로 이루어짐