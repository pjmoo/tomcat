# Tomcat Servlet & JSP Starter Project

본 프로젝트는 Apache Tomcat 및 Jakarta Servlet API 6.1.0 기반으로 작동하는 최소한의 자바 웹 애플리케이션 예제입니다. 초심자가 서블릿(Servlet)과 JSP의 기본 동작 원리를 이해할 수 있도록 구성되어 있습니다.

---

## 1. 프로젝트 디렉토리 구조 (Project Structure)

본 프로젝트는 Maven의 표준 디렉토리 레이아웃(Standard Directory Layout)을 따르고 있습니다.

```text
tomcat/
├── .mvn/                      # Maven Wrapper 관련 설정 폴더
├── mvnw                       # Linux/macOS용 Maven 실행 스크립트
├── mvnw.cmd                   # Windows용 Maven 실행 스크립트
├── pom.xml                    # Maven 의존성 및 빌드 설정 파일
└── src/
    └── main/
        ├── java/
        │   └── com/
        │       └── example/
        │           └── tomcat/
        │               └── HelloServlet.java  # 서블릿 자바 클래스 파일
        ├── resources/         # 클래스패스에 포함될 리소스 폴더
        └── webapp/            # 웹 애플리케이션 루트 디렉토리
            ├── index.jsp      # 메인 JSP 페이지
            └── WEB-INF/
                └── web.xml    # 웹 애플리케이션 배치 기술서 (Deployment Descriptor)
```

### 주요 구성 파일 링크 및 설명

