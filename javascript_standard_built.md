# JAVASCRIPT - STANDARD BUILT-IN OBJECTS
모든 빌트인 객체들은 WINDOW객체에 소속된다. 그것들을 GLOBAL 객체라고도 한다.  
전역에서의 THIS : 전역객체를 의미한다.
## 1. Global object
전역 객체 : 모든 객체의 유일한 최상위 객체를 의미  
> 일반적으로 browser-side : window, serverside : global을 의미

`실행 컨텍스트가 생기기 전에 GO가 존재한다.`

```javascript
// in browser console
this === window // true

// in Terminal
node
this === global // true
```
- 개발자가 전역객체를 생성한는 것은 불가능하다.
- 전역객체는 전역 스코프를 갖게된다.
- 전역객체의 자식 객체를 사용할 때 전역 객체의 기술은 생략할 수 있다.
- 사용자가 정의한 변수와 전역객체의 자식 객체 이름이 충돌할 때 명확히 전역객체를 기술해 혼동을 방지할 수 있다.
- 전역객체는 전역변수를 프로퍼티로 가지게 된다.
- 글로벌 영역에 선언한 함수도 전역객체의 프로퍼티로 접근할 수 있다.
```javascript
function moveTo(url) {
  var location = {'href':'move to '};
  alert(location.href + url); // bom에 있는 location
  // location.href = url;
  window.location.href = url;
}
moveTo('http://www.google.com');
```

### 1. global property(전역 프로퍼티)
전역프로퍼티 : 간단한 값을 나타내고, 다른프로퍼티나 메소드를 가지고 있지 않다.
> 다음의 프로퍼티는 모두 global object의 프로퍼티이다.

---

#### 1. infinity
양/음의 무한대를 나타내는 숫자값이다.
```javascript
console.log(3/0);  // Infinity
console.log(-3/0); // -Infinity
console.log(Number.MAX_VALUE * 2); // 1.7976931348623157e+308 * 2
//Max_value : 상수
console.log(typeof Infinity); // number
```

#### 2. NaN
숫자가 아님(not a number)을 나타내는 숫자값이다.
>NaN 프로퍼티는 Number.NaN프로퍼티와 같다.
```javascript
console.log(Number('xyz')); // NaN
console.log(1 * 'string');  // NaN
console.log(typeof NaN);    // number
```

#### 3. undefined
변수에 값이 대입되지 않았음을 나타내는 값.

> 초기값은 기본자료형 undefined이다.
```javascript
var foo;
console.log(foo); // undefined
console.log(typeof undefined); // undefined
```
---
### 2. global function(전역 함수)
전역에서 호출할 수 있으며 호출한 곳으로 결과값을 반환한다.  
> 다음 함수는 모두 전역객체의 함수 프로퍼티 이다.

#### 1. eval()
파라미터로서 전달된 문자열 구문 또는 표현식을 평가, 실행한다.

> 사용자로부터 입력받은 Contents(untrusted data)를 eval()로 실행하는 것은 매우 보안에 취약하다. 가급적 이함수의 사용은 금지되어야 한다.

```javascript
eval(string)
// string: code 또는 표현식을 나타내는 문자열. 표현식은 존재하는 객체들의 프로퍼티들과 변수들을 포함할 수 있다.

var foo = eval('2 + 2');
var x = 5,
    y = 4;
console.log(foo); // 4
console.log(eval('x * y')); // 20
```

#### 2. isFinite()
매개변수로 전달된 값이 유한수인지 , 정상적인 수인지를 검사해 그 결과를 boolean으로 반환한다.  
> 매개변수가 숫자가 아닌 경우, 숫자로 변환한후 검사를 수행한다.

```javascript
isFinite(testValue)
// testValue: 검사 대상 값

console.log(isFinite(Infinity));  // false
console.log(isFinite(NaN));       // false
console.log(isFinite('Hello'));   // false
console.log(isFinite('2005/12/12'));   // false

console.log(isFinite(0));         // true
console.log(isFinite(2e64));      // true
console.log(isFinite(null));      // true: null->0

Number(null)  // 0
Boolean(null) // false
```

