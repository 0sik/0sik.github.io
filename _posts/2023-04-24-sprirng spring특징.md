---
layout: single
title: "spring 특징"
toc: true
toc_sticky: true
toc_label: "목차"
categories: spring
toc_icon: "bars"
tags: [spring]
---

📘 spring 특징

## 1장

### 스프링의 특징을 설명할 수 있어야함

- O/R 매핑 프레임워크 지원
    - 데이터베이스 라이브러리롸 연결할 수 있는 인터페이스 제공(Mybatis,Hibernate,JPA)
- 스프링 데이터를 통한 다양한 데이터 연동 기능
    - NoSQL DB유형의 데이터 저장소 및 검색 엔진 연동
- 스프링 배치
    - 대량의 데이터를 일괄 처리, 병행 처리할 수 있는 템플릿 제공
- 스프링 시큐리티
    - 인증,인가 기능 제공
    - OAuth개방형 표준 인증 서비스 제공
- 스프링 클라우드
    - Cloud 환경에서 동작하는 애플리케이션 개발 지원

### **DI,AOP,POJO 키워드 알기**

- POJO관리
    - 특정한 인터페이스를 구현하거나 상속을 받을 필요가 없는 가벼운 객체를 관리
- DI
    - 각각의 계층이나 서비스들 간에 객체 의존성이 존재할 경우 프레임워크가 객체 간의 의존 관계를 만들어 줌 ( 변경 용이성, 확정성, 품질관리 용이)
- AOP
    - 트랜잭션, 로깅, 보안과 같이 여러 모듈에서 공통적으로 사용하는 기능의 경우 해당 기능을 공통 모듈로 분리하여 관리(프로그램 가독성, 기술 은닉)
- 스프링빈
    - 스프링 컨테이너가 관리하는 객체
- IOC
    - 역전 제어, 인스턴스를 제어하는 주도권이 역전된다는 의미 , 개발자의 소스코드가 아닌 di컨테이너가 대신해 주기 때문에 제어가 역전되었다고 정의함
- IOC컨테이너
    - 스프링 프레임워크가 제공하는 ioc컨테이너를 통해 인스턴스의 생명주기 관리 및 의존관계 주입을 처리함

### 결합도를 낮추기 위해서 3개의 레이어를 도입했는데 레이어에대한 설명

- 인터페이스를 추가했잖아 그 관련 내용을 설명할 수 있어야함

페이지 화면전환 또는 동작제어를 담당하는 컨트롤러가 있는 프리젠테이션층 , 특정업무처리하는 서비스와 클래스의 집합 도메인이 있는 비즈니스 로직층 , 데이터 엑세스를 추상화하는 데이터 엑세스층으로 단방향 3개 층을 구성된다. 결합도를 낮추기 위해 오목형 레이어를 이용하면 되는데 결합 부분에 약한 결합 결계 구현(인터페이스)도입 필요하다.

## 2장

### 메이븐의 관리 기능중에 디렉토리나 의존성관리 빌드프로세스관리 등이있는데 pom.xml에서 사용되는 태그들이 있어 그 태그들을 알아야함

관리기능

1. 정형화된 프로젝트 디렉토리 구조 관리 
2. 의존성 관리 기능 
3. 빌드 프로세스를 관리 : 플러그인 설정을 통해 빌드 자동화

• groupId : 프로젝트 조직 고유 도메인 예) org.tukorea
• artifactId : 프로젝트 명 예) myhomework
• version : 프로젝트 버전

```jsx
<groupId>org.tukorea</groupId>
<artifactId>myhomework /artifactId>
<version>0.0.1-SNAPSHOT</version>
<packaging>jar</packaging>
<name>maven</name>
<url>http://maven.apache.org</url>
```

### 메이븐에 빌드 프로세스의 라이프 사이클 관련된거 알아야하고

라이프사이클은 미리 정해진 빌드 순서를 의미

build , clean, site 3개의 라이프 사이클이 있음

- build
    - 여러 단계의 페이즈로 나뉘어져 있으며 각 페이즈는 의존관계를 가진다.
    - 기본 라이프 사이클은 compile, test, package deploy 순서로 진행된다
