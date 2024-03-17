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

### 컴포넌트 스캔 `@ComponentScan`
- 스프링은 생성 단계와 주입 단계가 나눠져 있다.
- AppConfig 안에 하나하나 `@Bean` 붙여서 스프링 컨테이너에 등록해주지 않아도, `@ComponentScan`만 붙여주면 해당 AppConfig가 속한 패키지 내에 있는 `@Component`를 모두 컨테이너에 등록한다.
- `excludeFilter`를 통해 등록하지 않을 Component를 선택할 수 있다.
```java
// 스프링 컨테이너 수동 등록
@Configuration  
public class AppConfig {  
    @Bean  
    public MemberService memberService() {  
        return new MemberServiceImpl(memberRepository());  
    }
	...
}

// 스프링 컨테이너 자동 등록
@Configuration
@ComponentScan
public class AutoAppConfig {
}
```

### 자동 주입 `@Autowired`
- 위 컴포넌트 스캔을 활용하면, 하나하나 빈 등록을 하지 않아도 된다는 장점이 있다. 그런데, 위의 예시에서 처럼 `MemberService`는 구현체가 `memberRepository` 의존성 주입을 필요로 한다. 이걸 어디서 넣어줄까?
- 스프링 빈을 등록할 때 필요한 의존성들은 `생성자 주입, 수정자 주입, 필드 주입, 메소드 주입`의 방법으로 주입할 수 있다.
- `생성자, 수정자, 필드, 메소드`에 `@Autowired`만 붙임으로써 주입해줄 수 있다.

#### 1. 생성자 주입
```java
public class MemberServiceImpl implements MemberService {
	private final memberRepository;

	@Autowired
	public MemberServiceImpl(MemberRepository memberRepository) {
		this.memberRepository = memberRepository;
	}
}
```
- 서비스의 구현체 의존성은 통상적으로 한 번 세팅해두면 바꿀 일이 없다. **불변!**
- `final`을 사용할 수 있다. **불변성**을 더 잘 살릴 수 있다.
- 컴파일 단계에서 의존성이 빠진 것을 알 수 있다.

#### 2. 수정자(Setter) 주입
```java
public class MemberServiceImpl implements MemberService {
	private memberRepository;

	@Autowired
	public setMemberRepository(MemberRepository memberRepository) {
		this.memberRepository = memberRepository;
	}
}
```
- setter를 활용해 의존성을 주입하는 방법이다.
- 구현체를 선택하거나 변경의 여지가 있는 의존관계에서 사용한다.
- 기본적으로 `@Autowired` 어노테이션은 `@Autowired(required = true)`다. 필요한 의존성이 null이면 오류가 나는 것이 기본이다.
- `required = false` 설정을 통해 null일 경우 메소드 호출을 하지 않도록 설정할 수 있다.
- 혹은 호출을 하더라도 `@Nullable, Optional<T>`를 활용해 오류가 발생하지 않도록 할 수 있다.

#### 3. 필드 주입
```java
public class MemberServiceImpl implements MemberService {
	@Autowired private memberRepository;
}
```
- 매우 간단한 주입 방법으로 개발자들에게 사랑 받았지만, DI 컨테이너가 아닌 외부에서, 가령 **테스트를 할 때, 의존성을 주입할 방법이 없다.**
- 스프링을 재부팅하는 등의 방법으로만 테스트가 가능하기 때문에... 쓰이지 않는다.
- 인텔리제이도 추천하지 않는 방법이라고 경고를 한다.

#### 4. 메소드 주입
```java
public class OrderServiceImpl implements OrderService {
	private orderRepository;
	private discountPolicy;

	@Autowired
	public init(MemberRepository memberRepository, DiscountPolicy discountPolicy) {
		this.memberRepository = memberRepository;
		this.discountPolicy = discountPolicy;
	}
}
```
- 수정자 주입과 결이 비슷하다.
- 다만, 수정자 주입과는 달리 여러 의존성을 묶어서 주입할 수 있다.
- 잘 쓰이지 않는다.