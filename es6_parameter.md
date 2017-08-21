# ECMA6 - EXTENDED PARAMETER HANDLING
## 1. 기본 파라미터 초기값(DEFAULT PARAMETER VALUE)
파라미터에 초기값을 설정하여 함수내에서 수행하던 파라미터 체크 및 초기화를 간편화할 수 있다.
```javascript
// ES5
function plus(x, y) {
  x = x || 0;
  y = y || 0;
  return x + y;
}

console.log(plus());     // 0
console.log(plus(1, 2)); // 3

// ES6
function plus(x = 0, y = 0) {
  // x, y에 인수가 할당되지 않으면 초기값 0이 할당된다.
  return x + y;
}

console.log(plus());     // 0
console.log(plus(1, 2)); // 3
```

## 2. REST 파라미터
### 1. SYNTAX
REST 파라미터는 SPREAD연산자(...)를 사용해 파라미터를 작성한 형태를 말한다.
> REST파라미터를 사용하면 인수를 함수내부에서 배열로 전달받을 수 있다.

```javascript
function foo( ...rest) {
  console.log(Array.isArray(rest)); // true
  console.log(rest); // [ 1, 2, 3, 4, 5 ]
}

foo(1, 2, 3, 4, 5);

// 인수는 순차적으로 파라미터와 rest파라미터에 할당된다.
function foo(param, ...rest) {
  console.log(param); // 1
  console.log(rest);  // [ 2, 3, 4, 5 ]
}

foo(1, 2, 3, 4, 5);

function bar(param1, param2, ...rest) {
  console.log(param1); // 1
  console.log(param2); // 2
  console.log(rest);   // [ 3, 4, 5 ]
}

bar(1, 2, 3, 4, 5);

//rest파라미터는 반드시 마지막 파라미터이어야 한다.
function foo( ...rest, param1, param2) { }

foo(1, 2, 3, 4, 5);
// SyntaxError: Rest parameter must be last formal parameter
```
>가변인자 함수를 대응하기위해 
### 2. arguments와 rest 파라미터
- ES6이전
  - 인자의 갯수를 사전에 알 수없는 가변인자 함수의 경우
    - ARGUMENTS객체를 통해 인자값을 확인한다.
    - ARGUMENTS객체는 함수 호출시 전달된 인수들의 정보를 담고 있는 순회가능한 유사배열 객체이다.
    - 함수 객체의 ARGUMENTS 프로퍼티는 ARGUMENTS객체를 값으로 가지며 함수 내부에서 지역변수 처럼 사용된다.

```javascript
// ES5
var foo = function () {
  console.log(arguments);
};

foo(1, 2); // { '0': 1, '1': 2 }

// ES5
function sum() {
  // 가변 인자 함수의 경우, 파라미터를 통해 인수를 전달받는 것이 불가능하므로 arguments 객체를 활용하여 인수를 전달받는다. 
  // arguments 객체를 배열로 변환
  var array = Array.prototype.slice.call(arguments);
  return array.reduce(function (pre, cur) {
    return pre + cur;
  });
}

console.log(sum(1, 2, 3, 4, 5)); // 15
```
- ES6이후
  - REST 파라미터를 사용해 가변인자를 함수내부에 배열로 전달할 수 있다.

```javascript
// ES6
function sum(...args) {
  console.log(arguments); // (5) [1, 2, 3, 4, 5, callee: (...), Symbol(Symbol.iterator): function]
  console.log(Array.isArray(args)); // true
  return args.reduce((pre, cur) => pre + cur);
}
console.log(sum(1, 2, 3, 4, 5)); // 15

// ES6
const sum = (...args) => {
  // console.log(arguments); // Uncaught ReferenceError: arguments is not defined
  console.log(Array.isArray(args)); // true

  return args.reduce((pre, cur) => pre + cur);
};

console.log(sum(1, 2, 3, 4, 5)); // 15
```

## 3. SPREAD 연산자
연산자의 대상 배열을 개별요소로 분리한다.
```javascript
// ...[1, 2, 3]는 [1, 2, 3]을 개별 요소로 분리한다(-> 1, 2, 3)
...[1, 2, 3] // -> 1, 2, 3
```

