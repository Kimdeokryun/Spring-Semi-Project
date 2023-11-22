# Spring-20231110
Spring Project

- [Spring-20231110](#spring-20231110)
- [](#)
  - [소개](#소개)
    - [간단한 웹 애플리케이션 개발](#간단한-웹-애플리케이션-개발)
    - [프로젝트 사용 기술](#프로젝트-사용-기술)
  - [프로젝트 환경설정 1110](#프로젝트-환경설정-1110)
    - [프로젝트 생성](#프로젝트-생성)
    - [Project](#project)
    - [IntelliJ Gradle 대신에 자바 직접 실행](#intellij-gradle-대신에-자바-직접-실행)
    - [단축키 검색](#단축키-검색)
    - [라이브러리 살펴보기](#라이브러리-살펴보기)
      - [스프링 부트 라이브러리](#스프링-부트-라이브러리)
      - [테스트 라이브러리](#테스트-라이브러리)
    - [View 설정](#view-설정)
      - [Welcome Page](#welcome-page)
      - [thymeleaf 템플릿 엔진](#thymeleaf-템플릿-엔진)
      - [참고](#참고)
    - [빌드하고 실행하기](#빌드하고-실행하기)
      - [만약 잘 안 된다면.](#만약-잘-안-된다면)
  - [스프링 웹 개발 기초](#스프링-웹-개발-기초)
    - [정적 컨텐츠](#정적-컨텐츠)
      - [스프링 부트 정적 컨텐츠 기능](#스프링-부트-정적-컨텐츠-기능)
    - [MVC와 템플릿 엔진](#mvc와-템플릿-엔진)
    - [API](#api)
  - [회원 관리 예제 -백엔드 개발](#회원-관리-예제--백엔드-개발)
    - [비즈니스 요구사항 정리](#비즈니스-요구사항-정리)
      - [일반적인 웹 애플리케이션 계층 구조](#일반적인-웹-애플리케이션-계층-구조)
      - [클래스 의존관계](#클래스-의존관계)
    - [회원 도메인과 리포지토리 만들기](#회원-도메인과-리포지토리-만들기)
      - [회원 객체](#회원-객체)
    - [회원 리포지토리 테스트 케이스 작성](#회원-리포지토리-테스트-케이스-작성)
      - [테스트 주도 개발](#테스트-주도-개발)
    - [회원 서비스 개발](#회원-서비스-개발)
    - [회원 서비스 테스트](#회원-서비스-테스트)
  - [스프링 빈과 의존관계](#스프링-빈과-의존관계)
    - [컴포넌트 스캔과 자동 의존관계 설정](#컴포넌트-스캔과-자동-의존관계-설정)
      - [회원 컨트롤러에 의존관계 추가](#회원-컨트롤러에-의존관계-추가)
      - [오류 발생](#오류-발생)
      - [스프링 빈을 등록하는 2가지 방법](#스프링-빈을-등록하는-2가지-방법)
      - [회원 서비스 스프링 빈 등록](#회원-서비스-스프링-빈-등록)
      - [회원 리포지토리 스프링 빈 등록](#회원-리포지토리-스프링-빈-등록)
    - [자바 코드로 직접 스프링 빈 등록하기](#자바-코드로-직접-스프링-빈-등록하기)
  - [회원 관리 예제 - 웹 MVC 개발](#회원-관리-예제---웹-mvc-개발)
    - [회원 웹 기능 - 홈 화면 추가](#회원-웹-기능---홈-화면-추가)
    - [회원 웹 기능 - 등록](#회원-웹-기능---등록)
    - [회원 웹 기능 - 조회](#회원-웹-기능---조회)
  - [스프링 DB 접근 기술](#스프링-db-접근-기술)
    - [H2 데이터베이스 설치](#h2-데이터베이스-설치)
    - [순수 JDBC](#순수-jdbc)
      - [환경 설정](#환경-설정)
      - [Jdbc 리포지토리 구현](#jdbc-리포지토리-구현)
    - [스프링 통합 테스트](#스프링-통합-테스트)
    - [스프링 JdbcTemplate](#스프링-jdbctemplate)


#

## 소개

### 간단한 웹 애플리케이션 개발

- 스프링 프로젝트 생성
- 스프링 부트로 웹 서버 실행
- 회원 도메인 개발
- 웹 MVC 개발
- DB 연동 - JDBC, JPA, 스프링 데이터 JPA
- 테스트 케이스 작성


### 프로젝트 사용 기술

- Spring Boot
- JPA (Java Persistence API)
- Gradle
- HIBERNATE
- Thymeleaf
- Apache Tomcat


## 프로젝트 환경설정 1110

### 프로젝트 생성
- Java 11 설치  (해당 프로젝트는 17설치)
- IDE: IntelliJ or Eclipse

스프링 부트 스타터 사이트 이동 후 스프링 프로젝트 생성
https://start.spring.io

- 프로젝트 선택
  - Project: Gradle Project
  - Spring Boot: 2.3.x (해당 프로젝트는 3.1.x)
  - Language: Java
  - Packaging: Jar
  - Java: 11 (해당 프로젝트는 17)
- Project Metadata
  - groupid: hello
  - artifactid: hello-spring
- Dependencies: Spring Web, Thymeleaf


### Project
Maven, Gradle 이란?

필요한 라이브러리가 담겨 있으며, build하는 lifecycle까지 관리해주는 Tool이다.

최근에는 Gradle로 많이 사용한다.

### IntelliJ Gradle 대신에 자바 직접 실행
최근 IntelliJ 버전은 Gradle을 통해서 실행 하는 것이 기본 설정이다.

이렇게 하면 실행속도가 느리다. 

다음과 같이 변경하면 자바로 바로 실행해서 실행속도가 더 빠르다.

![Alt text](./images/perference.png)


### 단축키 검색

 Refactor This의 윈도우 단축키는 Ctrl + Alt + Shift + T

### 라이브러리 살펴보기
> Gradle은 의존관계가 있는 라이브러리를 함께 다운로드 한다.
#### 스프링 부트 라이브러리
- spring-boot-starter-web
- spring-boot-starter-tomcat: 톰캣 (웹서버)
- spring-webmvc: 스프링 웹 MVC
- spring-boot-starter-thymeleaf: 타임리프 템플릿 엔진(View)
- spring-boot-starter(공통): 스프링 부트 + 스프링 코어 + 로깅
- spring-boot
- spring-core
- spring-boot-starter-logging
- logback, slf4j  (https://velog.io/@woply/spring-SLF4J%EC%99%80-Logback%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%B4-%EB%A1%9C%EA%B7%B8-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)
#### 테스트 라이브러리
- spring-boot-starter-test
- junit: 테스트 프레임워크
- mockito: 목 라이브러리
- assertj: 테스트 코드를 좀 더 편하게 작성하게 도와주는 라이브러리
- spring-test: 스프링 통합 테스트 지원


### View 설정

#### Welcome Page

스프링 부트가 제공하는 Welcome Page 기능

- static/index.html 을 올려두면 Welcome page 기능을 제공한다.


#### thymeleaf 템플릿 엔진

- thymeleaf 공식 사이트: https://www.thymeleaf.org/

th 는 thymeleaf를 말함.
```
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
  <title>Hello</title>
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
<p th:text="'안녕하세요. ' + ${data}" >안녕하세요. 손님</p>
</body>
</html>
```

index.html -> hello.html 로 이동 시에 data를 넘겨주는 방식.    but hello.html은 static 폴더가 아닌 templates 폴더에 있어야 한다.
```
@GetMapping("hello")
    public String hello(Model model){
        model.addAttribute("data", "Hello!!");
        return "hello";
    }
```

Controller에서 return 값으로 문자("hello")를 반환하면. viewResolver가 화면을 찾아서 처리한다.
- 스프링 부트 템플릿엔진 기본 viewName 매핑


#### 참고
spring-boot-devtools 라이브러리를 추가하면, html 파일을 컴파일만 해주면 서버 재시작 없이 View 파일 변경이 가능하다.

> 인텔리J 컴파일 방법: 메뉴 build Recompile


### 빌드하고 실행하기

해당 프로젝트 파일로 이동.

`gradlew build`
`cd build/libs`
`java -jar hello-spring-0.0.1-SNAPSHOT.jar`

실행 확인.

#### 만약 잘 안 된다면.
`gradlew clean build`


## 스프링 웹 개발 기초

### 정적 컨텐츠

#### 스프링 부트 정적 컨텐츠 기능
https://docs.spring.io/spring-boot/docs/2.3.1.RELEASE/reference/html/spring-boot-features.html#boot-features-spring-mvc-static-content

정적 콘텐츠는 /static (or /public or /resources or /META-INF/resources) 라고 부르는 폴더에서 전달한다.

해당 정적 콘텐츠(`hello-static.html`)에 접근하기 위해선 `http://localhost:8080/hello-static.htm` 로 접속

### MVC와 템플릿 엔진

MVC (Model View Controller)

```
    @GetMapping("hello-mvc")
    public String helloMVC(@RequestParam("name") String name, Model model){
        model.addAttribute("name", name);
        return "hello-template";
    }
```
`http://127.0.0.1:8081/hello-mvc?name=spring`

name param에 값을 전달하면 html에 해당 name의 값이 뜬다.

required는 default값이 true이다.

그렇기에 param을 전달하지 않으면, `Required request parameter 'name' for method parameter type String is not present` 해당 에러가 뜬다.

`return "hello-template";` hello-template.html을 /template 폴더에서 찾아서 Thymeleaf 템플릿 엔진 처리 후 변환해서 return 한다.


### API

`http://127.0.0.1:8081/hello-string?name=spring`
```
    @GetMapping("hello-string")
    @ResponseBody
    public String helloString(@RequestParam("name") String name){
        return "hello " + name;
    }
```
`hello spring` 값을 return 한다.


String 이 아닌 class 객체를 넘겨준다면?

`http://127.0.0.1:8081/hello-api?name=spring`
```
    @GetMapping("hello-api")
    @ResponseBody
    public Hello helloApi(@RequestParam("name") String name){
        Hello hello = new Hello();
        hello.setName(name);
        return hello;
    }

    static class Hello
    {
        private String name;

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }
    }
```

`{"name":"spring"}`  해당 하는 것 처럼 json 형태로 return 한다.

`@ResponseBody` 로 해당 값을 return 한다.  html형태가 아닌.
HttpMessageConverter에서 객체는 `JsonConverter` or String은 `StringConverter`로 처리해서 return 한다.



## 회원 관리 예제 -백엔드 개발

### 비즈니스 요구사항 정리

- 데이터: 회원ID, 이름
- 기능: 회원 등록, 조회
- 아직 데이터 저장소가 선정되지 않음(가상의 시나리오)


#### 일반적인 웹 애플리케이션 계층 구조
- 컨트롤러: 웹 MVC의 컨트롤러 역할
- 서비스: 핵심 비즈니스 로직 구현
- 리포지토리: 데이터베이스에 접근, 도메인 객체를 DB에 저장하고 관리
- 도메인: 비즈니스 도메인 객체, 예) 회원, 주문, 쿠폰 등등 주로 데이터베이스에 저장하고 관리됨

#### 클래스 의존관계
- 아직 데이터 저장소가 선정되지 않아서, 우선 인터페이스로 구현 클래스를 변경할 수 있도록 설계
- 데이터 저장소는 RDB, NoSQL 등등 다양한 저장소를 고민중인 상황으로 가정
- 개발을 진행하기 위해서 초기 개발 단계에서는 구현체로 가벼운 메모리 기반의 데이터 저장소 사용


### 회원 도메인과 리포지토리 만들기

#### 회원 객체

Optional: 요즘에는 null을 처리하는 방법에서 null을 그대로 반환하는 방법 대신 Optional이라는 것으로 감싸서 반환하는 방법을 많이 선호함.

동시성 문제: 실무에서는 동시성 문제가 있을 수 있어서 공유되는 변수의 경우 concurrent HashMap을 사용해야 하지만 예제에서는 단순하게 HashMap을 사용.

Optional.ofNullable(): return 값이 null이여도 Optional에 null이 포함되어 return이 가능하고 이는 클라이언트 부분에서 활용할 수 있음.

반복문을 통해 name값과 동일한 값을 넘겨줌. 없다면 위의 기능처럼 Optional에 null이 포함되어서 반환
```
store.values().stream()
                .filter(member -> member.getName().equals(name))
                .findAny();
```


### 회원 리포지토리 테스트 케이스 작성
개발한 기능을 실행해서 테스트 할 때 자바의 main 메서드를 통해서 실행하거나, 웹 애플리케이션의
컨트롤러를 통해서 해당 기능을 실행한다. 이러한 방법은 준비하고 실행하는데 오래 걸리고, 반복 실행하기
어렵고 여러 테스트를 한번에 실행하기 어렵다는 단점이 있다. 자바는 JUnit이라는 프레임워크로 테스트를
실행해서 이러한 문제를 해결한다.


```        
System.out.println("resullt = " + (result == member));
Assertions.assertEquals(result, member);
```

Assertions.assertEquals를 통해서 같다면 아무런 출력을 하지 않고 다르다면 아래의 문구를 볼 수 있다.
```
org.opentest4j.AssertionFailedError: 
Expected :com.hello.hellospring.domain.Member@214b199c
Actual   :null
<Click to see difference>
중략....
```

최근에는 `Assertions.assertThat(member).isEqualTo(result);` 를 더 많이 사용함

`Assertions.assertEquals`는 `import org.junit.jupiter.api.Assertions;` 를,
`Assertions.assertThat`는 `import org.assertj.core.api.Assertions;`를 import 한다.

static import `import static org.assertj.core.api.Assertions.*;`를 통해서

해당 메소드를 `assertThat(member).isEqualTo(result);` 이렇게 줄여서 사용 할 수 있다.



Test case class 에서 각 test function 별 의존관계를 없애기 위해선
test 를 위해 저장한 데이터를 clear해야함.

각 test 함수 실행 마다 실행하는 annotation @AfterEach
```
    @AfterEach
    public void afterEach(){
        repository.clearStore();
    }
```
repository class에서는 해당 func를 작성.
```
    public void clearStore(){
        store.clear();
    }
```

#### 테스트 주도 개발
테스트를 먼저 만들고 구현 클래스를 만들어서 돌려보는 것을 TDD(테스트 주도 개발)라고 한다.

-> 소스코드가 굉장히 길어지고 많아진다면 테스트 코드 없이 개발하기가 거의 불가능하다.
-> 그러므로 테스트 관련해서는 깊이 있게 공부해야한다.


### 회원 서비스 개발

ctrl + alt + v (command + option + v) -> 해당 return 값으로 생성.

`extract method` 를 통해 메서드 분리.

### 회원 서비스 테스트

ctrl + shift + t (command + shift + t) -> 개발된 서비스 부분에서 test class 생성

test 함수 이름은 한글로도 작성하기도 한다.


- 테스트 케이스 작성법

  // given -> 이 데이터를 기반

  // when  -> 이것을 검증

  // then  -> 검증부

## 스프링 빈과 의존관계

### 컴포넌트 스캔과 자동 의존관계 설정

회원 컨트롤러가 회원서비스와 회원 리포지토리를 사용할 수 있게 의존관계를 준비하자

#### 회원 컨트롤러에 의존관계 추가

- 생성자에 @Autowired 가 있으면 스프링이 연관된 객체를 스프링 컨테이너에서 찾아서 넣어준다. 이렇게
객체 의존관계를 외부에서 넣어주는 것을 DI (Dependency Injection), 의존성 주입이라 한다.

- 이전 테스트에서는 개발자가 직접 주입했고, 여기서는 @Autowired에 의해 스프링이 주입해준다

#### 오류 발생
```
Consider defining a bean of type 'hello.hellospring.service.MemberService' in 
your configuration.
```

memberService가 스프링 빈으로 등록되어 있지 않다.

#### 스프링 빈을 등록하는 2가지 방법

- 컴포넌트 스캔과 자동 의존관계 설정
- 자바 코드로 직접 스프링 빈 등록하기

컴포넌트 스캔 원리

- @Component 애노테이션이 있으면 스프링 빈으로 자동 등록된다.
- @Controller 컨트롤러가 스프링 빈으로 자동 등록된 이유도 컴포넌트 스캔 때문이다.
- @Component 를 포함하는 다음 애노테이션도 스프링 빈으로 자동 등록된다.
  - @Controller
  - @Service
  - @Repository

#### 회원 서비스 스프링 빈 등록
 참고: 생성자에 @Autowired 를 사용하면 객체 생성 시점에 스프링 컨테이너에서 해당 스프링 빈을 찾아서
주입한다. 생성자가 1개만 있으면 @Autowired 는 생략할 수 있다.

-> Dependency Injection

#### 회원 리포지토리 스프링 빈 등록

- memberService 와 memberRepository 가 스프링 컨테이너에 스프링 빈으로 등록되었다.

> 참고: 스프링은 스프링 컨테이너에 스프링 빈을 등록할 때, 기본으로 싱글톤으로 등록한다(유일하게 하나만
등록해서 공유한다) 

따라서 같은 스프링 빈이면 모두 같은 인스턴스다. 설정으로 싱글톤이 아니게 설정할 수
있지만, 특별한 경우를 제외하면 대부분 싱글톤을 사용한다.
  

### 자바 코드로 직접 스프링 빈 등록하기

- 회원 서비스와 회원 리포지토리의 @Service, @Repository, @Autowired 애노테이션을 제거하고
진행한다.

memberservice 와 memberRepository도 Spring Bean에 올려준다.


```
@Configuration
public class SpringConfig {

    @Bean
    public  MemberService memberService() {
        return new MemberService(memberRepository());
    }

    @Bean
    public MemberRepository memberRepository() {
        return new MemoryMemberRepository();
    }
}
```

- XML로 설정하는 방식도 있지만 최근에는 잘 사용하지 않으므로 생략
- Dependency Injection에는 필드 주입, setter 주입, 생성자 주입 이렇게 3가지 방법이 있다. 의존관계가 실행중에
동적으로 변하는 경우는 거의 없으므로 생성자 주입을 권장
- 실무에서는 주로 정형화된 컨트롤러, 서비스, 리포지토리 같은 코드는 `컴포넌트 스캔`을 사용한다. 
그리고 정형화 되지 않거나, 상황에 따라 구현 클래스를 변경해야 하면 설정을 통해 `스프링 빈`으로
등록한다

주의: @Autowired 를 통한 DI는 helloController , memberService 등과 같이 스프링이 관리하는
객체에서만 동작한다. 스프링 빈으로 등록하지 않고 내가 직접 생성한 객체에서는 동작하지 않는다.

스프링 컨테이너, DI 관련된 자세한 내용은 스프링 핵심 원리 강의에서 설명한다.


## 회원 관리 예제 - 웹 MVC 개발

MVC(Model View Controller)


### 회원 웹 기능 - 홈 화면 추가

컨트롤러가 정적 파일보다 우선순위가 높다.

### 회원 웹 기능 - 등록

- return "redirect:/";
/ 으로 redirect

- `createMemberForm.html`

name="name" 에서 "name" 은 spring 에서의 key다.

### 회원 웹 기능 - 조회

- `memberList.html`
<tr th:each="member : ${members}">

에서는 members model의 개수 만큼 loop

메모리에 저장되어 있기 때문에 어플리케이션 재실행 시 데이터는 초기화.

이를 위해 데이터베이스를 사용한다.


## 스프링 DB 접근 기술

### H2 데이터베이스 설치

### 순수 JDBC

#### 환경 설정

`build.gradle 파일에 jdbc, h2 데이터베이스 관련 라이브러리 추가`

```
implementation 'org.springframework.boot:spring-boot-starter-jdbc'
runtimeOnly 'com.h2database:h2'
```

`스프링 부트 데이터베이스 연결 설정 추가 (resources/application.properties)`

```
spring.datasource.url=jdbc:h2:tcp://localhost/~/test
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
```


#### Jdbc 리포지토리 구현
주의! 이렇게 JDBC API로 직접 코딩하는 것은 20년 전 이야기이다. 따라서 고대 개발자들이 이렇게
고생하고 살았구나 생각하고, 정신건강을 위해 참고만 하고 넘어가자.


기존 구현
```
        
        String sql = "insert into member(name) values(?)";

        Connection conn = dataSource.getConnection();

        PreparedStatement pstmt = conn.prepareStatement(sql);
        pstmt.setString(1, member.getName());

        pstmt.executeUpdate();
```


`pstmt.setString(1, member.getName());` 에서 1은 `String sql = "insert into member(name) values(?)";` 해당 query 문에서의 ? index 이다.

`pstmt.executeUpdate();` 을 실행하면 실제 DB에 값이 저장된다.

`pstmt = conn.prepareStatement(sql, Statement.RETURN_GENERATED_KEYS);` 을 설정하면 `rs = pstmt.getGeneratedKeys();`을 통해서 id(key)값을 return 받는다.

`close(conn, pstmt, rs);`  실 행 이후 리소스 반환.


`SpringConfig` 스프링 설정 변경

DataSource는 데이터베이스 커넥션을 획득할 때 사용하는 객체다. 스프링 부트는 데이터베이스 커넥션
정보를 바탕으로 DataSource를 생성하고 스프링 빈으로 만들어둔다. 그래서 DI를 받을 수 있다.


- 개방-폐쇄 원칙(OCP, Open-Closed Principle)
  - 확장에는 열려있고, 수정, 변경에는 닫혀있다.
- 스프링의 DI (Dependencies Injection)을 사용하면 기존 코드를 전혀 손대지 않고, 설정만으로 구현
- 클래스를 변경할 수 있다.
- 회원을 등록하고 DB에 결과가 잘 입력되는지 확인하자.
- 데이터를 DB에 저장하므로 스프링 서버를 다시 실행해도 데이터가 안전하게 저장된다.


### 스프링 통합 테스트

- @SpringBootTest : 스프링 컨테이너와 테스트를 함께 실행한다.
- @Transactional : 테스트 케이스에 이 애노테이션이 있으면, 테스트 시작 전에 트랜잭션을 시작하고, 테스트 완료 후에 항상 롤백한다.

이렇게 하면 DB에 데이터가 남지 않으므로 다음 테스트에 영향을 주지 않는다

- @Commit 하면 rollback 하지 않음.


### 스프링 JdbcTemplate

- 순수 Jdbc와 동일한 환경설정을 하면 된다. 
- 스프링 JdbcTemplate과 MyBatis 같은 라이브러리는 JDBC API에서 본 반복 코드를 대부분 제거해준다. 하지만 SQL은 직접 작성해야 한다.
