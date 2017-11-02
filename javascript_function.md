# JAVASCRIPT - FUNCTION

- 함수란 어떤 특정 작업을 수행하기 위해 필요한 일련의 구문들을 그룹화하기 위한 개념
- 함수의 일반적 기능
  - 특정작업을 수행하는 구문들의 집합을 정의, 필요시에 호출해 필요한 값 또는 수행결과를 얻는 것
- 함수도 객체이다.
- 객체와 차이점 : 호출할 수 있다.
- 변수나 객체, 배열 등에 저장될 수 있고, 다른 함수에 전달되는 인수로도 사용될 수 있으며 함수의 반환값이 될 수 도 있다.

## 1.  함수 정의

- 함수 선언식
- 함수 표현식
- function() 생성자 함수

### 1. 함수 선언식

- 함수명 
  - 함수명은 생략할 수 없다.(함수선언식)
- 매개변수 목록
  - 0개 이상의 목록을 괄호로 감싸고 ','로 분리한다.
  - 다른언어와의 차이점 : 매개변수의 자료형을 기술하지 않는다. (함수 몸채내에서 매개변수의 자료형 체크를 필요할 수 있다.)
- 함수 몸체
  - 실제 함수가 호출되었을 때 실행되는 구문들의 집합
  - return문으로 결과값을 반환할 수 있다. (반환값)

>return 값이 없다면 명확하게는 undefined를 반환한다.

` 함수 호이스팅이 일어난다.`

### 2. 함수 표현식

함수 리터럴 방식으로 함수를 정의하고 변수에 할당하는 방식

자바스크립트의 함수는 일급객체  

`함수의 특징`
- 무명의 리터럴로 표현이 가능하다.
- 변수나 자료구조에 저장할 수 있다.
- 함수의 파라미터로 전달할 수 있다.
- 반환값으로 사용할 수 있다.

```javascript
// 기명 함수표현식(named function expression)
var foo = function multiply(a, b) {
  return a * b;
};
// 익명 함수표현식(anonymous function expression)
var bar = function(a, b) {
  return a * b;
};
```

` 함수 선언식도 함수표현식과 동일하게 함수 리터럴 방식으로 정의되는 것이다.`

> 일반적으로는, 익명함수표현식으로 사용한다. why? 변수에 할당해서 사용할 수 있기 때문

> 기명함수 : 디버거나 재귀함수에 사용하기 위해 사용한다. 

### 3. Function() 생성자 함수

문법
```javascript
new Function(arg1, arg2, ... argN, functionBody)
```

> function 생성자 함수로 생성하는 방식은 일반적으로 사용하지 않는다.

## 2. 함수 호이스팅

함수 선언의 위치와 상관없이 코드내 어느 곳에서든지 호출이 가능 : 함수 호이스팅

- 호이스팅
  -  var 선언문이나 function 선언문 등을 해당 Scope의 맨 위로 옮기는 것

  `즉 자바스크립트는 코드를 실행하기 전에 var 선언문과 function 선언문을 해당 스코프의 맨위로 옮긴다. `

  함수표현식의 경우 함수 호이스팅이 아니라 변수 호이스팅이 발생한다.

  > 변수 호이스팅은 변수 생성 및 초기화와 할당이 분리되어 진행된다. 호이스팅된 변수는 undefined로 초기화되고 실제값의 할당은 할당문에서 이루어진다.
## 코딩 습관!!!
반드시 호출 전에 선언할 것!!

  ## 3. First-class object(일급객체)
  생성, 대입, 연산, 인자 또는 반환값으로서의 전달등 프로그래밍 언어의 기본적 조작을 제한없이 사용할 수 있는 대상

`일급객체의 조건`
- 무명의 리터럴로 표현이 가능하다
- 변수나 자료구조에 저장할 수 있다.
- 함수의 파라미터로 전달할 수 있다.
- 반환값으로 사용할 수 있다.

## 4. 매개변수(parameter)
함수내에서 변수와 동일하게 동작한다.

### 1. 매개변수(parameter) vs 인수(argument)
- 매개변수 
  - 함수내에서 변수와 동일하게 메모리공간을 확보하며 전달되어진 인수는 매개변수에 할당된다.
  - 인수가 전달되지 않으면 파라미터는 undefined 초기화된다.
```javascript
var foo = function (p1, p2) { //매개변수
  console.log(p1, p2); //인수
};
```
### 2. call-by-value
기본자료형 인수는 call-by-value로 동작한다.

> 함수내에서 매개변수를 통해 값이 변경되어도 전달이 완료된 기본자료형 값은 변경되지 않는다.

### 3. caal-by-reference
객체타입 인수는 call-by-reference로 동작한다.

> 함수내에서 매개변수의 참조값을 이용해 객체의 값을 변경했을 때 전달되어진 참조형의 인수값도 변경된다.

## 5. 반환값 (return value)
함수는 자신을 호출한 코드에게 수행한 결과를 반환할 수 있다.
- return 키워드는 함수를 호출한 코드에게 값을 반환할 때 사용한다.
- 함수는 배열등을 이용해 한번에 여러개의 값을 리턴할 수 있다.
- 함수는 반환을 생략할 수 있다. 함수는 암묵적으로 undefined를 이때 반환한다.
- 자바 스크립트 해석기는 return 키워드를 만나면 함수의 실행을 중단한 후 함수를 호출한 코드로 되돌아간다.
- 만약 return 키워드 이후 다른구문이 존재해도 그 구문은 실행되지 않는다.

## 6. 함수객체의 프로퍼티
함수도 프로퍼티를 가질 수 있다.

> 함수는 일반객체와는 다른 함수만의 표준프로퍼티를 갖는다.

