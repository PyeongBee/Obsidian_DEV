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
final은 정확히는 재할당만 금지한다.
```java
final Map<String, boolean> collection = new HashMap<>();

collection.put("name", "hans"); // 가능

collection = new HashMap<>(); // 불가능
```

### 6. String.join()
- 버전 : JAVA8
- 
