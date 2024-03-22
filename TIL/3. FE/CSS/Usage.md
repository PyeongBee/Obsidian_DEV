### 1. 마우스 호버 시 손가락
```css
.container:hover {
	cursor: pointer;
}
```

### 2. 긴 text ... 처리
```css
.txt_line {
	width: 100px;
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
}
```
- Block 레벨 태그에서 적용한다. (p, div, typography, ...)
- width가 fix되어야 적용된다.
- 그 하위 레벨에는 적용 안되니 주의하자.
- **overflow:hidden** : 넓이가 70px를 넒어서는 내용에 대해서는 보이지 않게 처리함
- **text-overflow:ellipsis** : 글자가 넓이 70px를 넘을 경우 생략부호를 표시함
- **white-space:nowrap** : 공백문자가 있는 경우 줄바꿈하지 않고 한줄로 나오게 처리함 (\A로 줄바꿈가능)