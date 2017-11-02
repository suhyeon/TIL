# ECMA6 - ENHANCED OBJECT PROPERTY
객체 리터럴 프로퍼티 기능확장

## 1. 프로퍼티 축약 표현
```javascript
// ES5
var x = 1, y = 2;

var obj = {
  x: x,
  y: y
};

console.log(obj); // { x: 1, y: 2 }

// ES6
let x = 1, y = 2;

const obj = { x, y };

console.log(obj); // { x: 1, y: 2 }
```
> ES6에서는 프로퍼티 값으로 변수를 사용하는 경우, 프로퍼티이름을 생략할 수 있다.
`이때 프로퍼티 이름은 변수의 이름으로 자동 생성된다.`
## 2. 프로퍼티 이름조합
ES6에서는 객체 리터럴 내에서 프로퍼티 이름을 동적으로 생성할 수 있다.
```javascript
// ES5
var i = 0;
var propNamePrefix = 'prop_';

var obj = {};

obj[propNamePrefix + ++i] = i;
obj[propNamePrefix + ++i] = i;
obj[propNamePrefix + ++i] = i;

console.log(obj); // { prop_1: 1, prop_2: 2, prop_3: 3 }

// ES6
let i = 0;
const propNamePrefix = 'prop_';

const obj = {
  [propNamePrefix + ++i]: i,
  [propNamePrefix + ++i]: i,
  [propNamePrefix + ++i]: i
};

console.log(obj); // { prop_1: 1, prop_2: 2, prop_3: 3 }
```
## 3. 메소드 축약 표현
ES6에서는 메소드를 선언에 FUNCTION키워드를 생략 가능하다.
```javascript
// ES5
var obj = {
  name: 'Lee',
  sayHi: function() {
    console.log('Hi! ' + this.name);
  }
};

obj.sayHi(); // Hi! Lee

// ES6
const obj = {
  name: 'Lee',
  // 메소드 축약 표현
  sayHi() {
    console.log('Hi! ' + this.name);
  }
};

obj.sayHi(); // Hi! Lee
```
## 4. __proto__프로퍼티에 의한 상속
ES6에서는 객체 리터럴 내부에서 __proto__프로퍼티를 직접 설정할 수 있다.
```javascript
// ES5
var parent = {
  name: 'parent',
  sayHi() {
    console.log('Hi! ' + this.name);
  }
};

// 프로토타입 패턴 상속
var child = Object.create(parent);
child.name = 'child';

parent.sayHi(); // Hi! parent
child.sayHi();  // Hi! child

// ES6
const parent = {
  name: 'parent',
  sayHi() {
    console.log('Hi! ' + this.name);
  }
};

const child = {
  // child 객체의 프로토타입 객체에 parent 객체를 바인딩하여 상속을 구현한다.
  __proto__: parent,
  name: 'child'
};

parent.sayHi(); // Hi! parent
child.sayHi();  // Hi! child
```
> 객체 리터럴에 의해 생성된 객체의 __proto__프로퍼티에 다른 객체를 직접 바인딩해 상속을 표현할 수 있음을 의미한다.