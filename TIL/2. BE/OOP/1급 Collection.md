### 1급 컬렉션 (일급 컬렉션, First-class collection)
참고 : https://jojoldu.tistory.com/412
Collection을 wrapping하면서, 그 외 다른 멤버 변수가 없는 객체를 일급 컬렉션이라고 한다.
특정한 로직, 기능이 있는 자료구조를 만든다고 생각하면 된다.
```java
public class Pay { // 일반 객체
	@Getter private name;
	@Getter private amount;
}

public class PayGroup { // 1급 컬렉션
	private List<Pay> pays;

	public PayGroup(List<Pay> pays) {
		this.pays = pays;
	}

	public Long getPaySum() {
		return pays.stream().mapToLong(Pay::getAmount).sum();
	}
}
```
#### 장점
1. 비즈니스 에 종속적인 자료구조
	- 서비스 메소드에서 비즈니스 로직을 모두 처리하면 문제가 발생한다.
	- 서비스에서 처리한다고 하면, 해당 객체가 사용되는 서비스에서는 모두 똑같은 동작이 반복해서 작성되는 문제가 있다.
	- 이 객체에 종속되는 동작을 객체에 넣어주면 좋을 것 같지 않나?
2.  Collection의 불변성 보장
	-  final만 붙여준다고 불변이 아니기 때문에, Setter 없이 일급 컬렉션을 만들어준다면, 진짜 불변 컬렉션을 만들어줄 수 있다.
3. 상태와 행위를 한 곳에서 관리
	- 위의 PayGroup에서 볼 수 있듯이, pays의 값들을 모두 더하는 행위를 객체에 넣어줌으로써, 서비스에서는 해당 객체의 행위를 호출만 해주면 된다.
4. 이름이 있는 컬렉션
	- `List<Pay> pays`보다는 `PayGroup`이 좀 더 명확하지 않은가?!