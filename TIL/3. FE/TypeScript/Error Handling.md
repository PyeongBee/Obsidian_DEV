### '--isolatedModules' 에러 해결방법
TypeScript에 빈페이지가 있으면 아래같은 에러가 뜬다

```
cannot be compiled under '--isolatedModules' because it is considered a global script file. Add an import, export, or an empty 'export {}' statement to make it a module. TS1208
```

빈페이지에 `export {}` 입력 하면 에러 해결
