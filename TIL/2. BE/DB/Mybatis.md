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
