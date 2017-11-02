# ECMA SCRIPT 6 - LET, CONST 
- FUNCTION LEVEL SCOPE
  - 전역 변수의 남발
  - FOR LOOP 초기화식에서 사용한 변수를 FOR LOOP 외부 또는 전역에서 참조
- VAR 키워드 생략 허용
  - 의도하지 않은 변수의 전역화
- 중복 선언 허용
  - 의도하지 않은 변수값 변경
- 변수 호이스팅
  - 변수를 선언하기 전에 참조가 가능

> ECMA6는 이러한 단점을 보완하기 위해 LET과 CONST키워드를 도입했다.
## 1. LET
### 1. BLOCK LEVEL SCOPE
- FUNCTION LEVEL SCOPE
  - 함수내에서 선언된 변수는 함수내에서만 유효하며 함수 외부에서는 참조할 수 없다. 
  - 즉 함수내부에서 선언한 변수는 지역변수이며 함수 외부에서 선언한 변수는 모두 전역 변수이다.
- BLOCK LEVEL SCOPE
  - 코드 블럭내에서 선언된 변수는 코드 블럭내에서만 유효하며 코드 블럭외부에서는 참조할 수 없다.

```javascript
console.log(foo); // undefined
var foo = 123;
console.log(foo); // 123
{
  var foo = 456;
}
console.log(foo); // 456
```
> ES6는 BLOCK LEVEL SCOPE를 갖는 변수를 선언하기 위해 LET키워드를 제공한다.
```javascript
let foo = 123;
{
  let foo = 456;
  let bar = 456;
}
console.log(foo); // 123
console.log(bar); // ReferenceError: bar is not defined
```

### 2. 중복 선언 금지
VAR는 중복 선언이 가능하였지만 LET은 중복선언시 SYNTAX ERROR가 발생한다.

```javascript
var foo = 123;
var foo = 456;  // OK

let bar = 123;
let bar = 456;  // Uncaught SyntaxError: Identifier 'bar' has already been declared
```

### 3. 호이스팅
ES6에서 도입된 LET, CONST를 포함한 모든선언을 호이스팅한다.
> 모든 선언 : VAR, LET, CONST, FUNCTION, FUNCTION*, CLASS

`호이스팅이란 VAR 선언문이나 FUNCTION선언문등을 해당 스코프의 선두로 옮기는 것을 말한다.`

- LET 키워드로 선언된 변수는 스코프의 시작에서 변수의 선언까지 `일시적 사각지대(TDZ: TEMPORAL DEAD ZONE)`에 빠지기 때문이다.

```javascript
console.log(foo); // undefined
var foo;

console.log(bar); // Error: Uncaught ReferenceError: bar is not defined
let bar;
```

- 변수는 3단계에 걸쳐 생성된다.
  - 선언단계
    - 변수객체에 변수를 등록한다.
    - 이 변수 객체는 스코프가 참조하는 대상이 된다.
  - 초기화 단계
    - 변수객체에 등록된 변수를 메모리에 할당한다.
    - 이 단계에서는 변수는 undefined로 초기화된다.
  - 할당 단계
    - undefined로 초기화된 변수에 실제값을 할당한다.

> var 키워드로 선언된 변수는 선언단계와 초기화 단계가 한번에 이루어진다.

`즉, 스코프에 변수가 등록된고 변수는 undefined로 초기화된다.`
> let 키워드로 선언된 변수는 선언단계와 초기화 단계가 분리되어 진행된다.

