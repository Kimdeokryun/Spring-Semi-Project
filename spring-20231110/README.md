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
