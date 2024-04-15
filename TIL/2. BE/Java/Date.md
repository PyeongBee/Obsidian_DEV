### 0. Date를 사용하는 대참사는 피하자
예제 : [2021년에 Calander 사용하는 참사](https://grandj.tistory.com/324)
예제 : [[String으로 받은 날짜 형태 변경](https://deersoul6662.tistory.com/71)](https://deersoul6662.tistory.com/71)
예제 : [# 자바 날짜 포맷 변경 방법](https://junghn.tistory.com/entry/JAVA-%EC%9E%90%EB%B0%94-%EB%82%A0%EC%A7%9C-%ED%8F%AC%EB%A7%B7-%EB%B3%80%EA%B2%BD-%EB%B0%A9%EB%B2%95SimpleDateFormat-yyyyMMdd)

### 1. Java 8 - LocalDate
> java.util.date 로 쩔쩔 고생했던게 엊그제 같은데 진작 8로 갈아탈걸 그랬다.

#### 자주 사용하는 것들
##### 1. **현재 날짜 반환**
```java
LocalDate localDate=LocalDate.now();  
System.out.println(localDate.toString());//(현재기준)2018-09-11 출력
```
##### 2. **현재 날짜의 다양한 요소 반환**
```java
System.out.println(localDate.getDayOfYear());//365일 중 며칠인지?  
System.out.println(localDate.getDayOfMonth());//오늘이 며칠인지?, 254  
System.out.println(localDate.getDayOfWeek());//무슨 요일인지?, 11  
System.out.println(localDate.getDayOfWeek().getValue());//무슨 요일인지?(월-1 ~일-7), 2  
System.out.println(localDate.getMonth());//September출력  
System.out.println(localDate.getMonthValue());//9출력  
System.out.println(localDate.getYear());//2018출력

// 해당 월의 마지막 날
System.out.println(localDate.lengthOfMonth());// 30, 31, 28, 29 출력

// 년월까지 포함한 마지막 날
System.out.println(localDate.withDayOfMonth(localDate.lengthOfMonth())) // 2023-05-31
```


##### 3. **날짜 변형**
```java
System.out.println(localDate.plusDays(1));//하루 뒤 출력  
System.out.println(localDate.plusWeeks(1));//한 주 뒤 출력  
System.out.println(localDate.plusYears(1));//일년 뒤 출력  
​  
System.out.println(localDate.withDayOfMonth(8));//8일로 변경하여 출력 - 2018-09-08  
System.out.println(localDate.withDayOfYear(12));///그 해의 12일로 변경하여 출력 - 2018-01-12  
System.out.println(localDate.withMonth(10));//10월로 변경하여 출력 - 2018-10-11  
System.out.println(localDate.withYear(2012));//2012년으로 변경하여 출력 - 2012-09-11
```

##### 4. YearMonth를 활용한 달의 마지막날 구하기
```java
//기준일자
LocalDate date = LocalDate.parse("2022-09-04");
//YearMonth
YearMonth month = YearMonth.from(date);
//해당 월의 첫째 날
LocalDate firstDate = month.atDay(1); // 2022-09-01
//해당 월의 마지막 날
LocalDate lastDate = month.atEndOfMonth(); // 2022-09-30
```

##### 5. 불변인 localDate 바꾸기
참고 : https://dev-cho.tistory.com/46

### 2. LocalDate, LocalTime, LocalDateTime
참고 : https://www.daleseo.com/java8-local-date-time/