### 4. 클로저
BLOCK LEVEL SCOPE를 지원하는 LET은 VAR보다 직관적이다
```javascript
var funcs = [];

// 함수의 배열을 생성한다
// i는 전역 변수이다
for (var i = 0; i < 3; i++) {
  funcs.push(function () { console.log(i); });
}

// 배열에서 함수를 꺼내어 호출한다
for (var j = 0; j < 3; j++) {
  funcs[j]();
}
```
> 위 코드의 실행 결과로 0,1,2,를 기대할 수 있지만 결과는 3이 3번 출력된다.
```javascript
var funcs = [];

// 함수의 배열을 생성한다
// i는 전역 변수이다
for (var i = 0; i < 3; i++) {
  (function (index) { // index는 자유변수이다.
    funcs.push(function () { console.log(index); });
  }(i));
}

// 배열에서 함수를 꺼내어 호출한다
for (var j = 0; j < 3; j++) {
  funcs[j]();
}
```
`클로저를 활용한 방법이다.`
```javascript
var funcs = [];

// 함수의 배열을 생성한다
// i는 for loop에서만 유효한 지역변수이면서 자유변수이다
for (let i = 0; i < 3; i++) {
  funcs.push(function () { console.log(i); });
}

// 배열에서 함수를 꺼내어 호출한다
for (var j = 0; j < 3; j++) {
  funcs[j]();
}
```
### 5. 전역 객체와 let
전역객체는 모든 객체의 유일한 최상위 객체를 의미하며 일반적으로 browser-side에서는 window객체, server-side에서는 global 객체를 의미한다.
```javascript
var foo = 123; // 전역변수

console.log(window.foo); // 123

let foo = 123; // 전역변수

console.log(window.foo); // undefined
```
## 2. CONST
CONST는 상수를 위해 사용한다. 하지만 반드시 상수만을 위해 사용하지는 않는다.
> CONST는 LET과 대부분 동일한 특징을 갖는다.

### 1. 선언과 초기화
LET은 초기화 이후 다른 값으로 재할당이 자유로우나 CONST는 초기화 이후 재할당이 금지된다.
```javascript
const FOO = 123;
FOO = 456; // TypeError: Assignment to constant variable.
//주의할 것은 const는 반드시 선언과 동시에 초기화가 이루어져야한다.
const FOO; // SyntaxError: Missing initializer in const declaration
{
  const FOO = 10;
  console.log(FOO); //10
}
console.log(FOO); // ReferenceError: FOO is not defined
//const는 let과 마찬가지로 block leve scope를 갖는다.
```

### 2. 상수
상수는 가독성의 향상과 유지보수의 편의를 위해 적극적으로 사용해야 한다.

```javascript
// Low readability
if (x > 10) {
}

// Better!
const MAXROWS = 10;
if (x > MAXROWS) {
}

const obj = { foo: 123 };
obj = { bar: 456 }; // TypeError: Assignment to constant variable.
```
> const는 객체에도 사용할 수 있지만 재할당은 금지된다.

### 3. const와 객체
const는 재할당이 금지된다. 
> 이는 const 변수의 값이 객체인 경우, 객체에 대한 참조의 변경을 금지한다는 것을 의미한다.  
`객체의 프로퍼티는 보호되지 않는다.`

```javascript
const user = {
  name: 'Lee',
  address: {
    city: 'Seoul'
  }
};

// const 변수는 재할당이 금지된다.
// user = {}; // TypeError: Assignment to constant variable.

// 프로퍼티 값의 재할당은 허용된다!
user.name = 'Kim';

console.log(user); // { name: 'Kim', address: { city: 'Seoul' } }
```
- 객체타입 변수 선언에는 const를 사용하는 것이 좋다.
  - 객체에 대한 참조는 변경될 필요가 없다.
  - 재할당이 필요 없다.
  - 만일 새로운 객체에 대한 참조를 변수에 할당해야 한다면 새로운 변수를 사용하면 된다.
- const를 사용한다 하더라도 객체의 프로퍼티를 변경할 수 있다.
- 자바스크립트의 값은 대부분 객체이므로 결국 대부분의 경우 const를 사용하게 된다.
> primitive 형 변수를 제외한 모든 값은 객체이다.

## 3. VAR VS. LET VS. CONST
- ES6를 같이 사용한다면 VAR 키워드는 사용하지 않는다.
- 변경이 발생하지 않는(재할당이 필요없는)PRIMITIVE형 변수와 객체형 변수에는 CONST를 사용한다.
- 재할당이 필요한 PRIMITIVE형 변수에는 LET을 사용한다.