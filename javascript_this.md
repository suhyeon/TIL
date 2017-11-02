# JAVASCRIPT - THIS
THIS
- 특별한 상황 2가지를 제외한 경우는 모두 전역객체를 의미한다.(메소드호출패턴, 생성자 함수 호출패턴)

> 자바스크립트의 함수는 호출될 때, 매개변수로 전달되는 인자값 이외에 arguments 객체와 this를 암묵적으로 전달받는다.
arguments 객체 : 인자값의 리스트

java에서의 this 
  - 인스턴스 자신을 가리키는 참조변수
javascript 에서의 this
  - 함수가 어떻게 호출되는지에 따라 this에 바인딩되는 객체가 달라진다.

> 함수호출 팬턴과 this 바인딩
- 1. 메소드 호출 패턴
- 2. 함수호출 패턴
- 3. 생성자 호출 패턴
- 4. apply 호출 패턴

## 1. 메소드 호출패턴
함수가 객체의 프로퍼티이면 메소드 호출패턴으로 호출된다.

> 이때의 this는 해당 메소드를 소유한 객체, 즉 해당 메소드를 호출한 객체에 바인딩 된다.

`쉽게말해, 그 메소드를 호출한 객체를 가리킨다.`

## 2. 함수 호출 패턴
전역객체는 모든 객체의 유일한 최상위 객체를 의미하며
클라이언트 사이드 : window 서버사이드 : global 객체를 의미한다.

> 메소드의 내부함수일 경우에도 this는 전역객체에 바인딩 된다.(콜백함수도 마찬가지)

```javascript
var value = 1;

var obj = {
  value: 100,
  foo: function() {
    setTimeout(function() {  //callback fuction
      console.log("callback's this: ",  this);  // window
      console.log("callback's this.value: ",  this.value); // 1
    }, 100);
  }
};

obj.foo();
```

`더글라스 크락포드의 내부함수의 this가 전역객체를 참조하는것을 회피하는 방법`
```javascript
var value = 1;

var obj = {
  value: 100,
  foo: function() {
    var that = this;  // Workaround : this === obj

    console.log("foo's this: ",  this);  // obj
    console.log("foo's this.value: ",  this.value); // 100
    function bar() {
      console.log("bar's this: ",  this); // window
      console.log("bar's this.value: ", this.value); // 1

      console.log("bar's that: ",  that); // obj
      console.log("bar's that.value: ", that.value); // 100
    }
    bar();
  }
};

obj.foo();
```

## 3. 생성자 호출 패턴
생성자 함수가 생성할 객체를 가리킨다.

### 1. 생성자 함수 동작방식

new 연산자와 함게 생성자 함수를 호출하면 다음과 같은 수순을 동작
- 1. 빈객체 생성 및 this 바인딩
- 2. this 를통한 프로퍼티 생성
- 3. 생성된 객체 반환


### 3. 생성자 함수에 new 연산자를 붙이지 않고 호출할 경우

```javascript
var Person = function(name) {
  // 전역객체에 name 프로퍼티를 추가
  this.name = name;
};

// 일반 함수로서 호출되었기 때문에 객체를 생성하여 반환하지 않는다.
// 일반 함수의 this는 전역객체를 가리킨다.
var me = Person('Lee');

console.log(me); // undefined
console.log(window.name); // Lee
```

방어코드를 만들어야한다.  
그중에 제일 대표적인 방법 코드
```javascript
// Scope-Safe Constructor Pattern
function A(arg) {
  // 생성자 함수가 new 연산자와 함께 호출되면 함수의 선두에서 빈객체를 생성하고 this에 바인딩한다.

  /*
  this가 호출된 함수(arguments.callee, 본 예제의 경우 A)의 인스턴스가 아니면 new 연산자를 사용하지 않은 것이므로 이 경우 new와 함께 생성자 함수를 호출하여 인스턴스를 반환한다.
  arguments.callee는 호출된 함수의 이름을 나타낸다. 이 예제의 경우 A로 표기하여도 문제없이 동작하지만 특정함수의 이름과 의존성을 없애기 위해서 arguments.callee를 사용하는 것이 좋다.
  */
  if (!(this instanceof arguments.callee)) {
    return new arguments.callee(arg);
  }

  this.value = arg ? arg : 0;
}

var a = new A(100);
var b = A(10);

console.log(a.value);
console.log(b.value);

```

### 4. apply 호출 패턴
객체는 기본적으로 순회가 안된다.  
`즉, 순서가 보장이 되지 않는다.`  
하지만 배열은 순서가 index로 관리가 될 수 있다.  

>유사배열은 객체이지만 배열처럼 순서를 매길 수 있다. ex) DOM, arguments객체)

내부적인 바인딩 이외에 this를 특정객체에 명시적 바인딩 방법을 제공하는 것 : Function.prototype.apply(), Function.prototype.call()메소드

> []의 의미는 옵션
```javascript
func.apply(thisArg, [argsArray])

// thisArg: 함수 내부의 this에 바인딩할 객체
// argsArray: 함수에 전달할 인자 배열
```

`call : 쉼표로 인자를 보내고, apply : 배열리스트로 보낸다.`
```javascript
Person.apply(foo, [1, 2, 3]);

Person.call(foo, 1, 2, 3);
```

```javascript
function convertArgsToArray() {
  console.log(arguments);

  // arguments 객체를 배열로 변환
  // slice: 배열의 특정 부분에 대한 복사본을 생성한다.
  var arr = Array.prototype.slice.apply(arguments); // arguments.slice
  // var arr = [].slice.apply(arguments);
  //위의 커멘츠는 빈배열이지만 프로토타입을 찾아가서 실행하기에 결과는 같다.
  console.log(arr);
  return arr;
}

convertArgsToArray(1, 2, 3);
```
문제1
```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.doSomething = function(callback) {
  if(typeof callback == 'function') {
    // --------- 1   this == person 메소드 안에서의 this는 메소드 소유주이다.
    callback();
  }
};

function foo() {
  console.log(this.name); // --------- 2    this == global(window)
}

var p = new Person('Lee');
p.doSomething(foo);  // undefined
```
해결책
```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.doSomething = function(callback) {
  if(typeof callback == 'function') {
    callback.call(this);
  }
};

function foo() {
  console.log(this.name);
}

var p = new Person('Lee');
p.doSomething(foo);  // 'Lee'
```