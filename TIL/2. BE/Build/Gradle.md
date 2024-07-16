### 1. Test 제외하고 Build하기
`gradle build -x test`

### 2. 특정 패키지 test 제외하고 Build하기
https://roomconerdeveloper.tistory.com/154
- gradle에 아래와 같이 추가해주자
```java
test {
    systemProperty 'spring.profiles.active', 'test'
    useJUnitPlatform {
        exclude("com/study/**/*.class")
    }
}
```