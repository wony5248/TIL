# Spring Bean
#### Spring Bean이란?
* Spring IoC 컨테이너가 관리하는 자바 객체를 빈(Bean)이라고 부릅니다. 이전 포스팅에서 제어의 역전 (IOC, Inversion Of Control)에 대하여 간략하게 알아보았는데요. IOC의 특징은 아래와 같습니다.
  * 일반적으로 처음에 배우는 자바 프로그램에서는 각 객체들이 프로그램의 흐름을 결정하고 각 객체를 직접 생성하고 조작하는 작업(객체를 직접 생성하여 메소드 호출)을 했습니다.
  * 즉, 모든 작업을 사용자가 제어하는 구조였습니다. 예를 들어 A 객체에서 B 객체에 있는 메소드를 사용하고 싶으면, B 객체를 직접 A 객체 내에서 생성하고 메소드를 호출합니다.
  * 하지만 IOC가 적용된 경우, 객체의 생성을 특별한 관리 위임 주체에게 맡깁니다. 이 경우 사용자는 객체를 직접 생성하지 않고, 객체의 생명주기를 컨트롤하는 주체는 다른 주체가 됩니다.
  * 즉, 사용자의 제어권을 다른 주체에게 넘기는 것을 IOC(제어의 역전) 라고 합니다.
#### Spring Bean 등록법
*  자바 어노테이션(Java Annotation)을 사용하는 방법
  * JAVA에서 Annotation 이라는 기능이 있습니다. 사전상으로는 주석의 의미이지만 Java 에서는 주석 이상의 기능을 가지고 있습니다. Annotation은 자바 소스 코드에 추가하여 사용할 수 있는 메타데이터의 일종입니다.
  * 소스코드에 추가하면 단순 주석의 기능을 하는 것이 아니라 특별한 기능을 사용할 수 있습니다.
* Bean Configuration File에 직접 Bean 등록하는 방법
  * @Configuration과 @Bean Annotation 을 이용하여 Bean을 등록할 수 있습니다. 아래의 예제와 같이 @Configuration을 이용하면 Spring Project 에서의 Configuration 역할을 하는 Class를 지정할 수 있습니다.
  * 해당 File 하위에 Bean 으로 등록하고자 하는 Class에 @Bean Annotation을 사용해주면 간단하게 Bean을 등록할 수 있습니다.
#### Spring Annotation
* @Component
  * 개발자가 생성한 Class를 Spring의 Bean으로 등록할 때 사용하는 Annotation입니다. Spring은 해당 Annotation을 보고 Spring의 Bean으로 등록합니다.
* @ComponentScan
  * Spring Framework는 @Component, @Service, @Repository, @Controller, @Configuration 중 1개라도 등록된 클래스를 찾으면, Context에 bean으로 등록합니다. @ComponentScan Annotation이 있는 클래스의 하위 Bean을 등록 될 클래스들을 스캔하여 Bean으로 등록해줍니다.
* @Bean
  * @Bean Annotation은 개발자가 제어가 불가능한 외부 라이브러리와 같은 것들을 Bean으로 만들 때 사용합니다.
* @Controller
  * Spring에게 해당 Class가 Controller의 역할을 한다고 명시하기 위해 사용하는 Annotation입니다.
* @RequestHeader
  * Request의 header값을 가져올 수 있으며, 해당 Annotation을 쓴 메소드의 파라미터에 사용합니다.
* @RequestMapping
  * @RequestMapping(value=”“)와 같은 형태로 작성하며, 요청 들어온 URI의 요청과 Annotation value 값이 일치하면 해당 클래스나 메소드가 실행됩니다. Controller 객체 안의 메서드와 클래스에 적용 가능하며, 아래와 같이 사용합니다.
* Class 단위에 사용하면 하위 메소드에 모두 적용됩니다.
  * 메소드에 적용되면 해당 메소드에서 지정한 방식으로 URI를 처리합니다.
* @RequestParam
  * URL에 전달되는 파라미터를 메소드의 인자와 매칭시켜, 파라미터를 받아서 처리할 수 있는 Annotation으로 아래와 같이 사용합니다. Json 형식의 Body를 MessageConverter를 통해 Java 객체로 변환시킵니다.
* @RequestBody
  * Body에 전달되는 데이터를 메소드의 인자와 매칭시켜, 데이터를 받아서 처리할 수 있는 Annotation으로 아래와 같이 사용합니다. 클라이언트가 보내는 HTTP 요청 본문(JSON 및 XML 등)을 Java 오브젝트로 변환합니다. 아래와 같이 사용합니다.
  * 클라이언트가 body에 json or xml 과 같은 형태로 형태로 값(주로 객체)를 전송하면, 해당 내용을 Java Object로 변환합니다.
* @ModelAttribute
  * 클라이언트가 전송하는 HTTP parameter, Body 내용을 Setter 함수를 통해 1:1로 객체에 데이터를 연결(바인딩)합니다. RequestBody와 다르게 HTTP Body 내용은 multipart/form-data 형태를 요구합니다. @RequestBody가 json을 받는 것과 달리 @ModenAttribute 의 경우에는 json을 받아 처리할 수 없습니다.
* @ResponseBody
  * @ResponseBody은 메소드에서 리턴되는 값이 View 로 출력되지 않고 HTTP Response Body에 직접 쓰여지게 됩니다. return 시에 json, xml과 같은 데이터를 return 합니다.
* @Autowired
  * Spring Framework에서 Bean 객체를 주입받기 위한 방법은 크게 아래의 3가지가 있습니다. Bean을 주입받기 위하여 @Autowired 를 사용합니다. Spring Framework가 Class를 보고 Type에 맞게(Type을 먼저 확인 후, 없으면 Name 확인) Bean을 주입합니다.
* @GetMapping
  * RequestMapping(Method=RequestMethod.GET)과 똑같은 역할을 하며, 아래와 같이 사용합니다.
* @PostMapping
  * RequestMapping(Method=RequestMethod.POST)과 똑같은 역할을 하며, 아래와 같이 사용합니다.
* @SpringBootTest
  * Spring Boot Test에 필요한 의존성을 제공해줍니다.
* @Test
  * JUnit에서 테스트 할 대상을 표시합니다.
