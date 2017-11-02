# ECMA6 - ARROW FUNCTION
## 1. SYNTAX
ARROW FUNCTION(화살표 함수)는 FUNCTION 키워드 대신 화살표(=>)를 사용하여 간략한 방법으로 함수를 선언할 수 있다.
> 모든 경우 사용할 수 있는 것은 아니다.
```javascript
// 매개변수 지정 방법
    () => { ... } // 매개변수가 없을 경우
     x => { ... } // 매개변수가 한개인 경우, 소괄호를 생략할 수 있다.
(x, y) => { ... } // 매개변수가 여러개인 경우

// 함수 몸체 지정 방법
x => { return x * x }  // single line block
x => x * x             // 함수 몸체가 한줄의 표현식이라면 중괄호를 생략할 수 있으며 자동으로 return된다. 위 표현과 동일하다.

() => { return { a: 1 }; }
() => ({ a: 1 })  // 위 표현과 동일하다. 객체 반환시 소괄호를 사용한다.

() => {           // multi line block.
  const x = 10;
  return x * x;
};
```

## 2. ARROW FUNCTION 의 호출
ARROW FUNCTION은 익명함수로만 사용할 수 있다.
> ARROW 함수를 호출하기 위해선 함수표현식을 사용한다.
```javascript
// ES5
var pow = function (x) { return x * x; };
console.log(pow(10)); // 100

// ES6
const pow = x => x * x;
console.log(pow(10)); // 100
```
>또는 콜백함수로 사용할 수 있다. 이경우 일반적인 함수 표현식보다 표현이 간결하다.
```javascript
// ES5
var arr = [1, 2, 3];
var pow = arr.map(function (x) { // x는 요소값
  return x * x;
});

console.log(pow); // [ 1, 4, 9 ]

// ES6
const arr = [1, 2, 3];
const pow = arr.map(x => x * x);

console.log(pow); // [ 1, 4, 9 ]
```

## 3. Arguments와 rest 파라미터
arguments 객체는 함수 호출시 전달된 arguments의 정보를 담고있는 순회가능한 유사배열 객체이다.
> 함수 객체의 arguments 프로퍼티는 arguments객체를 값으로 가지며 함수 내부에서 지역변수처럼 사용된다.
```javascript
// ES5
var foo = function () {
  console.log(arguments);
};

foo(1, 2); // { '0': 1, '1': 2 }
```
> arguments객체는 유사배열이기 때문에 배열메소드를 사용하려면 function.prototpye.call, function.prototype.apply를 사용하여야 하는 번거러움이 있다.
```javascript
/ ES5
function sum() {
  // 가변 인자 함수의 경우, 파라미터를 통해 인수를 전달받는 것이 불가능하므로 arguments 객체를 활용하여 인수를 전달받는다. 
  // arguments 객체를 배열로 변환
  var array = Array.prototype.slice.call(arguments);
  return array.reduce(function (pre, cur) {
    return pre + cur;
  });
}

console.log(sum(1, 2, 3, 4, 5)); // 15

var es5 = function () {};
console.log(es5.hasOwnProperty('arguments')); // true

const es6 = () => {};
console.log(es6.hasOwnProperty('arguments')); // false

// ES6
const sum = (...args) => {
  // console.log(arguments); // Uncaught ReferenceError: arguments is not defined
  console.log(Array.isArray(args)); // true

  return args.reduce((pre, cur) => pre + cur);
};

console.log(sum(1, 2, 3, 4, 5)); // 15
```

## 4. this
fucntion키워드를 사용해 생선한 일반 함수와 arrow function와의 가장큰 차이점은 this이다.

### 1. 일반함수의 this
일반 함수의 경우, 해당함수 호출 패턴에 따라 this에 바인딩 되는 객체가 달라진다.
> 콜백함수 내부의 this는 전역 객체 window를 가리킨다.

