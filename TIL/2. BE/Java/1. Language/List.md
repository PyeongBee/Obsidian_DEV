List를 초기화할 때 Arrays.asList()를 사용하는 경우가 있다. 그리고 단일 원소를 포함하는 리스트의 경우 인텔리제이는 singletonList를 사용하라고 권고한다.

단일 원소 리스트의 경우 singletonList를 사용해야할까? List.of에 하나만 넣는 것을 사용해야할까?

>Java 9 introduced factory methods to create _immutable_ lists with [`List.of()`](https://docs.oracle.com/javase/9/docs/api/java/util/List.html#of-E-) method.
>Which is more suitable to create an immutable list of one element?
>
> - `List<String> immutableList1 = List.of("one");`
> - `List<String> immutableList2 = Collections.singletonList("one");`

---
Prefer using factory method

```java
List<String> immutableList1 = List.of("one");
```

**Because** they disallow null elements is one of the benefit and also factory methods in `List` interface are handy to add multiple objects and creates immutable List

> They disallow null elements. Attempts to create them with null elements result in NullPointerException.

Where `Collections.singletonList` allows `null` value

```java
List<String> l = Collections.singletonList(null);
System.out.println(l);   //[null]
```
---
결론! 정적 팩토리 메서드를 사용하자.
참고 : [Arrays.asList() 와 List.of() 차이 한방 정리](https://inpa.tistory.com/entry/JAVA-%E2%98%95-ArraysasList-%EC%99%80-Listof-%EC%B0%A8%EC%9D%B4-%ED%95%9C%EB%B0%A9-%EC%A0%95%EB%A6%AC)

