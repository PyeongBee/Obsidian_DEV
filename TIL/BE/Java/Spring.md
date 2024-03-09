### Spring의 핵심, 본질
스프링은 자바 기반의 프레임워크다.
자바의 가장 큰 특징은 객체 지향이다.
스프링이 나오기 전, EJB 시절에는 객체 지향이라는 본질이 무너지면서, POJO 개념도 나왔다.
스프링은 이 객체 지향을 가장 잘 살리는 프레임워크다.
스프링의 본질은 객체 지향이다.

### BeanDefinition
**BeanDefinitionName** : 생성할 빈의 클래스명 (자바 설정처럼 팩토리 역할의 빈을 사용하면 없음)
**factoryBeanName** : 팩토리 역할의 빈을 사용할 경우 이름 **ex) appConfig**
**factoryMethodName** : 빈을 생성할 팩토리 메서드 지정 **ex) memberService**
**Scope** : 싱글톤(기본값)
**lazyInit** : 스프링 컨테이너를 생성할 때 빈을 생성하는 것이 아니라, 실제 빈을 사용할 때까지 생성을 최대한 지연 처리 하는지 여부
**InitMethodName** : 빈을 생성하고, 의존관계를 적용한 뒤에 호출되는 초기화 메서드 명
**DestroyMethodName** : 빈의 생명주기가 끝나서 제거하기 직전에 호출되는 메서드 명
**Constructor args, Properties** : 의존관계 주입에서 사용한다. (자바 설정 처럼 팩토리 역할의 빈을 사용하면 없음)

#### BeanDefinition - AnnotationConfigApplicationContext
- 자바에서 Annotation 기반으로 AppConfig를 설정할 경우 Bean을 등록할 때 factoryMethod Pattern을 활용해서 우회하는 방법으로 등록한다.
- beanDefinition 정보에 class 정보가 null이고, factory 정보가 등록되어 있다.
- Xml 기반으로 설정할 때와 달리, AppConfig bean도 등록되어 있다.
- AppConfig bean은 Factory Bean의 역할을 한다.
- Generic bean은 AppConfig 하나이고, 나머지 Bean들은  Root bean으로 등록된다. (팩토리)
```java
// AppConfig Definition - Factory Bean 역할
beanDefinition = 
Generic bean: class [com.pyeongbee.honeyhubsvc.sample.AppConfig$$SpringCGLIB$$0];
scope=singleton; abstract=false; lazyInit=null; autowireMode=0; dependencyCheck=0; autowireCandidate=true; primary=false;
factoryBeanName=null; factoryMethodName=null;
initMethodNames=null; destroyMethodNames=null

// memberService Definition
beanDefinition = 
Root bean: class [null];
scope=; abstract=false; lazyInit=null; autowireMode=3; dependencyCheck=0; autowireCandidate=true; primary=false; 
factoryBeanName=appConfig; factoryMethodName=memberService; // 팩토리 정보 등록
initMethodNames=null; destroyMethodNames=[(inferred)];
defined in com.pyeongbee.honeyhubsvc.sample.AppConfig
```
#### BeanDefinition - GenericXmlConfigApplicationContext
- 자바에서 Xml 기반으로 AppConfig를 설정할 경우 Bean을 등록할 때 class를 바로 direct로 등록한다.
- beanDefinition 정보에 class 정보가 등록되어 있고, factory 정보가 null이다.
- Annotation 기반으로 설정할 때와 달리, AppConfig bean은 없다.
- Annotation 기반으로 설정할 때와 달리, 모두 Generic bean으로 등록된다.
```java
// memberService Definition
beanDefinition = 
Generic bean: class [com.pyeongbee.honeyhubsvc.sample.service.MemberServiceImpl];
scope=; abstract=false; lazyInit=false; autowireMode=0; dependencyCheck=0; autowireCandidate=true; primary=false; 
factoryBeanName=null; factoryMethodName=null; // 팩토리 정보 null
initMethodNames=null; destroyMethodNames=null;
defined in class path resource [appConfig.xml]
```

### @ComponentScan
https://yoons-development-space.tistory.com/73
