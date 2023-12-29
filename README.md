# Spring Boot API Boilerplate
- slicequeue! spring boot api boilerplate 프로젝트
  - JPA 적용, H2 데이터베이스 사용

## 구성
Spring Boot RESTful API 전용 프로젝트
+ JPA 적용, H2 데이터베이스 사용

### 폴더 구조
- TBU

### 사용 라이브러리
build.gradle 구성 내용 설명
* JAVA 17
#### plugin
* 'org.springframework.boot' version 2.7.5
#### dependencies
* spring-boot-starter 관련 - plugin-version 2.7.5
  * spring-boot-starter-web
  * spring-boot-starter-test - junit jupiter
  * spring-boot-starter-actuator
  * spring-boot-starter-data-jpa
* database
  * runtimeOnly com.h2database:h2 - 실행용 인메모리 H2
  * testRuntimeOnly com.h2database:h2 - 테스트용 인메모리 H2
* micrometer & prometheus
  * io.micrometer:micrometer-registry-prometheus:1.8.4
* logback & log4j 취약점 대응
  * ch.qos.logback:logback-core:1.2.10
  * ch.qos.logback:logback-classic:1.2.10
  * org.slf4j:slf4j-api:1.7.32
  * org.slf4j:jul-to-slf4j:1.7.32
  * org.apache.logging.log4j:log4j-to-slf4j:2.17.1
  * org.apache.logging.log4j:log4j-api:2.17.1

## 초기 세팅
프로젝트 초기 세팅 관련 설정법 기술

### application.yml 설정
* 앱 이름 설정
  * spring.application.name: <프로젝트명_설정>

### H2 관련 설정
* main.resources.application.yml 설정
  * DB_URL: 데이터에비스 접속
    * 예시 (H2 in mem): jdbc:h2:mem:testdb;MODE=MySQL;DATABASE_TO_UPPER=FALSE
    * 예시 (H2 in local): jdbc:h2:~:testdb;MODE=MySQL;DATABASE_TO_UPPER=FALSE
  * DB_USER: DB 계정 아이디
    * 예시(H2 in mem):
  * DB_PASS: DB 계정 비밀번호
    * 예시(H2 in mem):
  * DB_POOL_SIZE: DB Hikari PoolSize
    * 예시(H2 in mem):
* test.resources.application.yml 설정
  * application.yml 에 H2 인메모리 DB 로 설정 고정
    * 상황에 맞게 직조작 할 것

### 액티브프로파일 설정
* jvm active profile 값 설정, IntelliJ 실행 설정으로 처리
  * 기본 설정값 관련해서는 예시용으로 작성한 logback-local.xml `local` 로 설정해야 작동
* JUnit 테스트 실행시에는 test.java.resources 부분에 application.yml 설정 적용되며
  * 각 테스트에 ActiveProfile 어노테이션으로 `test` 로 지정함
* 실행시 VM 다음 옵션으로 프로필 지정 `-Dspring.profiles.active={대상프로필값}` 으로 지정하여 실행
  * 각 개발 도구에 따라서 잘 적용할 것!
 
### 패키지경로 수정 & logback 로그 설정
* 현재 기본값인 `com.slicequeue.project` 명 적절하게 변경, 테스트 경로 까지 동일하게 변경 진행해야함
  * 각 개발 도구의 패키지 rename 기능을 활용하여 처리할 것
* ProjectApplication 클래스명 수정 위 프로젝트 명에 따라서 수정, 테스트에 동일하게 위치한 테스트 클래스명도 수정
* 위 액티브프로파일설정에서 main.resources.logback-local.xml 파일 수정
  * 31번 라인 관련하여 적절하게 로그 나올 수 있도록 프로젝트 패키지 경로 지정 필요