- clean
    - clean페이즈를 이용하여 이전 빌드에서 생성된 모든 파일들을 삭제한다
- site
    - site,site-deploy페이즈를 이용하여 생성된 문서들을 대상 사이트에 배포한다

리소스 준비(resource) 리소스가 준비되어 복사된다.
컴파일(compile) 소스 코드를 컴파일한다.
테스트(test) Junit과 같은 테스트 프레임워크로 단위 테스트한다.
패키지(package) pom.xml의 <packaging /> 엘리먼트 값(jar, war, ear 등)에 따라 압축한다.
인스톨(install) 패키지를 로컬 저장소에 배포한다
배포(deploy) 원격 메이븐 저장소에 압축한 파일을 배포한다

### 의존성 라이브러리 설정할때 스코프의 의미를 알아야하고

의존 라이브러리를 적용할 수 있는 시점을 제한할 수 있다 - scope설정

- compile : 스코프를 설정할지 않았을 때의 기본 스코프
- provided : 컴파일시에는 직접 의존성을 참조하고 런타임시에는 다른 환경에서 의존성
을 제공받는다.(해당 컨테이너의 서블릿 API)
- runtime : 컴파일 시에는 사용되지 않지만 애플리케이션을 실행할 때 사용되는 라이브
러리일 경우 설정한다.
- test : 테스트하는 시점에만 사용하는 라이브러리에 대한 스코프를 설정할 때 사용
한다. (예: JUnit)
- system : provided와 비슷하다. 단지 우리가 직접 jar 파일을 제공해야 한다.
- import : import(메이븐 2.0.9 이후 버전부터 사용 가능): 다른 POM 설정 파일에 정의
되어 있는 의존 관계 설정을 현재 프로젝트로 가져온다. 이 범위는
<dependencyManagement/> 엘리먼트에서만 사용 가능하다.

### phase , goal ,plugin

- 라이프사이클 하나당 여러 phase로 구성 각 phase별로 작업을 수행하는것이 plugin이고 그 작업을goal이라고 설명돼있다. 그 내용 이해하는것

각 빌드 단계에서 수행하는 작업을 골 이라고 한다, 골은 그 단계에 연결된 플러그인에 의해 실행된다, 빌드 라이프사이클은 하나 이상의 골을 수행하는 페이지들로 구성 각 페이즈 별로 플러그인이 작업을 수행하는데 그 작업을 골이라고 한다.

### 그레이들은 프로젝트를 만들면 디렉토리 구성을 기본적으로 주는데 그때 제공되는 몇가지 파일들(그레들 레포, 빌드.그레들) 각 파일들에 대해서 기능을 알아야함

gradle-wrapper.jar : gradle task를 실행하기 위한 Wrapper 파일. Wrapper는 선언된 버전의
Gradle을 호출하여 필요한 경우 미리 다운로드. 프로젝트를 새로운 환경
에 종속되지 않고 빌드 가능

