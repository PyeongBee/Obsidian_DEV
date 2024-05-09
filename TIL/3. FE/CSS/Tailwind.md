### 1. Next.js는 왜 Tailwind.css를 추천할까?
기존의 selector 기반 CSS는 다음과 같은 문제점을 설계상 가지고 있었다.

- Global namespace: 모든 스타일이 전역에 선언되기 때문에 겹치지 않는 class name의 필요
- Dependencies: 한 요소에 여러 CSS 규칙이 적용 가능하므로 관리가 어려움
- Dead Code Elimination: CSS가 JS와 분리되어 있으므로 기능 수정사항을 수동으로 동기화하는 어려움
- Minification: 겹치지 않게 class name 지정하려다 보니 길어지는 문제
- Sharing Constants: CSS가 분리돼 있어 JS의 상태 값을 공유하기 어려운 문제
- Non-deterministic Resolution: CSS 로드 순서에 따라 우선순위가 달라지는 문제
- Isolation: CSS는 부모로부터 스타일을 상속하므로 하위 컴포넌트에 영향

CSS-in-JS는 JS를 통해 CSS를 생성함으로써 위 문제를 커버하려는 방법이다.

- JS 내부에서 선언: 기능 수정 시 동기화가 용이, 상태 값 공유 가능
- 컴포넌트 단위로 적용: 한 요소에는 한 규칙, 로드 순서가 우선 순위에 영향을 주지 않음, 상속 제거
- class name 자동 생성: 빌드 타임에 짧고 유일한 이름을 지어줌