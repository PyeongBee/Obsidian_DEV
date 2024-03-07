- 객체 지향 프로그래밍은 프로그램을 객체들의 모임으로 생각하는 것
- 각 객체는 메시지를 주고 받고 데이터를 처리할 수 있다.
- 객체 지향 프로그래밍은 프로그램을 **유연하고 변경에 용이**하게 만든다.

### **객체 지향의 정수 : 다형성 (polymorphism)**
다형성의 실세계 비유 : **역할**과 **구현**을 분리한다.
![[Pasted image 20240226234641.png]]
- 자동차가 K3에서 아반떼로 바뀌어도 악셀과 브레이크의 동작은 그대로기에, 운전자는 자동차가 바뀌는 여부에 상관 없이 운전을 할 수 있다.

![[Pasted image 20240226234853.png]]
- 로미오 역할을 장동건이 하고 줄리엣 역할을 김태희가 한다.
- 줄리엣 역할이 송혜교, 무명 배우로 바뀌어도 로미오 역할의 장동건은 상관 없다.
- 로미오 역할만 잘하면 된다.
- 줄리엣 역할의 구현이 바뀌어도 로미오 역할은 상관이 없는 것이다.

### 관심사의 분리
위 공연 무대의 예시에서 로미오 역할을 하는 배우 장동건이 '나는 줄리엣 역할로 김태희 배우 아니면 안 해.'라고 하면 어떨까? 배우 송혜교가 줄리엣 역할을 할 경우, 배우 장동건이 로미오 역할을 제대로 해내지 못한다는 것이다. 코드로 표현하면 아래와 같다.

```Java
public Class 장동건 implements 로미오역할 {
	@Overide
	public void 공연() {
		줄리엣역할 줄리엣 = new 김태희();
		장동건의연기(줄리엣.김태희의손)
	}
}
```
- 줄리엣을 김태희로 정해놓았다.
- 장동건의 연기에는 줄리엣인 김태희의 손이 필요하다.
- 배우가 송혜교로 바뀌면 줄리엣에는 김태희의 손이 없기 때문에 오류가 발생한다.

로미오 역할의 장동건이 줄리엣 역할의 배우를 김태희로 정해놓은 것이다. 로미오 역할을 하는 사람이 로미오 연기 뿐만 아니라 줄리엣 배우 초빙까지 한 것이다. **SRP([[5 Principles#SRP]])** 를 위배한다.

SRP를 지키기 위해서는 배우 초빙의 역할을 따로 분리해야 한다. 공연 기획자가 나와야할 시점이다.

### AppConfig
- 구현체는 직접 인터페이스의 구현체를 정하면 안된다. 누군가가 주입해줘야 한다. 그것이 AppConfig이다.
- 애플리케이션의 동작을 구성하기 위해, 구현 객체를 생성하고 연결하는 책임을 진다.

#### 1. 생성자 주입
```java
// MemberServiceImpl - 구현 (MemberRepository 구현체 의존성 없음)
public Class MemberServiceImpl implements MemberService {
	MemberRepository memberRepository;
	
	public MemberServiceImpl (MemberRepository memberRepository) {
		this.memberRepository = memberRepository;
	}
	...
}
```

```java
// AppConfig - 구성 (MemberRepository에 MemoryMemberRepository 의존성 주입)
public Class AppConfig {
	public MemberService memberService() {
		return new MemberServiceImpl(new MemoryMemberRepository());
	}
	...
}
```

```java
// MemberController - 실행
public Class MemberController {
	AppConfig appConfig = new AppConfig();
	MemberService memberService = appConfig.memberService();
	...
}
```

### 2. 관심사의 분리로 적용한 객체지향 5원칙
- [[5 Principles#1. SRP 단일 책임의 원칙 (Single Responsibility Principle)]]
	- **하나의 클래스는 하나의 역할만 한다.**
	- 로미오는 로미오 역할만. 배우 선택은 기획자가 한다.
	- MemberServiceImpl은 MemberService 역할에 충실하고, MemberRepository 구현체는 AppConfig가 구성한다.
- [[5 Principles#2. OCP 개방 폐쇄의 원칙 (Open Close Principle)]]
	- **SW 요소는 확장에는 열려 있으나, 변경에는 닫혀 있어야 한다.**
	- 애플리케이션를 구현 영역과 구성 영역으로 나눴다.
	- MemberRepository 구현체가 바뀌어도, MemberService는 바뀌지 않는다.
	 -> 확장에는 열려있고, 변경에는 닫혀있다.
- [[5 Principles#5. DIP 의존성 역전의 원칙 (Depenedency Inversion Principle)]]
	- **개발자는 추상화에 의존해야 하고, 구체화에 의존하면 안된다.**
	- 로미오는 줄리엣 역할의 배우가 누군지에 의존하지 않는다.
	- MemberService에는 MemberRepository 구현체에 대한 의존성이 주입되지 않는다.

### IOC(Inversion Of Contrl, 제어의 역전)
- C언어를 생각해봐도 그렇지만, 기존 프로그램은 순차적으로 실행되게 되어 있다. 프로그램을 보면 변수 선언하고 초기화하고 로직이 있고 ... 그 프로그램 내에서 모든 것을 정의하고 수행한다. 구현체가 프로그램이 어떻게 흘러갈 지 제어의 흐름을 모두 관리한다. 개발자로서 아주 자연스러운 흐름이다.
- 하지만, 설정 정보는 AppConfig와 같은 설정 영역으로 분리를 함으로써 구현체는 로직을 실행하는 역할만 담당하게 된다. 프로그램의 제어 흐름은 AppConfig가 가져간다.
- 심지어, 구현체를 생성하는 것 또한 AppConfig가 가져간다.
- **구현 영역과 설정 영역을 분리함으로써, 프로그램의 제어 흐름을 직접 제어하는 것이 아니라 외부에서 관리하는 것을 제어의 역전, IOC이라고 한다.**

