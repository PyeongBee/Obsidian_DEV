### 세팅 방법
1. build.gradle
```
// 아래 추가
configurations {  
    compileOnly {  
       extendsFrom annotationProcessor  
    }  
}

// dependencies 추가  
compileOnly 'org.projectlombok:lombok'  
annotationProcessor 'org.projectlombok:lombok'
```

2. Settings>Plugin>lombok 설치

3. Settings>Annotation Processors>Enable annotation processing 체크

### @Getter, @Setter
- Model의 getter, setter를 자동으로 만들어준다.

### @ToString
- Model의 ToString을 필드를 이용해 깔끔하게 만들어준다.

### @RequiredArgsConstructor
- 필요한 arguments로 생성자를 자동으로 만들어준다.
```java
// 기존 코드
@Service  
public class MemberServiceImpl implements MemberService{  
    private final MemberRepository memberRepository;

	public MemberServiceImpl(MemberRepository memberRepository) {
		this.memberRepository = memberRepository;
	}
	...
}

// @RequiredArgsConstructor 적용
@Service  
@RequiredArgsConstructor
public class MemberServiceImpl implements MemberService{  
    private final MemberRepository memberRepository;
	...
}
```