- [pom.xml](file:///Users/morgan/Documents/workspace/tomcat/pom.xml)
    - 프로젝트 빌드 환경, 자바 버전(Java 17), 그리고 Jakarta Servlet API 6.1.0과 JUnit 5 등의 의존성을 설정하는 파일입니다.
- [HelloServlet.java](file:///Users/morgan/Documents/workspace/tomcat/src/main/java/com/example/tomcat/HelloServlet.java)
    - HTTP GET 요청을 받아 HTML 페이지를 동적으로 응답하는 서블릿 클래스입니다.
- [index.jsp](file:///Users/morgan/Documents/workspace/tomcat/src/main/webapp/index.jsp)
    - 사용자에게 보여지는 첫 화면으로, 간단한 HTML 구조와 Java 코드가 융합된 JSP 스크립트가 포함되어 있습니다.
- [web.xml](file:///Users/morgan/Documents/workspace/tomcat/src/main/webapp/WEB-INF/web.xml)
    - 서블릿 컨테이너(Tomcat)가 웹 애플리케이션을 구동할 때 필요한 설정을 담는 XML 설정 파일입니다.

---

## 2. 초심자를 위한 핵심 개념 설명 (Core Concepts)

### 웹 서버 (Web Server) vs 웹 애플리케이션 서버 (WAS)
- **웹 서버 (Web Server)**: 클라이언트(브라우저)로부터 HTTP 요청을 받아 HTML, CSS, 이미지 등 정적(Static) 콘텐츠를 제공하는 서버입니다. (예: Apache, Nginx)
- **웹 애플리케이션 서버 (WAS - Web Application Server)**: 데이터베이스 조회나 복잡한 비즈니스 로직 등 동적(Dynamic)인 요청을 처리하기 위한 서버입니다. 웹 서버 기능에 더해 **서블릿 컨테이너**를 내장하고 있습니다. (예: Apache Tomcat)

### 서블릿 (Servlet)
- 자바를 사용하여 웹 페이지를 동적으로 생성하는 서버 측 프로그램 기술입니다.
- [HelloServlet](file:///Users/morgan/Documents/workspace/tomcat/src/main/java/com/example/tomcat/HelloServlet.java#L9) 클래스는 `HttpServlet`을 상속받아 HTTP 요청 방식에 맞는 메서드(`doGet`, `doPost` 등)를 구현하여 동적으로 HTML을 생성합니다.

### 서블릿 컨테이너 (Servlet Container)
- 서블릿의 생성, 실행, 소멸 등 전체적인 라이프사이클을 관리하는 소프트웨어입니다. (Tomcat이 이에 해당)
- 클라이언트의 HTTP 요청을 받고 응답할 수 있도록 소켓 통신 및 멀티스레딩 처리를 대신 해줍니다.

### 서블릿 생명주기 (Servlet Lifecycle)
1. **초기화 (`init`)**: 서블릿 객체가 처음 메모리에 로드될 때 단 한 번 실행됩니다. 초기 설정 작업을 수행합니다.
2. **요청 처리 (`service` -> `doGet`/`doPost`)**: 클라이언트의 요청이 올 때마다 스레드가 할당되어 실행됩니다.
3. **종료 (`destroy`)**: 서블릿 컨테이너가 서블릿을 종료하고 메모리에서 해제할 때 호출됩니다.

### JSP (JavaServer Pages)
- HTML 문서 내부에 Java 코드를 삽입하여 동적인 웹 페이지를 생성하는 기술입니다.
- 브라우저가 [index.jsp](file:///Users/morgan/Documents/workspace/tomcat/src/main/webapp/index.jsp)를 요청하면, 서블릿 컨테이너(Tomcat)는 이 JSP 파일을 내부적으로 `.java` 서블릿 파일로 컴파일하여 실행합니다. 즉, JSP도 결국 서블릿으로 변환되어 실행됩니다.

---

## 3. 기술 면접 대비 예상 질문 & 답변 (Interview Questions)

### Q1. Web Server와 WAS의 차이점은 무엇인가요?
**A1.** Web Server는 클라이언트로부터 HTTP 요청을 받아 HTML, CSS, 이미지 등 **정적 콘텐츠**를 주로 처리하고 제공합니다. 반면, WAS(Web Application Server)는 DB 조회나 다양한 비즈니스 로직 처리를 요구하는 **동적 콘텐츠**를 제공하는 서버입니다. WAS는 내부에 웹 컨테이너(또는 서블릿 컨테이너)를 가지고 있어 자바 서블릿이나 JSP를 실행할 수 있습니다. 톰캣은 대표적인 WAS입니다. 보통 서비스 구축 시 정적 리소스는 Web Server가 빠르게 처리하고, 동적 요청은 WAS로 넘겨주는 구조를 사용하여 부하를 분산합니다.

### Q2. 서블릿(Servlet)의 생명주기(Lifecycle)에 대해 설명해주세요.
**A2.** 서블릿의 생명주기는 크게 세 단계로 이루어지며, 서블릿 컨테이너(Tomcat)에 의해 관리됩니다.
1. **init()**: 서블릿 인스턴스가 최초 생성될 때 1회 호출되며, 서블릿의 초기화 작업을 수행합니다.
2. **service() / doGet() / doPost()**: 클라이언트의 요청이 들어올 때마다 호출됩니다. `service()` 메서드가 요청의 HTTP Method(GET, POST 등)를 분석하여 해당하는 `doGet()`, `doPost()` 등의 메서드로 요청을 분기합니다.
3. **destroy()**: 서블릿 객체가 수명을 다하고 소멸될 때 1회 호출되며, 자원 해제 등의 정리 작업을 수행합니다.

### Q3. 서블릿은 멀티스레드 환경에서 어떻게 동작하며, 스레드 세이프(Thread-Safe)한가요?
**A3.** 서블릿 컨테이너(Tomcat)는 기본적으로 **싱글톤(Singleton)** 패턴으로 서블릿 객체를 단 하나만 생성하여 메모리에 올립니다. 클라이언트로부터 요청이 올 때마다 새로운 스레드를 생성(또는 스레드 풀에서 꺼내어)하여 동일한 서블릿 객체의 `service()` 메서드를 실행시킵니다.
따라서, 여러 스레드가 동시에 서블릿 인스턴스에 접근하므로 **서블릿은 기본적으로 Thread-Safe하지 않습니다.** 서블릿 내부에 공유 가능한 상태를 저장하는 멤버 변수(필드 변수)를 두어 값을 수정하는 행위는 지양해야 하며, 요청별 데이터는 메서드 내부의 지역 변수나 `HttpServletRequest` 객체를 통해 안전하게 관리해야 합니다.

### Q4. JSP와 Servlet의 차이점은 무엇인가요?
**A4.** 두 기술 모두 서버 측에서 동적 콘텐츠를 생성하기 위한 기술이지만, 역할과 구조에서 차이가 있습니다.
- **Servlet**은 자바 클래스(`.java`) 내부에 HTML 코드가 들어가는 구조로, 비즈니스 로직 처리 및 흐름 제어(Controller 역할)에 유리합니다.
- **JSP**는 HTML 문서(`.html`/`.jsp`) 내부에 자바 코드가 들어가는 구조로, 화면단 구성(View 역할)에 유리합니다.
  동작 흐름을 보면, JSP는 사용자가 요청할 때 톰캣에 의해 자바 서블릿 클래스로 컴파일(변환)된 후 실행됩니다. 현대 웹 개발(Spring MVC 등)에서는 주로 서블릿이 요청을 받아 비즈니스 로직을 처리하고, JSP는 데이터를 출력하는 뷰 역할을 담당하는 MVC 패턴을 적용합니다.

### Q5. web.xml 설정 방식과 @WebServlet 어노테이션 방식의 차이는 무엇인가요?
**A5.**
- **web.xml (배치 기술서)**: 웹 애플리케이션의 서블릿 등록, 매핑, 필터, 리스너 등을 XML 파일에 명시적으로 기술하는 전통적인 방식입니다. 코드의 변경 없이 XML 설정만 변경하여 서블릿 매핑 등을 수정할 수 있다는 장점이 있습니다.
- **@WebServlet 어노테이션**: Servlet 3.0 스펙부터 도입된 방식으로, 자바 소스 코드 위에 직접 어노테이션을 붙여 서블릿을 등록하는 방식입니다. 설정이 분산되지 않고 코드 내에서 직관적으로 매핑 주소를 확인할 수 있어 개발 생산성이 높습니다.
  현재 본 프로젝트의 [HelloServlet](file:///Users/morgan/Documents/workspace/tomcat/src/main/java/com/example/tomcat/HelloServlet.java#L8)은 `@WebServlet` 어노테이션을 사용하고 있으며, [web.xml](file:///Users/morgan/Documents/workspace/tomcat/src/main/webapp/WEB-INF/web.xml)은 빈 파일 상태로 유지 중입니다.

### Q6. Servlet에서 forward 방식과 redirect 방식의 차이점을 설명해주세요.
**A6.**
- **Forward (포워드)**: 서블릿에서 다른 서블릿이나 JSP로 제어권을 넘기는 방식입니다. 웹 브라우저는 다른 페이지로 이동했는지 알 수 없어 브라우저의 URL 창 주소가 바뀌지 않습니다. 또한 HTTP 요청(Request)과 응답(Response) 객체가 공유되므로 데이터를 담아 전달하기 적합합니다. 서버 내부에서만 이동이 일어납니다.
- **Redirect (리다이렉트)**: 서버가 클라이언트에게 "다른 주소(URL)로 다시 요청해라"는 응답(HTTP Status 302와 Location 헤더)을 보내는 방식입니다. 브라우저는 서버의 지시에 따라 해당 주소로 완전히 새로운 HTTP 요청을 다시 보냅니다. 따라서 브라우저의 URL 주소가 실제로 변경되며, 기존의 Request와 Response 객체는 소멸하고 새로운 객체가 생성됩니다. 시스템 상태를 변경하는 작업(예: 글쓰기 성공 후 목록으로 이동) 이후에는 새로고침 시 중복 요청을 방지하기 위해 리다이렉트를 사용하는 것이 바람직합니다.