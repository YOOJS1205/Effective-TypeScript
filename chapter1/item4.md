# 구조적 타이핑에 익숙해지기

자바스크립트는 기본적으로 덕 타이핑 기반이다. -> 특정 함수에 매개변수 값이 모두 제대로 주어지면, 값의 타입을 신경쓰지 않고 사용한다.

```typescript
interface Vector2D {
  x: number;
  y: number;
}

function calculateLength(v: Vector2D) {
  return Math.sqrt(v.x * v.x + v.y * v.y);
}
```

이름이 들어간 벡터를 추가해보자.

```typescript
interface NamedVector {
  name: string;
  x: number;
  y: number;
}

const v: NamedVector = { x: 3, y: 4, name: "Zee" };
calculateLength(v); // 5
```

NamedVector와 Vector2D가 호환이 가능하기 때문에 calculateLength 함수를 사용할 수 있다. -> 구조적 타이핑
<br><br>

구조적 타이핑 때문에 발생하는 문제

```typescript
interface Vector3D {
    x: number;
    y: number;
    z: number;
}

// 정규화 함수
function normalize(v: Vector3D) {
    const length = calculateLength(v);

    return {
        x: v.x / length;
        y: v.y / length;
        z: v.z / length;
    }
}

// 3차원 벡터이기 때문에 2차원 벡터와 호환이 되면 안되는데, x, y 프로퍼티가 호환이 되어서 문제가 생김
// 구조적으로 호환이 되어서 발생하는 문제
```