```javascript
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  // (A)
  return arr.map(function (x) {
    return this.prefix + ' ' + x; // (B)
  });
};

var pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));
```
- A에서의 THIS 는 생성자 함수 PREFIXER가 생성한 객체, 즉 생성자 함수의 인스턴스이다.
  - 생성자함수 : 가장먼저, 빈객체를 만든다.
  - 빈객체에대해서 property를 set해준다.
  - 선두에서 만든 빈객체에 set된 객체를 리턴한다.
  - 단, new와 함께 사용됬을 경우이다.
- B에서의 THIS는 아마도 생성자 함수 PREFIXER가 생성한 객체일 것으로 기대하였겠지만 이곳에서 TIHS는 전역객체 WINDOW를 가리킨다.
- 이는 생성자함수와 객체의 메소드를 제외한 모든함수의 내부의 THIS는 전역객체를 가리키기 때문이다.

> 콜백함수 내부의 THIS가 메소드를 호출한 객체를 가리키게 하기 위한 해결법
- 1.
```javascript
// Solution 1: that = this
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  var that = this;  // this: Prefixer 생성자 함수의 인스턴스
  return arr.map(function (x) {
    return that.prefix + ' ' + x;
  });
};

var pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));
```
- 2.
```javascript
// Solution 2: map(func, this)
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  return arr.map(function (x) {
    return this.prefix + ' ' + x;
  }, this); // this: Prefixer 생성자 함수의 인스턴스
};

var pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));
```
- 3.
```javascript
// Solution 3: bind(this)
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  return arr.map(function (x) {
    return this.prefix + ' ' + x;;
  }.bind(this)); // this: Prefixer 생성자 함수의 인스턴스
};

var pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));
```

### 2. ARROW FUNCTION의 THIS
ARROW 함수는 언제나 자신을 포함하는 외부 SCOPE에서 THIS를 계승받는다.
> ARROW 함수는 자신만의 THIS를 생성하지 않고 자신을 포함하고 있는 컨텍스트로부터 THIS를 계승받는다. `이를 LEXICAL THIS라 한다.`
```javascript
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  return arr.map(x => `${this.prefix}  ${x}`);
};

const pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));
```

## 5. ARROW 함수를 사용해서는 안되는 경우
LEXICAL THIS를 지원하므로 콜백함수에 사용하기 편리하다.
> ARROW FUNCTION을 사용하는 것이 오히려 혼란을 불러오는 경우도 있기 때문에 주의하여야 한다.

### 1. 메소드
메소드 정의시 ARROW 함수를 사용하는 것은 피해야 한다. 
```javascript
// Bad
const obj = {
  name: 'Lee',
  sayHi: () => console.log(`Hi ${this.name}`)
};

obj.sayHi(); // Hi undefined
```
수정하기
```javascript
// Good
const obj = {
  name: 'Lee',
  sayHi() { // === sayHi: function() {
    console.log(`Hi ${this.name}`);
  }
};

obj.sayHi(); // Hi Lee
```
### 2. prototype
메소드로 사용했을 때와 동일한 문제가 발생한다. 
```javascript
// Bad
const obj = {
  name: 'Lee',
};

Object.prototype.sayHi = () => console.log(`Hi ${this.name}`);

obj.sayHi(); // Hi undefined
```
같은 문제 발생 (수정하기)
```javascript
// Good
const obj = {
  name: 'Lee',
};

Object.prototype.sayHi = function() {
  console.log(`Hi ${this.name}`);
};

obj.sayHi(); // Hi Lee
```

### 3. 생성자 함수
생성자 함수로 사용할 수 없다.
> prototype 프로퍼티를 가지며 prototype 프로퍼티가 가리키는 프로토타입 객체의 constructor를 사용하지만 arrow함수는 prototype프로퍼티를 가지고 있지 않다.
```javascript
const Foo = () => {};
// Arrow Function은 prototype 프로퍼티가 없다
console.log(Foo.hasOwnProperty('prototype')); // false
const foo = new Foo(); // TypeError: Foo is not a constructor
```