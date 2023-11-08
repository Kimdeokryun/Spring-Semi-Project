# Spring-Semi-Project
Spring Project

[src 디렉터리](#src)

[issue](#issue)
- [Java versionerror](#Java-version-error)
- [포트 사용](#포트-사용)
- [spring-javaformat:apply](#Run-`spring-javaformat:apply`-to-fix.)

[개발 부분](#개발-부분)
- [생성 단축키](#생성-단축키)
- [query](#query)
- [IoC](#IoC-(Inversion-of-Control))
- [스프링 IoC 컨테이너](#스프링-IoC-컨테이너)
- [Bean을 가져오는 방법](#Bean을-가져오는-방법.)
- [AOP](#AOP)
- [다양한 AOP 구현 방법](#다양한-AOP-구현-방법)
- [프록시 패턴](#프록시-패턴)

#

### src
```
src
┣ checkstyle
┣ main
┣ test
```

./mvnw package   패키징 필수.   그래야 jar 실행 파일 build 됨.

java -jar target/*.jar  프로젝트 빌드


#
maven 프로젝트 설정.


## issue

### Java version error
java.lang.UnsupportedClassVersionError: org/springframework/boot/loader/JarLauncher has been compiled by a more recent version of the Java Runtime (class file version 61.0), this version of the Java Runtime only recognizes class file versions up to 55.0

-> 최신버전의 Java 17로 컴파일 해야함.

JRE(JAVA Runtime Environment) : 자바 프로그램이 실행될 수 있는 환경 구성

JDK(JAVA Development Kit) : 자바로 개발을 할 수 있는 환경구성(때문에 JRE가 포함됨)

jdk-17_windows-x64_bin.exe로 java 17.0.9 설치.


#### 환경 변수 설정
JAVA_HOME   ex) C:\Program Files\Java\jdk-17

CLASSPATH   %JAVA_HOME%\lib

Path        %JAVA_HOME%\bin

java -version과 javac -version 명령어로 설치 확인


### 포트 사용

8080포트를 jenkins로 사용중이여서 application.properties의 파일에 server.port = 8081  로 변경


### 로그 정보
application.properties
logging.level.org.springframework=INFO
logging.level.org.springframework.web=DEBUG


### Run `spring-javaformat:apply` to fix.

terminal에서

./mvnw spring-javaformat:apply


#


## 개발 부분


### 생성 단축키
IntelliJ 기준 -> Alt + Insert   (생성자, Getter, Setter 등)

#

### query
@Query("SELECT DISTINCT owner FROM Owner owner left join  owner.pets WHERE owner.firstName LIKE :firstName %")

firstName 부분 앞에 다른 값 삽입 불가.

LIKE %:firstName % 로 작성해야함.

#

### IoC (Inversion of Control)

일반적인 (의존성에 대한) 제어권: “내가 사용할 의존성은 내가만든다.”

IoC: “내가 사용할 의존성을 누군가 알아서 주겠지”

-> OwnerController.java
public OwnerController(OwnerRepository clinicService) {
	this.owners = clinicService;
}

해당 코드에서 OwnerRepository clinicService 는 누가 넣어주느냐.

-> OwnerControllerTests.java
@MockBean                   // MockBean 스프링프레임워크 핵심기술
private OwnerRepository owners;    // 스프링이 테스트를 만들 때, 자동으로 Bean으로 등록

Bean 이란? Spring이 관리하는 객체

**** 해당 코드를 통해 스프링의 IoC 컨테이너가 의존성을 관리해준다.

직접 만들어서 의존성 주입을 할 수 있지만, 스프링이 제공하는 의존성 주입 관련 기능 혹은
컨테이너 lifecycle 인터페이스를 통해 다양한 기능 확장이 가능하다. 

그래서 IoC 컨테이너 기능을 사용한다.

#

### 스프링 IoC 컨테이너

빈(bean)을 만들고 엮어주며 제공해준다.

#### bean을 아는 방법.
IntelliJ Ultimate 버전 기준  codeline 부분에 콩(bean) 모양이 보인다.

@Bean 혹은 extends interface 혹은 직접 해당 타입의 return 을 통해 IoC 컨테이너에 Bean 등록.

의존성 주입을 스프링 IoC 컨터이너에서 해준다.

의존성 주입은 Bean 끼리만 가능하다.  (IoC 컨터이너 내부에 있는 객체들 끼리)

#

### Bean을 가져오는 방법.
#### 굳이 할 필요는 없음.

ApplicationContext applicationcontext;

applicationcontext.getBeanDefinitionNames();  // 모든 Bean의 이름 get.

applicationcontext.getBean(s:)  // 해당 Bean의 이름으로 Bean을 가져옴.

or Bean type으로 가져옴.
OwnerController.class로 

# 


### Bean을 등록하는 방법

● Component Scanning
	@Component
		■ @Repository
		■ @Service
		■ @Controller (test 폴더의 java sample패키지에 SampleControllerTest.java)
		■ @Configuration (test 폴더의 java sample패키지에 SampleConfig.java)

● 또는 직접 일일히 XML이나 자바 설정 파일에 등록

#### 사용하는 방법
●  @Autowired 또는 @Inject
-> Spring version 4.3 ~ 

클래스에 생성자가 하나뿐이고, 생성자를 주입받는 레퍼런스변수들이 Bean으로 등록되어 있다면 Bean을 자동으로 주입해주도록 되어 있다. 

따라서 Autowired가 생략가능하다. (main java owner 패키지에 OwnerController.java 생성자 부분.)

-> Field에서 직접 주입 (생성자 대신.)

-> Setter에서 주입 (생성자 대신.)

● 또는 ApplicationContext에서 getBean()으로 직접 꺼내거나


● Field에서 의존성을 주입받는 방법.

오로지 “빈"들만 의존성 주입을 해줍니다

#### Bean 등록이 되어 있지 않았는데, 의존성 주입을 하려할 때 error문.

No qualifying bean of type 'org.springframework.~'

#### 생성자에 Bean을 등록하는 것이 좋은 이유

필수적으로 사용해야 하는 레퍼런스 없이는 해당 인스턴스를 만들지 못하도록 강제할 수 있다.

#### 상호 참조 의존성 문제 해결

Field injection이나 Setter injection 사용



#### 과제 OwnerController에 PetRepository 주입하기

Field
```
	@Autowired
	private PetRepository petRepository;
```

Constructor
```
	private final PetRepository petRepository;
	public OwnerController(OwnerRepository clinicService, PetRepository petRepository) {
		this.owners = clinicService;
		this.petRepository = petRepository;
	}
```

Setter
```
	private PetRepository petRepository;

	@Autowired
	public setPetRepository(PetRepository petRepository){
		this.petRepository = petRepository;
	}
```

#

### AOP
Aspect Oriented Programming

관점지향 프로그래밍

흩어진 AAAA 와 BBBB를 별도의 클래스 메소드로 모아 놓는다.

ex) 요청 처리 시 성능 측정을 위한 도구로 Spring의 StopWatch 유틸 사용

API 호출 메서드 내에 해당 코드가 반복적으로 작성된 경우.
```
StopWatch stopwatch = new StopWatch();
stopwatch.start();
~
stopwatch.stop();
System.out.println(stopwatch.prettyPrint());
```

AOP를 사용하면 해당 코드를 작성하지 않아도 API 호출 시 실행된다.

### 다양한 AOP 구현 방법
● 컴파일 A.java ----(AOP)---> A.class (AspectJ)
● 바이트코드 조작 A.java -> A.class ---(AOP)---> 메모리 (AspectJ)
● 프록시 패턴 (스프링 AOP)

### 프록시 패턴
● https://refactoring.guru/design-patterns/proxy

#