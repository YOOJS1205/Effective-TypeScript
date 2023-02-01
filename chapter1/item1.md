# 타입스크립트와 자바스크립트의 관계 이해하기
타입스크립트는 자바스크립트의 상위 집합(superset)이다.
<br><br>
그 말은, 자바스크립트의 코드는 곧 타입스크립트의 코드이기도 하다. (타입 지정이 없다 하더라도)
<br>
하지만, 역은 성립하지 않는다. (타입스크립트는 타입을 명시하는 추가적인 문법이 있기 때문)
<br><br>

```typescript
// 아래의 코드는 유효한 타입스크립트 코드이다.
// 하지만, 자바스크립트를 구동하는 노드에서 실행하면 오류가 발생한다.
function greet(who: string) {
    console.log('Hello', who);
}
```

타입 체커의 장점 1
```javascript
// 노드에서 실행 시
let city = 'new york city';
console.log(city.toUppercase()); // TypeError: toUppercase is not a function
```

```typescript
// 타입 체커
let city = 'new york city';
console.log(city.toUppercase()); // toUpperCase를 사용하시겠습니까?
```
즉, 런타임에 오류를 발생시킬 코드를 미리 찾아준다. (타입스크립트가 정적 언어인 이유)
<br><br>

타입 체커의 장점 2
```javascript
// 의도하지 않은 결과 출력
const states = [
    { name: 'Alabama', capital: 'Montgomery' },
    { name: 'Alaska', capital: 'Juneau' },
    { name: 'Arizona', capital: 'Phoenix' },
];

for (const state of states) {
    console.log(state.capitol);
}

// undefined
// undefined
// undefined
```

```typescript
const states = [
    { name: 'Alabama', capital: 'Montgomery' },
    { name: 'Alaska', capital: 'Juneau' },
    { name: 'Arizona', capital: 'Phoenix' },
];

for (const state of states) {
    console.log(state.capitol);
}

// 'capital'을(를) 사용하시겠습니까?
```
<br>

타입을 더욱 명확하게 지정해서 오류를 바로잡을 수 있다.
```typescript
interface State {
    name: string;
    capital: string;
}

const states: State[] = [
    { name: 'Alabama', capital: 'Montgomery' },
    { name: 'Alaska', capital: 'Juneau' },
    { name: 'Arizona', capital: 'Phoenix' },
]
```
<br>

**타입스크립트의 타입 시스템은 자바스크립트의 런타임 동작을 모델링한다.**