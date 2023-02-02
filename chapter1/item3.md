# 코드 생성과 타입이 관계없음을 이해하기

## 타입스크립트 컴파일러의 역할

1. 브라우저에서 동작할 수 있도록 구버전의 자바스크립트로 트랜스파일 한다.
2. 코드의 타입 오류를 체크한다.
   <br>

위의 두 가지는 완전히 **독립적**이다. 이러한 특성 때문에 생기는 여러가지 현상이 존재한다.

### 1. 타입 오류가 있는 코드도 컴파일이 가능하다.

오류와 비슷하다. 문제 될 부분을 알려주지만, 빌드를 멈추지는 않는다.

```json
{
  "compilerOptions": {
    "noEmitOnError": true
  }
}

// 오류가 있을 때 컴파일 되는 것을 막아준다.
```

### 2. 런타임에는 타입 체크가 불가능하다.

타입은 런타임 시점에 아무런 역할을 할 수 없다.
<br>
컴파일 되는 과정에서 인터페이스, 타입, 타입 구문은 제거해버린다.

```typescript
interface Square {
  width: number;
}

interface Rectangle extends Square {
  height: number;
}

type Shape = Square | Rectangle;

function calculateArea(shape: Shape) {
  if (shape instanceof Rectangle) {
    // Rectangle은 형식만 참조하지만, 여기서는 값으로 사용되고 있습니다.
    return shape.width * shape.height;
  } else {
    return shape.width * shape.width;
  }
}
```

**런타임에 타입을 유지**해주는 방안이 필요하다.
<br>

방안1. 속성이 존재하는지 체크하기

```typescript
function calculateArea(shape: Shape) {
  if ("height" in shape) {
    return shape.width * shape.height;
  } else {
    return shape.width * shape.width;
  }
}
```

방안2. 런타임에 접근 가능한 타입 정보를 명시적으로 저장하는 태그 기법

```typescript
interface Square {
  kind: "square";
  width: number;
}

interface Rectangle {
  kind: "rectangle";
  height: number;
  width: number;
}

type Shape = Square | Rectangle;

function calculateArea(shape: Shape) {
  if (shape.kind === "rectangle") {
    return shape.width * shape.height;
  } else {
    return shape.width * shape.width;
  }
}
```

방안3. 클래스를 생성하여 타입과 값 모두 사용하기

```typescript
class Square {
  constructor(public width: number) {}
}

class Rectangle extends Square {
  constructor(public width: number, public height: number) {
    super(width);
  }
}

type Shape = Square | Rectangle;

function calculateArea(shape: Shape) {
  if (shape instanceof Rectangle) {
    return shape.width * shape.height;
  } else {
    return shape.width * shape.width;
  }
}
```

### 3. 타입 연산은 런타임에 영향을 주지 않는다.

아래의 예시는 타입 체커를 통과하지만 잘못됐다.

```typescript
function asNumber(val: number | string): number {
  // as : 타입 연산 (타입 단언문)
  return val as number;
}

// 컴파일러가 자바스크립트로 변환한 코드는 다음과 같다.
function asNumber(val) {
  return val;
}

// 런타임에 타입 연산을 하는 방법
function asNumber(val: number | string): number {
  return typeof val === "string" ? Number(val) : val;
}
```

### 4. 런타입 타입은 선언된 타입과 다를 수 있다.

### 5. 타입스크립트 타입으로는 함수를 오버로드할 수 없다.

### 6. 타입스크립트 타입은 런타임 성능에 영향을 주지 않는다.

타입과 타입 연산자는 자바스크립트 변환 시점에 제거되기 때문이다.
