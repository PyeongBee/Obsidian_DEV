### 1. 파라미터 대소문자 구분
- FE와 BE 간 통신 시, 파라미터 명의 대소문자를 구분한다는 점을 주의하자.
```javascript
alcrCnt != AlcrCnt
```
### 2. BE를 통해 받은 response.data는 promise 형태
- `then`을 통해 풀어줘야 한다.
```javascript
response.then((res) => console.log(res));
```

### 3. index.js에서 import 모으기
```javascript
export { default as Title } from "./Title";
export { default as Content } from "./Content";
export { default as Subtitle } from "./Subtitle";
export * from "./Console";
```
- index.js 에서 필요한 모든 파일을 import
- default로 export하면 항목들이 겹치기 때문에, as 키워드를 활용

### 4. string 공백인지 체크
```js
string str = '  ';
if (str.trim() === '') return true;
```
- `trim()`을 활용해 확실하게 체크하자.

### 5. 마지막 문자 제거
```js
var str = 'HTML, CSS, JavaScript, ';
str = str.slice(0, -2);
```

### 6. Set
- Set는 배열과 달리, 데이터를 순서 없이 저장한다.
- 배열처럼 인덱스를 통해서 접근할 수가 없다.
- Set는 중복된 데이터를 허용하지 않는다.
- 값 존재 여부 확인 : has("A") - 개수 비교하지 말자.

### 7. Set 객체 <-> 배열 변환
```js
const set = new Set([1, 2, 3]);

const arr = Array.from(set);

const newSet = new Set(arr);
```

> Array.from 함수는 유사 배열 객체나 반복 가능 객체를 얕은 복사(shallow copy)하여 새로운 배열(Array) 객체를 만들어줍니다.
>- **유사 배열 객체(array-like object) :** length 속성과 index element를 가지는 객체
>- **반복 가능 객체(iterable object) :** 배열을 일반화한 객체 ex)Map, Set