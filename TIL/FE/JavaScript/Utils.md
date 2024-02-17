### 1. string "20231201" -> Date
```javascript
dayjs('20231201', 'YYYYMMDD').toDate()
```

### 2. 달의 시작날짜, 끝날짜
```js
dayjs().startOf('month')
dayjs().endOf('month')
```