### 1. arguments 프로퍼티
함수 호출시 전달된 인수들의 정보를 담고 있는 순화가능한 유사 배열 객체

> 함수 외부에서는 사용할 수 없다.

`매개변수는 인수로 초기화된다.`
- 매개변수의 갯수보다 인수를 적게 전달했을 때, 인수가 전달되지 않은 매개변수는 undefined로 초기화된다.
- 매개변수의 갯수보다 인수를 더많이 전달한 경우, 초과된 인수는 무시된다.


> argument 객체는 매개변수 갯수가 확정되지 않은 가변인자 함수를 구현할 때 유용하게 사용된다.

argument 객체는 배열의 형태로 인자값 정보를 담고 있지만, 실제 배열이 아닌 유사배열객체이다.

### 2. caller 프로퍼티
자신을 호출한 함수를 의미

> caller == null 인경우, 전역에서 바로 부르는 것을 의미

```javascript
function foo(func) {
  var res = func();
  return res;
}

function bar() {
  if (bar.caller == null) {
    return 'The function was called from the top!';
  } else {
    return 'This function\'s caller :\n' + bar.caller;
  }
}

console.log(foo(bar));
console.log(bar()); // caller == null
```
`node.js에서와 자바스크립트엔진에서의 전역의 범위가 다르다`

### 3. length 프로퍼티
함수 정의 시 작성된 매개변수 갯수를 의미
argument.length : 함수 호출시 인자의 갯수

### 4. name 프로퍼티
함수명을 나타냄. 기명함수의 경우 함수명을 값으로 갖고, 익명함수의 경우, 빈문자열을 값으로 갖는다.

### 5. __proto__ 프로퍼티

모든 객체는 자신의 프로토타입을 가리키는 [[Prototype]] 이라는 숨겨진 프로퍼티를 가진다.

- 왜 이러한 관계를 갖는 건가?
  - 유용하게 프로토타입체인이라는 것에서 답을 찾을 수 있다.

__proto__ == [[Prototype]]

> 자신의 부모를 찾을 때 __proto__를 이용해 찾을 수 있다.
```javascript
function square(number) {
  return number * number;
}

console.dir(square);
// console.dir(square);
console.dir(square.__proto__); //function.prototype
console.dir(square.prototype); //square.prototype

console.log(square.__proto__ === Function.prototype); // true ①
console.log(square.__proto__ === square.prototype);   // false
console.log(square.prototype.constructor === square); // true ②
console.log(square.__proto__.constructor === square.prototype.constructor); // false
```
> 모든 객체를 다가지고있는 링크 : __proto__

### 6. prototype 프로퍼티
모든 함수 객체는 prototype 프로퍼티를 갖는다.

> 주의할 것은 prototype 프로퍼티는 프로토타입 객체를 가리키는 [[Prototype]]프로퍼티와는 다르다.

- [[Prototype]] 프로퍼티
    - 모든 객체가 가지고 있는 프로퍼티
    - 객체의 입장에서 자신의 부모역할을 하는 프로토타입객체를 가리키며 함수객체의 경우 Function.prototype을 가리킨다.
- prototype 프로퍼티
    - 함수 객체만 가지고 있는 프로퍼티
    - 함수객체가 생성자로 사용될 때 이 함수를 통해 생성된 객체의 부모 역할을 하는 객체를 가리킨다.
    - 함수가 생성될 때 만들어지며 constructor 프로퍼티를 가지는 객체를 가리킨다.
    - constructor 프로퍼티는 함수 객체 자신을 가리킨다.

## 7. 함수의 다양한 형태

### 1. 즉시 호출함수표현식 (Immediately Invoke Function Expression, IIFE)
함수의 정의와동시에 실행되는 함수  

최초 한번만 호출되며 다시호출할 수는 없다.  

`이러한 특징을 이용해 최초 한번만 실행이 필요한 초기화 처리등에 사용할 수 있다.`

```javascript
// 기명 즉시실행함수(named immediately-invoked function expression)
(function myFunction() {
  var a = 3;
  var b = 5;
  return a * b;
}());
//function을 ()로 막아지는 이유 : 코드가 엉킬수 있어서.전역변수를 안만들기 위해서 사용할 수 도 있다.
```
자바스크립트의 가장 큰 문제점 : 글로벌 스코프에서 선언된 변수의 남발 (전역변수의 남발)

### 2. 내부 함수
함수내부에 정의된 함수
> closure와 관계가 있다.

`scope는 좁을 수록 좋다. 전역변수는 왠만하면 피하라`

내부함수는 자신을 포함하고 잇는 부모함수의 변수에 접근할 수있지만 부모는 그럴수 없다.

>내부함수는 부모함수 외부에서 접근할 수 없다.

### 3. 콜백 함수 
함수를 명시적으로 호출하는 방식이 아니라 특정 이벤트가 발생했을 때 시스템에 의해 호출되는 함수

ex ) 이벤트 핸들러 처리

```javascript
setTimeout(function(){
  console.log('1초 후 출력된다.');
}, 1000);
```

```javascript
    var button = document.getElementById('myButton');
    button.addEventListener('click', function() {
      console.log('button clicked!');
    }); //document : DOM의 가장 상위 객체
    //addEventListener : 이벤트를 등록하는 함수
    //클릭이라는 이벤트가 발생하면 어딘가에 대기하고 있다가 나중에 실행된다.
```
```javascript
setTimeout(function () {
  console.log('1초 후 출력된다.');
}, 1000); //setTimeout : 앞에 window객체가 생략된것이다.
//alert()도 마찬가지.
```

>콜백함수는 비동기식 처리모델과 관련이 있다.