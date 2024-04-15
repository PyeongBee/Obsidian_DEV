### 1. String 구분자로 split 후 List로 변환
```Java
String srcList = "haha,jaja";
String[] splitList = srcList.split(",");

List<String> ls = Arrays.asList(splitList);

>> [haha, jaja]
```

#### 1-1. 공백 제거
```Java
String srcList = "haha,jaja, baba,  tata, kaka  ";
String[] splitList = srcList
						.trim() // 양쪽 공백 제거
						.split("\\s*,\\s*"); // 사이 공백 제거 후 split

List<String> ls = Arrays.asList(splitList);

>> [haha, jaja, baba, tata, kaka]
```

### 2. Json data를 객체로 변환
respose data가 다음과 같다.
```json
{
	status: 'Y'
	data: {
		name: 'haha',
		old: 20
	}
}
```
이를 객체로 변환하려면 다음과 같이 작성하자.
```Java
JsonNode responseJson = objectMapper.readTree(response);
String status = responseJson.get("status").asText();
String name = responseJson.get("data").get("name").asText();
int old = responseJson.get("data").get("old").asText();
```

### 3. Function default 값
- Java는 default 값을 지원하지 않는다.
```java
public static void func(int a = 5, int b) { // a = 5 이거 안됨.
	return a + b
}
```

### 4. record 커스텀 생성자
```java
public record StudentDTO (
	String name,
	int rollNo,
	int marks,
	String id
) {
    public StudentDTO (String name, int rollNo, int marks) {
        this(
	        name,
	        rollNo,
	        marks,
	        UUID.randomUUID().toString()
	    );
    }
}
```

### 5. final과 불변성
- final은 값이 정해져서 바뀌면 안되는 마지막 값을 의미한다.
- null일 수 없다.
- final은 정확히는 재할당만 금지한다.
```java
final Map<String, boolean> collection = new HashMap<>();

collection.put("name", "hans"); // 가능

collection = new HashMap<>(); // 불가능
```

### 6. String을 합치는 방법
참고 : [StringBuilder, StringBuffer, + 연산자, concat 비교](https://futurecreator.github.io/2018/06/02/java-string-concatenation)
참고 : [String.Join vs. StringBuilder: which is faster?](https://stackoverflow.com/questions/585860/string-join-vs-stringbuilder-which-is-faster)
참고 : [concat, + 연산자, StringBuilder](https://devdy.tistory.com/9)
참고 : [StringJoining.class and String.join()](https://parkhyeokjin.github.io/java/2019/07/18/StringJoining.html)
참고 : [Performance for Java Stream.concat VS Collection.addAll](https://stackoverflow.com/questions/41622027/performance-for-java-stream-concat-vs-collection-addall)

#### 1. String.join()
- 버전 : JAVA8

### 7. String Byte 수로 글자수 계산
참고 : [java 한글을 2byte로 취급하여 substring 하는 함수](https://databook.tistory.com/39)
참고 : [String Byte 계산 성능 비교](https://programmingsummaries.tistory.com/239)
참고 : [인코딩에 따른 차이](https://hgko1207.github.io/2021/03/10/java-dev-6/)

### 8. Char 비교
```java
str.charAt(i) == "1"
```

이건 틀렸다. charAt은 **char**이고, "1" 이건 **string** 이라서 비교가 안된다.
따라서, " " -> ' ' 이렇게 바꾸면 해결된다.

```java
str.charAt(i) == '1'
```

