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

### query
@Query("SELECT DISTINCT owner FROM Owner owner left join  owner.pets WHERE owner.firstName LIKE :firstName ")

firstName 부분 앞에 다른 값 삽입 불가.

firstName 부분을 애초에  "%" + firstName + "%" 로 만들어야 함.