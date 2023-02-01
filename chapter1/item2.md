# 타입스크립트 설정 이해하기
타입스크립트 설정에 대한 내용을 담은 파일

```json
// tsconfig.json
// $ tsc --init 으로 생성
{
    "compilerOptions": {
        "noImplicitAny": true // 변수들이 미리 정의한 타입을 가지고 있어야 하는지에 대한 여부 제어
    }
}
```
<br>

위의 속성이 꺼져있다면 타입을 미리 정의하지 않아도 오류가 발생하지 않고, 암시적으로 any 형식이 포함된다.
<br><br>

켜져있다면 명시적으로 분명한 타입을 선언해주자.
```typescript
function add (a: number, b: number) {
    return a + b;
}
```

위의 설정을 해제하는 것은 타입스크립트로의 마이그레이션 이외에는 지양한다.

## strictNullChecks
null, undefined가 모든 타입에서 허용되는지 확인하는 설정
```typescript
// strictNullChecks 설정 해제 시
const x: number = null;
// 설정 시
const x: number = null; // null 형식은 number 형식에 할당할 수 없습니다.
```

의도적으로 null을 명시하는 방법이 있다.
```typescript
const x: number | null = null;
```
해당 설정 없이는 'undefined는 객체가 아닙니다.' 라는 무서운 런타임 오류를 만날 가능성이 높다...