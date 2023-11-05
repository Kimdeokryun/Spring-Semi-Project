# Spring-Semi-Project
Spring Project


./mvnw package   패키징 필수.   그래야 jar 실행 파일 build 됨.

java -jar target/*.jar  프로젝트 빌드


#
gradle프로젝트로 설정 (gradle X).


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
8080포트를 jenkins로 사용중이여서 server.port = 8081  로 변경


### 로그 정보
application.properties
logging.level.org.springframework=INFO
logging.level.org.springframework.web=DEBUG



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
