# 0126_JangSoyun

# 이론

open jdk → 오라클이 아닌 다른 회사 (redhat, IBM등)이 만든 오픈소스

GA → General Availibility 의 약자, 안정된 버전이라고 보면 된다.

IDE → integrated development environment 인터프리터, 컴파일러 등 따로 있는걸 모두 합쳐놓은 통합개발 환경

STS3(Eclipse + Spring 플러그인)은 spring, springboot 가능

IntelliJ 

Tomcat 웹서버용

## Java spec

---

### SE

Standard, 일반

### EE

Enterprise, 서버용, 톰캣은 이를 준수한다.

### ME

micro, 소형기기를 위한(ATM등) 

## AWS란?

아마존이 제공하는 클라우드 서비스, 사용한 만큼만 지불하면 됨.

관리가 쉽고, 확장성이 유연하다. 보안도 대신 관리해준다.

### 클라우드 서비스

클라우드 컴퓨팅으로 서비스를 제공하는 것. 

클라우드는 인터넷을 의미한다. 인터넷을 통해서 엄청 많은 서버를 이용한다.

서버와 클라이언트 사이 클라우드 서비스들을 이용해서 자원을 사용한다. 

중간에 클라우드 서비스가 껴있으면 요청하는 만큼 자원을 사용할 수 있다.

### 유연한 확장성

작업을 하다가 자원이 모자라면, AWS의 더 많은 컴퓨터를 사용할 수 있게 한다.

하드웨어 추상화에서 오는 개념인데, 추상화는 구체화의 반대이다.

## Amazon EC2

웹 호스팅에 해당하는 것. AWS에 가상 컴퓨터(버츄얼 머신)을 만든다.

가상컴퓨터에 윈도우즈를 설치하고, 톰캣을 설치하여 웹브라우저를 통해 이곳에 접속해본다.

## Amazon S3

Simple Storage Service의 약자, 데이터 공간을 제공한다.

확장성, 가용성, 내구성을 가진다.

- 확장성: 우리가 필요하면 더 많은 공간을 쓸 수 있는거.
- 가용성: 저장 공간을 여러 서버에서 공유할 수 있는 것.
- 내구성: 데이터가 깨지면 복구해줌.

## Amazon RDS

관계형 DB 관리 서비스이다. (Relational Database Service)

오라클이나 mySQL 를 사용할 수 있게 해주고, 메모리등을 모니터링해주고, 주기적으로 백업도 해준다.

아마존에서 DB를 구축하려면 두 가지 방법이 있다.

- 가상 컴퓨터를 설치하고, DB를 직접 설치→ 이게 Amazon EC2임.
- 아마존에서 제공하는 RDS 를 이용

## 관련 용어

### on-Premise

서버를 직접 운영하는 것, 직접 다 관리하는 거라 관리자가 필요하다. 

회사들이 직접 서버를 운영하기도 하지만, 대형 IDC를 이용함. 

IDC: 인터넷 데이터 센터

- 이번에 카카오 불난곳이 IDC임

### Serverless

서버가 없다는 게 아닌, RDS같은 서비스를 이용하는 걸 말한다. 서버 작업을 직접 하지 않는다.

- DB구축하는 방법
    
    1) EC2안에 직접 설치
    
    2) 아마존 RDS사용
    

### Region

데이터 센터가 물리적으로 존재하는 곳. 

서울에도 생김. 

### CDN

정적 리소스(자주사용하는 이미지 등)을 빠르게 제공할 수 있게.. 해주는 서비스.

로컬프로그램 커맨드 라인에 적고 엔터를 치면 실행된다.

```java
public class Main{
	public static void main(String[] args){
		System.out.println("Hello");
	}
}
```

자바 인터프린터가 메인 클래스에 있는 메인 메서드를 호출을 한다

- 자바 인터프린터가 메인 메서드를 호출할 수 있는 이유는, 메인 메서드가 static이기 때문이다.
    
    static이 아니면 객체를 생성해야하는데, static이면 객체를 생성할 필요가 없으므로 바로 호출할 수 있다.
    

## 원격프로그램 실행

---

원격프로그램을 실행하려면 원격컴퓨터에는 WAS(톰캣)이 필요하고, 내 컴퓨터에는 브라우저가 필요하다. 

원격프로그램 실행 매커니즘은 다음과 같다.

1. `브라우저` ’ip주소:포트번호’ 호출 (=`톰캣`에게 요청)
2. `톰캣` 해당 프로그램 실행

### 원격프로그램 실행해보기

외부에서 브라우저로 서버에 있는 프로그램을 실행하려면 두가지 작업이 필요하다.

1. 원격 호출 가능한 프로그램으로 등록 (@Controller)
2. URL과 main메서드(프로그램) 연결 (@RequestMapping)

```java
@Controller
public class Hello{
	@RequestMapping("/hello")
	public void main(){
		System.out.println("Hello");
	}
}
```

서버를 실행 중인 컴퓨터에서 브라우저에 ip주소:포트번호/context root/url를 입력하면 프로그램이 실행된다. 요청받은 원격컴퓨터가 메인메서드를 수행한다.

- context root 는 프로젝트 이름이다.
- url은 @RequestMapping(”/hello”) 에서 hello이다.

### Static main() vs Instance main

아래처럼 main()이 Static이 아니어도 호출할 수 있다.

```java
@Controller
public class Hello{
	@RequestMapping("/hello")
	public void main(){
		System.out.println("Hello");
	}
}
```

instance 메서드는 객체를 생성한 후 호출할 수 있다. 톰캣 내부에서 객체를 생성해준 다음 호출하기 때문이다.

static 메서드는 instance멤버를 쓸 수 없기 때문에 웬만하면 instance메서드로 하는게좋다.

instance메서드는 static멤버와 instance멤버를 모두 사용할 수 있다.

### Reflection API

public이 아닌 private이어도 서버에서 호출이 가능하다.

RequestMapping은 접근제한자에 상관없이 외부에서 접근이 가능하도록 한다.

→ 클래스 정보를 얻고 다룰 수 있는 강력한 기능을 제공하는 Reflection API(java.lang.reflact 패키지)를 사용하기 때문임.

그러나 서버가 아닌 다른 패키지의 클래스가 private클래스에 접근하지 못하는데, Class.forName(”클래스의 정보를 담고있는 객체”)를 이용하여 객체를 만들 수 있다.

```dart
Class helloClass = Class.forName("com.fastcampus.ch2.hello");
Hello hello = (Hello)helloClass.newInstance(); //Class 객체가 가진 정보로 객체생성
Method main = helloClass.getDeclaredMethod("main"); //메서드 참조
main.setAccessible(true); // main 호출 가능하게 함
main.invoke(hello); //hello.main() 호출
```