## Spring MVC

### MVC 란?
* MVC 패턴은 애플리케이션의 개발 영역을  MVC(Model, View, Controller)로 구분하여 각 역할에 맞게 코드를 작성하는 개발 방식이다.
* MVC 패턴의 도입으로 UI 영역과 도메인(비즈니스 로직) 영역으로 구분되어 서로에게 영향을 주지 않으면서 개발과 유지보수가 가능하게 되었다.

### M(Model) / V(View) / C(Controller)
   * **Model(모델)**
      * 데이터나 비즈니스 로직을 관리하는 부분
      * 클라이언트의 요청 사항을 구체적으로 처리하는 영역을 서비스 계층
      * 요청사항을 처리하기 위해 Java 코드로 구현한 것을 비즈니스 로직이라고 한다.
   * **View(뷰)**
      * 보여줄 값(모델)을 컨트롤러로부터 받아와 사용자에게 보여주는 역할
      * 웹 브라우저와 같은 애플리케이션의 화면에 보이는 리소스를 제공한다.
   * **Controller(컨트롤러)**
      * 클라이언트 측의 요청을 직접적으로 전달받는 엔드포인트로써 모델과 뷰의 중간에서 상호작용하는 역할
      * 클라이언트 측의 요청을 전달받아 비즈니스 로직을 거친 후, Model 데이터가 만들어지면, 이 Model 데이터르 ㄹView로 전달하는 역할을 한다.

### Spring MVC
Spring MVC 는 DispatcherServlet, View Resolver, Interceptor, Handler, View 등올 구성되어 있으며, 이 중 DispatcherServlet 이 가장 앞단의 front controller 역할을 하며 가장 핵심적인 역할을 한다.

* Servlet(서블릿)
   * Servlet 은 클라이언트의 요청을 처리하도록 특정 규약에 맞춰 Java 코드로 작성하는 클래스 파일이다.
   * 아파치 톰캣은 이러한 서블릿들이 웹 애플리케이션으로 실행할 수 있도록 해주는 서블릿 컨테이너(Servlet Container) 중 하나이다.
   * Spring MVC 내부에서는 서블릿을 기반으로 웹 애플리케이션을 동작하며, Spring Boot 는 기본적으로 아파치 톰캣이 내장되어 있다.
   
* DispatcherServlet
   * DispatcherServlet 은 HttpServlet을 상속받아 사용하고, 서블릿으로 동작한다.
   * DispatcherServlet → FrameworkServlet → HttpServletBean → HttpServlet
   * DispatcherServlet 을 사용하면 서블릿으로 등록하면서 모든 경로에 대해 매핑한다. (urlPatterns="/")

* 요청 흐름
   * Servlet 이 호출되면 HttpServlet 이 제공하는 service()가 호출된다.
   * Spring MVC 는 FrameworkServlet.service() 를 시작으로 여러 메서드가 호출되면서 DispatcherServlet.doDispatch() 이 최종적으로 호출된다. 

![image](https://user-images.githubusercontent.com/118621835/222413746-14f1d0bf-69b2-4c65-b912-8a4926908381.png)

* 동작 과정
   * (1) DispatcherServlet 이 모든 웹 브라우저로부터 요청을 받는다.
   * (2) DispatcherServlet 은 HandlerMapping 으로부터 주어진 request 를 처리할 수 있는 Handler 객체를 가져온다. (URL 에 매핑된 Handler(컨트롤러)를 조회)
   * (3) 가져온 Handler 를 실행(invoke)시킬 수 있는 HandlerAdapter 객체를 가져온다.
   * (4) 만약 해당 Controller 를 처리할 Handler 객체에 적용할 interceptor 가 존재한다면 모든 interceptor 객체의 preHandle 메소드를 호출한다.
   * (5) HandlerAdapter 객체를 통해 실제 컨트롤러의 메소드를 실행 후 ModelAndView 를 얻는다.
   * (6) 만약 해당 Controller 를 처리할 Handler 객체에 적용할 interceptor 가 존재한다면 모든 interceptor 객체의 postHandle 메소드를 호출한다.
   * (7) DispatcherServlet 은 5번에서 얻은 ModelAndView 를 통해서 view name 을 ViewResolver 에게 전달하여 응답에 필요한 View 객체를 얻어온다.
   * (8) DispatcherServlet 은 7번 과정에서 얻은 View 객체에 5번 과정에서 얻은 ModelAndView 의 Model 을 파라미터로 넘겨주어 render 메소드를 호출하여 페이지 렌더링을 수행한다.
   * (9) DispatcherServlet 은 렌더링된 페이지를 response 로 사용자에게 리턴한다.






참조
* [Spring의 MVC 패턴과 MVC1과 MVC2 비교](https://chanhuiseok.github.io/posts/spring-3/)
* [스프링 MVC란 무엇인가? - 스프링 MVC 구조 이해](https://ittrue.tistory.com/234)
* [Spring MVC 동작 과정](https://jeonyoungho.github.io/posts/Spring-MVC-%EB%8F%99%EC%9E%91-%EA%B3%BC%EC%A0%95/)