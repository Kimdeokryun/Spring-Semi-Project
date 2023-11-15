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

