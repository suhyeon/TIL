# JAVASCRIPT - DATA TYPE & VARIABLE
데이터 타입구분을 스크립트 엔진 메모리에 7가지로 구분되어 있다.  
literal을 인식해 알아서 분류를 하는 과정을 거친다.

`JavaScript는 동적 타이핑(Dynamic Typing) 언어로 변수의 Type annotation이 필요없이 값이 할당되는 과정에서 자동으로 자료형이 결정(Type Inference)된다. `

같은 변수에 여러 자료형의 값을 대입할 수 있다.
## 1. DATA TYPE (자료형)

- 기본 자료형 
    - BOOLEAN
    - NULL
    - UNDEFINED
    - NUMBER
    - STRING 
    - SYMBOL (ECMA 6 에서 추가)
- 객체형
    - OBJECT

---

### 1.1 기본 자료형 
변경 불가능한 값이다. pass-by-value

모든 기본자료형은 레포 객체가 있어서 순간 객체화 하는 것이 가능하다.

---

#### 1.1 BOOLEAN
논리적인 요소를 나타내며 true, false 두가지 값을 가진다.  
비어있는 문자열과 null, undefined, 0 은 false로 간주된다.

#### 1.2 NULL
null 타입 한가지 하나.  
js 는 case-sensitive 하기에 null 은 Null, NULL 과 다르다.

` 주의할 것은 데이터 형식을 나타내는 문자열을 반환하는 typeof 연산자로 null값은 가진 변수를 연산해 보면 null이 아닌 object가 나온다. ` 

> null 타입 변수 확인: 일치연산자(===)를 사용해야 한다.  


#### 1.3 undefined
값을 할당하지 않은 변수의 타입.
`선언은 되었지만 할당된 적이 없는 변수에 접근하거나 존재하지 않는 객체 프로퍼티에 접근할 경우 반환된다.`

> javascript 엔진이 DOM 트리를 건드리면서 데이터가 손상된다. 그래서 자주 해커들이 해킹할 때 서버가 스크립트엔진에게 데이터를 응답해야할 때 스크립트 엔진이 그 데이터 안에 태그나, 스크립트 태그가 있는지 확인해봐야한다.

#### 1.4 Number
c 언어, 정수형과 실수형을 구분 - int, float, long, double등과 같은 다양한 숫자자료형이 존재한다.

javascript - 하나의 숫자 자료형만 존재

ECMA Script 표준 - 숫자자료형은 배정밀도 64비트 부동소수점형(double precision 64-bit floating-point format) 단하나만 존재  
정수만을 표현하기 위한 특별한 자료형은 없다. (integer type)은 없다.

```
var x = 10;    // 정수
var y = 10.12; // 실수
var z = -20;   // 음의 정수

var foo = 42 / -0;
console.log(foo);        // -Infinity
console.log(typeof foo); // number

var bar = 1 * 'string';
console.log(bar);        // NaN
console.log(typeof bar); // number
```
+infinity : 양의 무한대
-infinity : 음의 무한대
NaN : Not a Number : 숫자가 아니다.

#### 1.5 String
문자열 타입은 텍스트 데이터를 나타내는데 사용  
0개 또는 그이상의 유니코드 문자들의 집합  

```
var str = "string";      // double quotes
    str = 'string';      // single quotes
console.log(typeof str); // string

var answer = "It's alright";        // Single quote inside double quotes
    answer = "He is called 'John'"; // Single quotes inside double quotes
    answer = 'He is called "John"'; // Double quotes inside single quotes
```

> 자바스크립트의 문자열은 변경 불가능 (한번 문자열이 생성되면, 그 문자열을 변경할 수 없다는 걸 의미)

` 문자열은 배열처럼 인덱스를 통해 접근할 수 있다.`

새로운 문자열을 할당하는 건 가능! 기존 문자열을 수정하는 게 아니라 새로 문자열울 할당하는 것이기 때문이다!  

```
var str = 'string';
console.log(str); // string

str = 'String';
console.log(str); // String

str += ' test';
console.log(str); // String test

str.substring(0, 3);
console.log(str); // Str

str = str.toUpperCase();
console.log(str); // STR
```

object : 변경이 가능하다.
나머지는 변경이 불가능하다.

> 문자열 내에 It's 와같은 문구가 삽입될 때는 문자열을 ""로 막아서 표현해준다.

