# JAVASCRIPT - MATH
MATH 객체 : 수학 상수와 함수를 위한 프로퍼티와 메소드를 제공하는 BUILT-IN 객체

> 생성자 없으며 모든 프로퍼티와 메소드는 MATH객체와 별도 생성없이 프로퍼티와 메소드를 사용할 수 있다.

## 1. Math property
정적 프로퍼티로 Math객체를 생성할 필요없이 Math.propertyName의 형태로 사용한다.

### 1. Math.PI
PI값을 반환한다.

>Math.PI; // 3.141592653589793

## 2. Math Method

### 1. Math.abs()
절대값을 반환한다.

### 2. Math.round()
숫자를 가장 인접한 정수로 올림/내림한다.
```javascript
var x;

// Returns the value 20
x = Math.round(20.49);

// Returns the value 21
x = Math.round(20.5);

// Returns the value -20
x = Math.round(-20.5);

// Returns the value -21
x = Math.round(-20.51);
```
### 3. Math.sqrt()
양의 제곱근을 반환한다.

### 4. Math.ceil()
지정된 숫자를 자신보다 큰, 가장 가까운 정수로 올림한다.
```javascript
Math.ceil(1.4); // 2
```

### 5. Math.floor()
지정된 숫자를 자신보다 작은, 가장 가까운 정수로 내림한다.
```javascript
Math.floor(1.6); // 1
```

### 6. Math.random()
0과 1 사이의 임의의 숫자를 반환한다.
> 이때 0은 포함되지만 1은 포함되지 않는다.

### 7. Math.pow()
첫번재 인수를 밑(base), 두번재 인수를 지수(exponent)로 하여 거듭제곱을 반환한다.

### 8. Math.max()
숫자 중 가장 최대수를 반환한다.
>배열에서 선택을 많이한다.

### 9. Math.min()
숫자 중 가장 최소수를 반환한다.
> 배열에서 선택을 많이한다.
