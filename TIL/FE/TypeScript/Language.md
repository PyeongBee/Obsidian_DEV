### 1. BE의 HashMap type 지정 (HashMap<string, string>)
```typescript
[data: string]: string;
```

### 2. ! 문법
```typescript
let x:number;

const fn1 = () => {
	x = 1;
}
fn1();
console.log(x + x);
```
- 위의 경우에 x가 초기화되지 않았다고 에러가 발생한다.
- 하지만, **변수 x의 값이 있다는 걸 확신할 수 있다면, ! 문법을 사용하자!**
```typescript
console.log(x! + x!);
```

### 3. type vs interface