### 1. 함수의 인수로 사용하는 경우
배열을 함수의 인수로 사용하고, 배열의 각 요소를 개별적인 파라미터로 전달하고 싶은 경우, `function.prototype.apply를 사용하는 것이 일반적이다.`
```javascript
// ES5
function foo(x, y, z) {
  console.log(x); // 1
  console.log(y); // 2
  console.log(z); // 3
}

// 배열을 foo 함수의 인자로 전달하려고 한다.
const arr = [1, 2, 3];

// apply 함수의 2번째 인자(배열)는 호출하려는 함수(foo)의 개별 인자로 전달된다.
foo.apply(null, arr);
// foo.call(null, 1, 2, 3);

// ES6
function foo(x, y, z) {
  console.log(x); // 1
  console.log(y); // 2
  console.log(z); // 3
}

// 배열을 foo 함수의 인자로 전달하려고 한다.
const arr = [1, 2, 3];

// ...[1, 2, 3]는 [1, 2, 3]을 개별 요소로 분리한다(-> 1, 2, 3)
// spread 연산자에 의해 분리된 배열의 요소는 개별적인 인자로서 각각의 매개변수에 전달된다.
foo(...arr);

// Spread 연산자를 사용한 매개변수 정의 (= Rest 파라미터)
// ...rest는 분리된 요소들을 함수 내부에서 배열로 변환한다
function foo(param, ...rest) { 
  console.log(param); // 1
  console.log(rest);  // [ 2, 3 ]
}
foo(1, 2, 3);

// Spread 연산자를 사용한 인수
// 배열 인수는 분리되어 순차적으로 매개변수에 할당
function bar(x, y, z) {
  console.log(x); // 1
  console.log(y); // 2
  console.log(z); // 3
}

// ...[1, 2, 3]는 [1, 2, 3]을 개별 요소로 분리한다(-> 1, 2, 3)
// spread 연산자에 의해 분리된 배열의 요소는 개별적인 인자로서 각각의 매개변수에 전달된다.
bar(...[1, 2, 3]);
```
>REST 파라미터는 반드시 마지막 파라미터이어야 하지만 SPREAD 연산자를 사용한 인수는 자유롭게 사용할 수 있다.

```javascript
// ES6
function foo(v, w, x, y, z) {
  console.log(v); // 1
  console.log(w); // 2
  console.log(x); // 3
  console.log(y); // 4
  console.log(z); // 5
}

// ...[2, 3]는 [2, 3]을 개별 요소로 분리한다(-> 2, 3)
// spread 연산자에 의해 분리된 배열의 요소는 개별적인 인자로서 각각의 매개변수에 전달된다.
foo(1, ...[2, 3], 4, ...[5]);
```

### 2. 배열에서 사용하는 경우
spread 연산자를 배열에서 사용하는 경우, 보다 간결하고 가독성이 향상된 표현이 가능하다.
#### 1. concat
기존 배열요소를 새로운 배열요소의 일부로 만들고 싶은 경우, 배열 리터럴 구문만으로 해결할 수 없고 concat 메소드를 사용해야 한다.
```javascript
// ES5
var arr = [1, 2, 3];
console.log(arr.concat([4, 5, 6])); // [ 1, 2, 3, 4, 5, 6 ]

//spread 연산자를 배열에서 사용하는 경우, 배열 리터럴 구문만으로 기존 배열의 요소를 새로운 배열 요소의 일부로 만들 수 있다.
// ES6
const arr = [1, 2, 3];
// ...arr은 [1, 2, 3]을 개별 요소로 분리한다
console.log([...arr, 4, 5, 6]); // [ 1, 2, 3, 4, 5, 6 ]
```
#### 2. push
```javascript
// ES5
var arr1 = [1, 2, 3];
var arr2 = [4, 5, 6];

// apply 메소드의 2번째 인자는 배열. 이것은 개별 인자로 push 메소드에 전달된다.
// 1번째 인자는 this로 사용될 인자
// push : 리스트로 들어온다.
Array.prototype.push.apply(arr1, arr2);

console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]

// ES6
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

// ...arr2는 [4, 5, 6]을 개별 요소로 분리한다
arr1.push(...arr2); // == arr1.push(4, 5, 6);

console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]
```

#### 3. splice
```javascript
// ES5
var arr1 = [1, 2, 3, 6];
var arr2 = [4, 5];

// apply 메소드의 2번째 인자는 배열. 이것은 개별 인자로 push 메소드에 전달된다.
// [3, 0].concat(arr2) => [3, 0, 4, 5]
// arr1.splice(3, 0, 4, 5) => arr1[3]부터 0개의 요소를 제거하고 그자리(arr1[3])에 새로운 요소(4, 5)를 추가한다.
Array.prototype.splice.apply(arr1, [3, 0].concat(arr2));

console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]

// ES6
const arr1 = [1, 2, 3, 6];
const arr2 = [4, 5];

// ...arr2는 [4, 5]을 개별 요소로 분리한다
arr1.splice(3, 0, ...arr2); // == arr1.splice(3, 0, 4, 5);

console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]
```

#### 4. copy
```javascript
// ES5
var arr  = [1, 2, 3];
var copy = arr.slice();

console.log(copy); // [ 1, 2, 3 ]
// copy를 변경한다.
copy.push(4);
console.log(copy); // [ 1, 2, 3, 4 ]
// arr은 변경되지 않는다.
console.log(arr);  // [ 1, 2, 3 ]

// ES6
const arr  = [1, 2, 3];
// ...arr은 [1, 2, 3]을 개별 요소로 분리한다
const copy = [...arr];

console.log(copy); // [ 1, 2, 3 ]
// copy를 변경한다.
copy.push(4);
console.log(copy); // [ 1, 2, 3, 4 ]
// arr은 변경되지 않는다.
console.log(arr);  // [ 1, 2, 3 ]
```