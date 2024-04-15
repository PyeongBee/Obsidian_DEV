[오라클 Error Docs](https://docs.oracle.com/cd/E11882_01/server.112/e17766/e0.htm)

### 1. Auto increment
- Oracle 에서는 MySql에 있는 Auto_Increment 기능이 없다.
- 자동으로 인덱스 값을 증가시키기 위해서는 시퀀스를 생성해서 사용해야한다.
```sql
CREATE TABLE TB1 (
	IDX NUMBER(10),
	NAME VARCHAR2(100)
);

CREATE SEQUENCE TB1_SEQ START WITH 1 INCREMENT BY 1 MAXVALUE 10000 CYCLE NOCACHE;

INSERT INTO TB1 VALUES(TB1_SEQ.NEXTVAL, 'haha');
```
- MINVALUE : 시퀀스가 시작되는 최초의 숫자
- MAXVALUE : 시퀀스가 끝나는 최대 숫자
- INCREMENT BY : 시퀀스가 증가하는 단위
- START WITH : 시퀀스 생성이 시작되는 값
- NOCACHE : 캐시를 사용하지 않음
- NOORDER : 요청되는 순서대로 값을 생성하지 않음
- NOCYCLE : 초기 값부터 다시 시작하지 않음

### 2. Oracle 12c 이후 Auto increment
```sql
GENERATED [ ALWAYS | BY DEFAULT [ ON NULL ] ] AS IDENTITY [ ( identity_options ) ]
```

```sql
CREATE TABLE TB2 (
	IDX INT GENERATED ALWAYS AS IDENTITY,
	NAME VARCHAR2(100)
);

INSERT INTO TB1 VALUES('haha');
```

### 3. Sequence CURRVAL
```sql
SELECT SEQ.CURRVAL FROM DUAL;

>> ORA-08002 : 시퀀스 SEQ.currval 은 이 세션에서는 정의되어 있지 않습니다
```
- 다짜고짜 CURRVAL을 조회하면, 위와 같은 오류가 발생한다.
- sequence CURRVAL has been selected before sequence NEXTVAL
- 현재 세션의 CURRVAL을 조회하기 때문에, NEXTVAL로 세션을 잡고 CURRVAL을 조회해야 한다.
- 세션 1에서 NEXTVAL 후, CURRVAL 조회 시 100이었다고 가정하자. 세션 2에서 NEXTVAL 후, CURRVAL 조회 시에는 101이다. 하지만 세션 1에서 다시 조회를 해도 100이 나온다.

참고 : https://mkil.tistory.com/218

### 4. EXISTS/NOT EXISTS vs JOIN
```sql
SELECT NAME, COST, CITY
  FROM PRODUCT AS P
 WHERE NOT EXISTS ( 
	SELECT ID 
      FROM SALE 
     WHERE YEAR = 2020 AND PRODUCT_ID = P.ID
 );

==>

SELECT P.NAME, P.COST, P.CITY
  FROM PRODUCT AS P
  LEFT JOIN SALE AS S
    ON P.ID = S.PRODUCT_ID
 WHERE S.YEAR != 2020 OR S.YEAR IS NULL;
```

> - **EXISTS는 상황에 따라 조인(JOIN) 보다 수행시간이 더 빠를 수도 있다.**  
> - **EXISTS의 경우는 inner query를 만족하는 레코드를 처음 만나는 순간 EXISTS가 true이므로 inner query를 더 이상 평가하지 않는다.**  
> - **그래서 일반적으로 EXISTS보다 JOIN 속도가 빠르다고 하지만, 중복된 값이 많이 나올 경우에는 EXISTS가 더 빠르다.**

참고 : https://jason-heo.github.io/mysql/2014/05/22/avoid-mysql-in.html
