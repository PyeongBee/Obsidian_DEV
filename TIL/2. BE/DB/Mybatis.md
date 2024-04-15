### 1. bulk insert
```xml
<insert id="addList" parameterType="com.dto.Receiver$Info">
	INSERT INTO (
		   ID
		 , NAME
		 , OLD
	)
	VALUES
	<foreach collection="list" index="index" item="emp" separator=",">
	(
		#{emp.id},
		#{emp.name},
		#{emp.old}
	)
	</foreach>
</insert>
```

### 2. Mybatis Mapper XML
참고 : [Mybatis Mapper XML](https://m.blog.naver.com/PostView.nhn?isHttpsRedirect=true&blogId=songintae92&logNo=221225986681)

### 3. 리턴 값 int
참고 : https://dbelle.tistory.com/67

### 4. 리턴값이 왜 -1?
질문 : https://okky.kr/questions/912992

### 5. foreach
참고 : https://snowbro0314.tistory.com/45

### 6. selectKey
> 개발을 하다보면
> **INSERT => 특정 로직 수행 => UPDATE**
> 이런 형태로 구현을 해야 할 때가 있다.

참고 : [order 속성](https://cheezred.tistory.com/134)

>**keyProperty**: selectKey구문의 결과가 셋팅될 대상 프로퍼티.
>
>**keyColumn**: 리턴되는 결과셋의 칼럼명은 프로퍼티에 일치한다. 여러개의 칼럼을 사용한다면 칼럼명의 목록은 콤마를 사용해서 구분한다.  
>
>**resultType**: 결과의 타입. 마이바티스는 이 기능을 제거할 수 있지만 추가하는게 문제가 되지는 않을것이다. 마이바티스는 String을 포함하여 키로 사용될 수 있는 간단한 타입을 허용한다.  
>
>**order**: BEFORE 또는 AFTER를 셋팅할 수 있다. BEFORE로 설정하면 키를 먼저 조회하고 그 값을 keyProperty 에 셋팅한 뒤 insert 구문을 실행한다. AFTER로 설정하면 insert 구문을 실행한 뒤 selectKey 구문을 실행한다. 오라클과 같은 데이터베이스에서는 insert구문 내부에서 일관된 호출형태로 처리한다.  
>
>**statementType**: STATEMENT, PREPARED 또는 CALLABLE중 하나를 선택할 수 있다. 마이바티스에게 Statement, PreparedStatement 또는 CallableStatement를 사용하게 한다. 디폴트는 PREPARED 이다.  

출처 - https://deeplify.dev/back-end/spring/select-key

### 7. 파라미터 받아올 때 '#'과 '$'의 차이
참고 : https://mine-it-record.tistory.com/300

### 8. Enum 사용 시 TypeHandler
참고 : https://yonghwankim-dev.tistory.com/249
참고 : [커스텀 타입핸들러](https://goodgid.github.io/MyBatis-Handling-TypeHandler-Enum/)
예시 1: https://oedpus.tistory.com/entry/Mybatis-Enum-%EC%82%AC%EC%9A%A9

### 9. Enum 사용 시 name()을 확인하자
참고 : [Using enum parameters in myBatis dynamic SQL](https://stackoverflow.com/questions/12933813/using-enum-parameters-in-mybatis-dynamic-sql)

### 10. Null 처리
```xml
SELECT * 
  FROM SomeTable
 WHERE 1=1 
<if test="Parameter != null &amp;&amp; !Parameter.equals('')">
   AND Parameter = #{Parameter}
</if>
```
