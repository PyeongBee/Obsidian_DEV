> ORA-00932: 일관성 없는 데이터 유형: -이(가) 필요하지만 CLOB임

```sql
SELECT DISTINCT SOME_SEQ(NUMBER형 컬럼), SOME_CLOB(CLOB형 컬럼)
  FROM DEMO_TABLE
```
**결론!** DISTINCT를 사용할 때 CLOB형 컬럼이 있으면 원하는 기능이 실행되지 않는다. 
DISTINCT를 사용하고 싶다면 CLOB형 컬럼은 제외하고 사용해야 한다.