#### 1.6 Symbol
ES6에서 새로 추가된 7번째 타입.   
어플리케이션 전체에서 유일하고 변경 불가능한 기본 자료형.  
` 주로 객체의 프로퍼티 키로 사용한다.`
> 유일하기 때문에 symbol값을 키로 갖는 프로퍼티는 다른 어떤 프로퍼티와도 충돌하지 않는다.

---

### 2. 객체형 (참조형)
객체 : 데이터와 그 데이터에 관련되는 동작을 모두 포함할 수 있는 개념적 존재  
`이름과 값을 가지는 데이터를 의미하는 프로퍼티와 동작을 의미하는 메서드를 포함하고 있는 독립적 주체`

- 함수(function)
- 배열(array)
- 날짜(date)
- 정규식(RegExp)

>객체는 pass by reference이다.

--- 

## 2. 변수 (Variable)

어플리케이션에서 값을 유지할 필요가 있을 때 사용한다.  

값을 저장,조회,조작하는데 사용되며 다른 사용자가 변수의 존재 목적을 쉽게 이해할 수 있도록 이름을 지정해야 한다.

- 반드시 영문자, _, $로 시작해야한다.
- 이어서는 숫자도 사용할 수 있다.
- 대/소문자를 구별한다.

> 미선언 변수에 접근하면 reference Error 예외가 발생한다.

undefined : c언어의 경우, 선언하고 초기화가 이루어져있지 않으면 메모리에 쓰레기값이 있는 곳에 선언했을 가능성이 있다. 그걸 자바스크립트에선 방지하고자 undefined를 알아서 초기화 해주려는 설이있다.

---
### 1. 변수의 중복선언
변수는 중복선언이 가능하다.

>변수의 중복선언은 문법적으로 허용되지만 의도치 않게 변수의 값을 변경할 수 있으므로 사용하지 않는 것이 좋다.

### 2. 변수 선언시 var 키워드 생략 허용
변수 선언시 var 키워드를 생략할 수 있다.

> 문법적으로 허용되지만 의도치 않게 변수를 전역화 할 수 있으므로 사용하지 않는 것이 좋다.

### 3. 동적 타이핑
동적 타입언어 혹은 느슨한 타입언어 이다.  
변수의 type annotation이 필요없이 값이 할당되는 과정에서 자동으로 자료형이 결정될 것이라는 뜻!  
같은 변수에 여러 data type의 값을 대입할 수 있다. - 동적타이핑

```
var foo;

console.log(typeof foo);  // undefined

foo = null;
console.log(typeof foo);  // object

foo = {};
console.log(typeof foo);  // object

foo = 3;
console.log(typeof foo);  // number

foo = 3.14;
console.log(typeof foo);  // number

foo = 'Hi';            
console.log(typeof foo);  // string

foo = true;                  
console.log(typeof foo);  // boolean
```
하나의 변수로 여러개의 타입을 설정할 수 있지만 그냥 쓰고 버려라!

### 4. 변수 호이스팅

```
console.log(foo); // ① undefined
var foo = 123;
console.log(foo); // ② 123
{
  var foo = 456;
}
console.log(foo); // ③ 456
```

>그렇다면 js에서는 글로벌 배리어블만 있고 로컬배리어블은 없는 것인가.

해답 : ~!

- function-level-scope 
    - 함수내에서 선언되 변수는 지역변수, 함수외부에서 선언한 변수는 모두 전역 변수
- Block-level-scope
    - 코드블럭 내에서 선언된 변수는 코드블럭내에서만 유효, 코드블럭외부에서는 참조할 수 없다.

### 5. var 키워드로 선언된 변수의 문제점

- function-level-scope
    - 전역 변수의 남발
    - for loop 초기화 식에서 사용한 변수를 for loop 외부 또는 전역에서 참조할 수 있다.
- var 키워드 생략 허용
    - 의도하지 않은 변수의 전역화
- 중복 선언 허용
    - 의도하지 않은 변수값 변경
- 변수 호이스팅
    - 변수를 선언하기 전에 참조가 가능하다.

> 대부분의 문제는 전역변수로 인해 발생한다.

` 변수의 범위(scope)는 좁을 수록 좋다.`  

` 전역변수는 범위가 넓어서 어디에서 어떻게 사용될지 파악하기 힘들다. 이는 의도치 않은 변수의 변경이 발생할 수 있는 가능성이 증가한다.`

> function안에서 가급적 변수를 선언하라~! (깨달은것)