[gradle-wrapper.properties](http://gradle-wrapper.properties) : gradle wrapper 설정 정보 파일

build.gradle: 프로젝트의 라이브러리 의존성, 플러그인, 라이브러리 저장소 등을 설정
할 수 있는 빌드 스크립트 파일

Gradlew 리눅스 또는 맥OS용 실행 스크립트 파일
gradlew.bat 윈도우용 실행 스크립트 파일

setting.gradle :  프로젝트의 설정 정보 파일

### 그레이들의 의존관계설정 implementation,runtimeOnly등등 각각의 설정을 알아야함

implementation 코드 컴파일 과정과 필요시 런타임에 필요한 라이브러리 의존성을 추가
compileOnly 코드 컴파일 과정에만 필요한 라이브러리 의존성을 추가
compileClasspath 코드 컴파일하는 시점의 Compile classpath를 의미
annotationProcessor 컴파일 시점에 어노테이션이 붙은 코드에 대해서 코드를 생성
runtimeOnly 코드 실행시, 런타임에만 필요하다는 의미
runtimeClasspath 코드 런타임에서 사용하는 runtimeClasspath를 의미

## 3장

### DI 설정 xml , java 기반 방식은 코드를 작성 할 수 있어야함

- xml → java로 코드를 바꿀수 있어야함
- @Bean 매서드를 불러들여서 객체를 취득
- XML 에서는 <property> 태그나 <constructor-arg> 태그를 이용해서 설정하였으나
자바 설정에서는 직접 의존 객체를 주입해야 한다.

```jsx
xml
<bean id="memberDAO" class="org.tukorea.di.persistence.MemberDAOImpl">
</bean>
<bean id="memberService" class="org.tukorea.di.service.MemberServiceImpl">
<constructor-arg ref="memberDAO" />
</bean>

java
@Configuration
public class JavaConfig {
@Bean
public MemberDAO memberDAO() {
return new MemberDAOImpl();
}
@Bean(name="service")
public MemberService memberService() {
return new MemberServiceImpl(memberDAO());
}
}
```

### DI에 쓰는 애노테이션 방식으로 보면 annotation-config , component-scan 방식의 차이점을 설명할 수 있어야함

annotation-config : xml에 bean이 이미 있고 autowired를 활용하여 annotation-config을 참고하여 의존성 주입을 하는 방식

```jsx
<bean id="memberDAO" class="org.tukorea.di.persistence.MemberDAOImpl">
</bean>
<bean id="memberService" class="org.tukorea.di.service.MemberServiceImpl">
</bean>
<context:annotation-config />

public class MemberServiceImpl implements MemberService {
@Autowired
private MemberDAO memberDAO;
```

component-scan : 특정 패키지 밑에 있는 컴포넌트를 스프링 빈으로 등록도하고 주입도 하는 방식, 패키지 경로를 지정해줌, 스프링 빈도 찾고 주입

```jsx
<context:component-scan base-package="org.tukorea.di.persistence"></context:component-scan>
<context:component-scan base-package="org.tukorea.di.service"></context:component-scan>

@Component
public class MemberServiceImpl implements MemberService {
@Autowired
private MemberDAO memberDAO;
```

### 애노테이션 @Configuration @Bean에 대한 이해도 알아야한다

@Configuration 빈 설정 메타 정보를 담고 있는 클래스를 선언
해당 클래스가 스프링 설정으로 사용됨

@Bean 클래스 내의 매서드를 정의하여 새로운 빈 객체를 정의할 때 사용
name 속성을 사용하여 새로운 빈 이름 적용 가능

### Bean을 생성할때 초기화 하는방식 4가지

XML 기반 <bean> 요소의 init-method 속성에 메서드 지정
애너테이셔 기반 @PostConstruct 애너테이션 붙은 메서드
자바 기반 @Bean의 initMethod 속성에 지정된 메서드
인터페이스 구현 InitializeBean 인터페이스의 afterPropertiesSet 메서드

## 4장

### 스프링 jdbc에서 사용하는 스프링 bean은 datasorce 와 JdbcTemplate 그리고 필요한 라이브러리

데이터소스 : 데이터 액세스 기술 종류와 상관없이 데이터베이스 접속을 관리해주는 인터페이스 (Apache Commons DBCP)

```jsx
<dependency>
<groupId>commons-dbcp</groupId>
<artifactId>commons-dbcp</artifactId>
<version>1.4</version>
</dependency>

<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
```

스프링 JDBC기 제공하는 중요 탬플릿

- JdbcTemplate
- NamedParameterTemplate

```jsx
<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
<constructor-arg ref="dataSource" />
</bean>
<bean class="org.springframework.jdbc.core.namedparam.NamedParameterJdbcTemplate">
<constructor-arg ref="dataSource" />
</bean>
```

### JdbcTemplate 클래스 제공 메서드 p.13 각 요 기능을 알아야함

queryForObject  하나의 결과 레코드 중에서 하나의 컬럼 값을 가져올 때
                              RowMapper와 함께 사용하면 하나의 레코드 정보를 객체에 매핑

```jsx
int count = jdbcTemplate.queryForObject(
"SELECT COUNT(*) FROM STUDENT", Integer.class);

String name = jdbcTemplate.queryForObject(
"SELECT username FROM STUDENT WHERE id= ?", String.class, id);
```

queryForMap      하나의 결과 레코드 정보를 Map 형태로 매핑할 수 있음

```jsx
Map<String, Object> student = jdbcTemplate.queryForMap(
"SELECT * FROM STUDENT WHERE id= ?", id);
String name = (String)student.get("username");
```

queryForList        여러 개의 Map 형태의 결과 레코드를 다룰 수 있음

```jsx
List<Map<String, Object>> studentList = jdbcTemplate.queryForMap(
"SELECT * FROM STUDENT ");
```

query                    여러 개의 레코드를 객체로 변환하여 처리(ResultSetExtractor)

```jsx
List<StudentVO> studentlist = jdbcTemplate.query(
"SELECT * FROM STUDENT",
new RowMapper<StudentVO>() {
public StudentVO mapRow(ResultSet rs, int rowNum) throws SQLException {
StudentVO vo = new StudentVO();
vo.setId(rs.getString("ID"));
vo.setPasswd(rs.getString("PASSWD"));
vo.setUsername(rs.getString("USERNAME"));
vo.setSnum(rs.getString("SNUM"));
vo.setDepart(rs.getString("DEPART"));
vo.setMobile(rs.getString("MOBILE"));
vo.setEmail(rs.getString("EMAIL"));
return vo;
}
```

update                  데이터의 변경(INSERT, UPDATE, DELETE)을 실행할 때

```jsx
StudentVO vo;
jdbcTemplate.update(
"INSERT INTO STUDENT (ID, PASSWD, USERNAME, SNUM, DEPART, MOBILE, EMAIL)
VALUES (?, ?, ?, ?, ?, ?, ?) " , vo.getId(), vo.getPasswd(), vo.getUsername(),
vo.getSnum(), vo.getDepart(), vo.getMobile(), vo.getEmail()
);

StudentVO vo;
jdbcTemplate.update( “DELETE FROM STUDENT WHERE ID=? “, vo.getId() );
```

### junit test 프레임워크를 쓸때 애노테이션 @runwith @ContextConfiguration @Test 을 설명할 수 있어야함

스프링 프레임워크에서 만든 클래스(@Controller, @Service, @Repository,
@Component 등이 붙은 클래스)를 테스트하는 모듈

단위 테스트, 통합 테스트를 지원하기 위한 매커니즘이나 편리한 기능을 제공

• Junit 테스트 프레임워크를 사용하여 스프링 DI 컨테이너를 동작시키는 기능
• 트랜잭션 테스트를 상황에 맞게 제어하는 기능
• 애플리케이션 서버를 사용하지 않고 스프링 MVC 동작을 재현하는 기능
• RestTemplate을 이용해 HTTP 요청에 대한 임의 응답을 보내는 기능

@RunWith(SpringJUnit4ClassRunner.class) : 테스트용 DI컨테이너를 동작시키기 위한 Runner클래스

@ContextConfiguration(locations = "classpath:/applicationContext.xml") : 테스트용 DI 컨테이너가 사용하는 설정 파일

@Test : 테스트 메서드 선언

## 5장

### 모델 1, 모델2, 프론트 컨트롤러의 차이점을 설명할 수 있어야 함

- 모델 1 : JSP만 구현 개발하거나 java bean을 포함하여 개발하는 방식을 의미 , JSP에 뷰와 비즈니스 로직이 혼재되어 복잡도가 높아 유지보수 어려움
- 모델 2 : 사용자 입력 처리와 화면의 흐름 제어 담당하는 컨트롤러 , 뷰에 필요한 비즈니스 영역의 로직을 처리하는 모델, 비즈니스 영역에 대한 결과하면을 담당하는 뷰로 나누어 개발하는 방식
- 프론트 컨트롤러 : 클라이언트 요청을 별도의 프론트 컨트롤러에 집중, 모든 요청의 공통 부분을 별도(프론트 컨트롤로)로 처리

### 프론트 컨트롤러 패턴에서 실행 프로세스가 있는데 그 실행 프로세스의 절차를 설명 할 수 있어야함

① DispatcherServlet이 HTTP 요청을 받음
② DispatcherServlet은 서브 Controller로 HTTP 요청 위임
③ 서브 Controller는 클라이언트의 요청 처리를 위해 DAO 객체를 호출
④ DAO 객체는 리소스를 엑세스하여 Model 객체를 생성 후 요청 결과 리턴
⑤ DispatcherServlet 은 처리 결과에 적합한 뷰에 화면 처리 요청
⑥ 선택된 뷰는 화면에 모델 객체를 가져와 화면 처리
⑦ HTTP 응답

### mvc모듈 구성 요소 p.8 Handler~~,~~ 구성요소가 무슨 기능이 있는지 알아야하고

DispatcherServlet : 프론트 컨트롤러를 담당한다. 클라이언트의 요청을 받아서 Controller에게 클라이언트의 요청을 전달하고, 리턴 결과값을 View에게 전달하여 알맞은 응답을 생성한다.

HandlerMapping : 
URL과 요청 정보를 기준으로 어떤 컨트롤러를 실행할지 결정하는 객체.
DispatcherServlet은 하나 이상의 핸들러 매핑을 가질 수 있음. 애노테이션을 이용
할 때에는 mvn:annotation-driven 태그를 설정해야 함

- HandlerMapping의 mvn:annotation-driven 태그와 annotation-bean을 구별 주의
    
    <annotation-driven />
    
    - 스프링 MVC를 이용하는데 필요한 컴포넌트 빈(HandlerMapping) 등록을 자동으로 수행
    - 패키지 내부에서 찾은 빈(컨트롤러)과 URI를 맵핑

Controller :  클라이언트의 요청을 처리한 뒤 그 결과를 DispatcherServlet에게 알려 줌

Model :  컨트롤러가 뷰에게 넘겨줄 데이터를 저장하기 위한 객체

ViewResolver :  Controller가 리턴한 뷰 이름을 기반으로 Controller 처리 결과를 생성할 뷰를 결정

View :  Controller의 처리 결과 화면을 생성함

### 웹 어플리케이션 컨텍스트 등록 설정 ContextLoadListner 클래스, DispatcherServlet 클래스 두개의 과정을 설명할 수 있어야함

톰캣실행 종료 시점과 wac실행 종료 시점 같고, listener(특정 이벤트 발생 시 실행)을 통해 실행시 초기 설정 가능하다. listener을 통해 톰캣에 contextloadlistener을 등록하고 root-context을 통해 설정 파일을 등록한다. 

root-context.xml(서비스 이하 계층 빈 등록): component-scan 으로 빈 등록 (서비스 이하 di 등록) (서블릿 관련 빈 외 모든 계층 빈 등록)

그 다음 DispatcherServlet을 톰캣에 등록하고 servlet-context.xml을 통해 설정파일 등록한다  servlet-context.xml : (contextLoadListener상속 받은, 컨트롤러 빈 등록) : component-scan 으로 빈등록 ( 컨트롤러 빈 di 등록) (서블릿관련 계층 빈 등록)

### 컨트롤러하면서 매개변수 받는 방법 p.25 방법의 차이점을 알아야함

- @RequestMapping
    - URL과 컨트롤러 메서드의 매핑을 설정하는 애노테이션

@ModelAttribute 매개변수

```jsx
**// http://localhost:8080/web/tryB?msg=thankyou
@RequestMapping(value="/tryB", method = RequestMethod.GET)
public String getUserTest2( @ModelAttribute("msg") String msg )** {
logger.info(msg);
logger.info(" /tryB URL called. then getUserTest2 method executed.");
return "result_b";
}

**// http://localhost:8080/web/tryC?msg=thankyou
@RequestMapping(value={"/tryC", "/tryD"}, method = RequestMethod.GET)
public String getUserTest2( @ModelAttribute("msg") String msg )** {
logger.info(msg);
logger.info(" /tryB URL called. then getUserTest2 method executed.");
return "result_c";
}

**// http://localhost:8080/web/tryF
@RequestMapping(value={"/tryF"}, method = RequestMethod.POST)
public String setUserTest5Post( @ModelAttribute("student") StudentVO vo)** {
logger.info(vo.toString());
logger.info(" /tryF URL POST method called. then setUserTest5Post method executed.");
return "result_info";
}
```

@PathVariable 매개변수

```jsx
// http://localhost:8080/web/try/thankyou
**@RequestMapping(value="/try/{msg}", method = RequestMethod.GET)
public String getUserTest( @PathVariable("msg") String msg)** {
logger.info(msg);
logger.info(" /try URL called. then getUserTest method executed.");
return "result_a";
}
```

@RequestParam 매개변수

```jsx
**// http://localhost:8080/web/tryA?msg=thankyou
@RequestMapping(value="/tryA", method = RequestMethod.GET)
public String getUserTest1( @RequestParam("msg") String msg )** {
logger.info(msg);
logger.info(" /tryA URL called. then getUserTest1 method executed.");
return "result_a";
}
```

@RequestBody 매개변수

### 애노테이션들은 기본적으로 외우고 있어야함

@Autowired 컨테이너가 빈과 다른 빈과의 의존성을 자동으로 연결하도록 하는 수단

@Component 컨테이너가 인젝션을 위한 인스턴스(빈)을 설정하는 수단

@Controller 프레젠테이션 층 스프링 MVC용 애노테이션
@Service
비즈니스 로직 층 Service용 애노테이션으로. @Component와 동일
이 애노테이션으로 트랜잭션 관리를 할 수 있다는 소문이 있지만 아직 실현되
지 않음
@Repository 데이터 액세스 층의 DAO용 애노테이션
데이터 액세스에 관련된 예외를 모드 DataAccessException으로 변환
@Configuration Bean 정의를 자바 프로그램에서 실행하는 JavaConfig용 애노테이션

### 레스트아키텍처에 관련된 내용하고 관련된애노테이션 request body response body 등 설명할 수 있어야함

➢ REST 아키텍처

- REST(Representational State Transfer)는 클라이언트와 서버 사이에 데이터 연동
애플리케이션을 위한 아키텍처 스타일
- 웹 상의 정보를 리소스로 파악하고 그 식별자로서 URI를 할당해 고유하게 주소를 지정
하는 방법
- HTTP 프로토콜을 사용해 리소스에 접근하고 HTTP 메서드에 대한 처리 결과를 서버는
JSON 또는 XML 등의 형식으로 전송한다.

@RestController : REST API를 제공하는 컨트롤러를 의미하며
@Controller와 @ResponseBody를 의미를 합침

@RequestBody : 컨트롤러 메서드 매개 변수에 @RequestBody가 애노테이션 된 경
우, 스프링은 요청된 HTTP request body를 해당 매개 변수에 바인딩한다.

@ResponseBody : 컨트롤러 메소드가 @ResponseBody로 어노테이션 된 경우, 스
프링은 반환 값을 나가는 HTTP response body에 바인딩한다. 스프링은 요청된 메시
지의 HTTP 헤더에 있는 Content-Type을 기반으로 HTTP Message converter를 사용
하여 반환 값을 HTTP response body로 변환한다.

ResponseEntity : 전체 HTTP 응답을 나타내며 statusCode, headers, body 3가지 속
성 값을 지정할 수 있다.

### 예외처리에 관련되 애노테이션 @ExceptionHandler, @ControllerAdvice가 어떤 기능을 하는지 알아야함

컨트롤러 별로 예외 처리
• 컨트롤러의 메서드에서 예외가 발생했을 때의 처리를 정의
• 별도의 예외 처리 메서드를 정의하고 그 메서드에 @ExceptionHandler 애노테이션 설정

하나의 웹 애플리케이션 안에서 공통된 예외 처리
• 복수의 컨트롤러에서 사용할 수 있는 공통된 예외 처리 클래스를 정의
• 공통된 예외 처리 클래스를 정의하고 그 클래스에 @ControllerAdvice 애노테이션을 설정