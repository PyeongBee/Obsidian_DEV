- JPA를 위해서 Entity를 설계할 경우, 기본 생성자가 있어야 한다.
- 기본 생성자란 아무 파라미터도 없는 생성자 (NoArgsConstructor)를 의미한다.
- 그래서, @NoArgsConstructor 어노테이션을 붙여주면 해결된다.
- 그런데, 문제는 @NoArgsConstructor를 붙이는 순간, Class에 @Builder를 붙일 수 없다.

#### 1. JPA는 왜 기본 생성자가 있어야 하는가?
- 기본 생성자가 없으면 Hibernate와 같은 프레임워크가 엔터티를 초기화하지 못할 수 있다.
- 따라서, @Entity와 @NoArgsConstructor를 포함하는 것이 일반적인 관행이다.


@Builder: Lombok의 @Builder 주석은 클래스에 대한 빌더 패턴을 생성하므로 유창한 API로 인스턴스를 쉽게 구성할 수 있습니다. @Builder는 인수가 없는 생성자를 포함하여 생성자를 생성하지만 @NoArgsConstructor로 명시적으로 주석을 달지는 않습니다. 즉, 인수 없는 생성자를 명시적으로 제공하지 않고 @Builder를 사용하면 JPA에 문제가 발생할 수 있습니다.

Lombok의 @Builder와 함께 JPA를 사용하려면 몇 가지 옵션이 있습니다.