>isFinite(null)은 true를 반환하는데 이것은 null을 숫자로 변환해 검사를 수행하였기 때문

#### 3. isNaN()
매개변수로 전달된 값이 NaN인지를 검사해 그 결과를 boolean으로 반환한다. 
> 매개변수가 숫자가 아닌경우, 숫자로 변환한 후 검사를 수행한다.

```javascript
isNaN(testValue)
// testValue: 검사 대상 값

isNaN(NaN)       // true
isNaN(undefined) // true: undefined -> NaN
isNaN({})        // true: {} -> NaN
isNaN('blabla')  // true: 'blabla' -> NaN

isNaN(true)      // false: true -> 1
isNaN(null)      // false: null -> 0
isNaN(37)        // false

// strings
isNaN('37')      // false: '37' -> 37
isNaN('37.37')   // false: '37.37' -> 37.37
isNaN('')        // false: '' -> 0
isNaN(' ')       // false: ' ' -> 0

// dates
isNaN(new Date())             // false: new Date() -> Number
isNaN(new Date().toString())  // true:  String -> NaN
```

#### 4. parseFloat()
매개변수로 전달된 문자열을 부동소수점숫자로 변환해 반환한다.

```javascript
parseFloat(string)
// string: 변환 대상 문자열

parseFloat('3.14');     // 3.14
parseFloat('10.00');    // 10
parseFloat('34 45 66'); // 34
parseFloat(' 60 ');     // 60
parseFloat('40 years'); // 40
parseFloat('He was 40') // NaN
```

> 매개변수 문자열의 첫 숫자만 반환되며 전후 공백은 무시된다. 첫문자를 숫자로 변환할 수 없다면 NaN을 반환한다.

#### 5. parseInt()
매개변수로 전달된 문자열을 정수형 숫자로 반환해 반환한다.

```javascript
parseInt(string, radix);
// string: 변환 대상 문자열
// radix: 진법을 나타내는 기수(2 ~ 36, 기본값 10)

parseInt('10');       // 10
parseInt('10.33');    // 10
parseInt('34 45 66'); // 34
parseInt(' 60 ');     // 60
parseInt('40 years'); // 40
parseInt('He was 40') // NaN

parseInt('0x20');     // 32
parseInt('10', 16);   // 16
parseInt('10', 8);    // 8
```
> 매개변수 문자열의 첫 숫자만 반환되고 전후 공백은 무시된다. 첫문자를 숫자로 변환할 수 없다면 NaN을 반환한다.

#### 6. encodeURI()/decodeURI()
encodeURI() : 매개변수로 전달된 URI을 인코딩한다.

> 인코딩 : uri의 문자들을 이스케이프 처리하는 것

- 이스케이프 처리 : 네트워크를 통해 정보를 공유할 때 어떤 시스템에서도 읽을 수 있는 아스키문자로 변환하는 것.

decodeURI() : 매개변수로 전달된 URI를 디코딩한다.

```javascript
encodeURI(URI)
// URI: 완전한 URI
decodeURI(encodedURI)
// encodedURI: 인코딩된 완전한 URI

var uri = 'http://www.test.com/자바스크립트/test.php?who=나&target=너#전역 객체';
var enc = encodeURI(uri);
var dec = decodeURI(enc);
console.log(enc);
// http://www.test.com/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8/test.php?who=%EB%82%98&target=%EB%84%88#%EC%A0%84%EC%97%AD%20%EA%B0%9D%EC%B2%B4
console.log(dec);
// http://www.test.com/자바스크립트/test.php?who=나&target=너#전역 객체
```

#### 7. encodeURIComponent() / decodeURIComponent()
encodeURIComponent() : 매개변수로 전달된 uri컴포넌트를 인코딩한다.

> 인코딩 : uri문자들을 이스케이프 처리하는 것

decodeURIComponent() : 매개변수로 전달된 uri 컴포넌트를 디코딩 한다.

