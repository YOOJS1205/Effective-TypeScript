# any 타입 지양하기

### 1. any 타입에는 타입 안전성이 없다.

```typescript
let age: number;
age = "12" as any;

age += 1;
console.log(age); // '121'
```

### 2. any는 함수 시그니처를 무시한다.

약속된 타입의 입력을 제공하고, 약속된 타입을 출력을 반환하는 시그니처를 무시할 수 있다.

```typescript
function calculateAge(birthDate: Date): number {
  // ...
}

let birthDate: any = "1990-01-19";
calculateAge(birthDate); // 정상
```

### 3. any 타입에는 언어 서비스가 적용되지 않는다.

자동 완성 서비스와 도움말을 제공받을 수 없다.

### 4. any 타입은 코드 리팩터링 때 버그를 감춘다.

### 5. any는 타입 설계를 감춰버린다.

### 6. any는 타입시스템의 신뢰도를 떨어뜨린다.