> encodeURIComponenet() : 인수를 쿼리스트링의 일부라고 간주한다.

```javascript
encodeURIComponent(URI)
// URI: URI component(구성 요소)
decodeURIComponent(encodedURI)
// encodedURI: 인코딩된 URI component(구성 요소)

var uriComp = 'who=나&target=너#전역 객체';
var enc = encodeURIComponent(uriComp);
var dec = decodeURIComponent(enc);
console.log(enc);
// who=%EB%82%98&target=%EB%84%88#%EC%A0%84%EC%97%AD%20%EA%B0%9D%EC%B2%B4
console.log(dec);
// who=나&target=너#전역 객체
```

## 2. Stnadard Built-in Objects (global objects)
프로그램 전체의 영역에서 공통적으로 필요한 기능을 사용자가 각자가 일일히 작성하는 수고를 줄이기 위해 표준 빌트인 객체를 제공한다.

### 1. Object
객체 생성자 : wrapper 객체를 생성ㅎ나다.

> 만약 생성자 인수값이 null이거나 undefined이면 빈 객체를 반환한다.
```javascript
// 변수 o에 빈 객체를 저장한다
var o = new Object();
console.log(typeof o + ': ', o);

o = new Object(undefined);
console.log(typeof o + ': ', o);

o = new Object(null);
console.log(typeof o + ': ', o);

// String 객체를 반환한다
// var o = new String('String');과 동치이다
var obj = new Object('String');
console.log(typeof obj + ': ', obj);
console.dir(obj);

var strObj = new String('String');
console.log(typeof strObj + ': ', strObj);

// Number 객체를 반환한다
// var o = new Number(123);과 동치이다
var obj = new Object(123);
console.log(typeof obj + ': ', obj);

var numObj = new Number(123);
console.log(typeof numObj + ': ', numObj);

// Boolean 객체를 반환한다.
// var o = new Boolean(true);과 동치이다
var obj = new Object(true);
console.log(typeof obj + ': ', obj);

var boolObj = new Boolean(123);
console.log(typeof boolObj + ': ', boolObj);
```

`객체를 생성할 경우 특수한 상황이 아니라면 객체리터럴방식을 사용하는 것이 일반적이다.`

### 2. Function
자바스크립트의 모든 함수는 Function 객체이다.

>다른 모든 객체들처럼 Function 객체는 new 연산자를 사용해 생성할 수 있다.

```javascript
var adder = new Function('a', 'b', 'return a + b');

adder(2, 6);  // 8
```

### 3. Boolean
기본자료형 boolean을 위한 wrapper객체  

> Boolean 생성자 함수로 Boolean 객체를 생성할 수 있다.

`Boolean 객체와 기본자료형 boolean을 혼동하기 쉽다.`

### 4. Number
### 5. Math
### 6. Date
### 7. String
### 8. RegExp
### 9. Array

### 10. Error
error 생성자 : error 객체를 생성한다.
> error 객체의 인스턴스는 런타임 에러가 발생했을 때 throw된다.

```javascript
try {
  // foo();
  throw new Error('Whoops!');
} catch (e) {
  console.log(e.name + ': ' + e.message);
}
```

- error관련된 객체
    - EvalError
    - InternalError
    - RangeError
    - ReferenceError
    - SyntaxError
    - TypeError
    - URIError

### 11. Symbol
ES6에서 추가된 유일하고 변경불가능한 기본자료형 
> 기본자료형 symbol을 위한 wrapper 객체를 생성

## 3. 기본자료형과 래퍼객체(Wrapper Object)
standard Built-in object는 각자의 프로퍼티와 메소드를 가진다.

> 정적 프로퍼티, 메소드는 해당 인스턴스를 생성하지 않아도 사용할 수 있고, prototype 에 속해있는 메소드는 해당 prototype을 상속받은 인스턴스가 있어야만 사용할 수 있다.

` 기본자료형의 값은 연관된 객체(Wrapper 객체)로 일시 변환 `