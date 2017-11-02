# JAVASCRIPT - NUMBER
기본자료형 NUMBER를 위한 WRAPPER 객체

> 기본자료형이 WRAPPER 객체의 메소드를 사용할 수 있는 이유 : `기본자료형으로 프로퍼티나 메소드를 호출할 때 기본자료형과 연관된 wrapper 객체로 일시적으로 변환되어 프로토타입 객체를 공유하게 되기 때문`

## 1. NUMBER CONSTRUCTOR
NUMBER 객체는 NUMBER()생성자 함수를 통해 생성할 수 있다.

>인자가 숫자로 변환할 수 없다면 NaN을 반환

`Number()생성자 함수를 new를 붙이지 않아 생성자로 사용하지 않으면 Number객체를 반환하지 않고 기본자료형 숫자를 반환한다.`
>이때 형변환이 발생할 수 있다.

## 2. Number Property
정적 프로퍼티. Number 객체를 생성할 필요 없이 Number.propertyName의 형태로 사용한다.

### 1. Number.EPSILON
자바스크립트에서 표현할 수 있는 가장 작은 수

>부동소수점의 비교는 Number.EPSILON을 사용해 비교 기능을 갖는 함수를 작성해야 한다.

```javascript
console.log(0.1 + 0.2);        // 0.30000000000000004
console.log(0.1 + 0.2 == 0.3); // false!!!

function isEqual(a, b){
  // Math.abs는 절대값을 반환한다.
  // 즉 a와 b의 차이가 JavaScript에서 표현할 수 있는 가장 작은 수인 Number.EPSILON보다 작으면 같은 수로 인정할 수 있다.
  return Math.abs(a - b) < Number.EPSILON;
}

console.log(isEqual(0.1 + 0.2, 0.3));
```
> 2.2204460492503130808472633361816E-16

### 2. Number.MAX_vALUE
자바스크립트에서 사용가능한 가장 큰숫자 를 반환한다.

>1.7976931348623157e+308 (지수표기법)

`MAX_VALUE보다 큰 숫자는 Infinity이다.`

### 3. Number.MIN_VALUE
자바스크립트에서 사용 가능한 가장 작은 숫자를 반환한다.

>0에 가장 가까운 양수 값이다. 
`MIN_vALUE보다 작은 숫자는 0으로 변환된다.`

? 궁금점 : Number.EPSILON과 차이점
어떠한 비교값보다 큰 수들 중에서 가장 작은 수  
EX) 0.1 < 0.0000000....1과의 차이 : EPSILON
### 4. Number.POSITIVE_INFINITY
양의 무한대를 반환

### 5. Number.NEGATIVE_INFINITY
음의 무한대를 반환

### 6. Number.NaN
숫자가 아님을 나타내는 숫자값.

## 3. Number Method

### 1. Number.isFinite()
매개변수를 통해 전달된 값이 유한수인지, 정상적인 수인지를 검사해 결과를 Boolean으로 반환한다.

>전역함수 isFinite()차이점 : 전역함수 isFinite()는 인수를 숫자로 변환해 검사를 수행하지만 Number.isFinite()는 인수를 변환하지 않는다.

`숫자가 아닌 인수가 주어졌을 때는 언제나 false가 된다.`
```javascript
Number.isFinite(testValue)
// testValue: 검사 대상 값
```
### 2. Number.isInteger()
매개변수를 통해 전달된 값이 정수인지 검사해 그 결과를 boolean으로 반환한다.

> 검사전에 인수를 숫자로 변환하지 않는다.
```javascript
Number.isInteger(testValue)
// testValue: 검사 대상 값
```
### 3. Number.isNaN()
매개변수를 통해 전달된 값이 NaN인지 검사해 그 결과를 boolean을 반환한다.

>isNaN() 차이점 : isNaN은 인수를 숫자로 변환해 검사를 수행하지만 Number.isNaN은 인수를 변환하지 않는다.

`따라서 숫자가 아닌 인수가 주어지면 언제나 false가 된다.`
```javascript
Number.isNaN(testValue)
// testValue: 검사 대상 값
```
### 4. Number.isSafeInteger()
매개변수를 통해 전달된 값이 안전한 정수인지 검사해 그 결과를 boolean으로 반환한다.

> 범위 : (253 - 1)와 -(253 - 1) 사이의 정수값

`검사 전에 인수를 숫자로 변환하지 않는다.`

소속 : Number.constructor
```javascript
Number.isSafeInteger(testValue)
// testValue: 검사 대상 값
```
### 5. Number.prototype.toExpotential()
대상을 지수 표기법으로 변환해 문자열로 반환

> 지수 표기법 : 매우 큰 숫자를 표기할 때 주로 사용하고 e(Exponent)앞에 있는 숫자에 10의 n승이 곱하는 형식
```javascript
numObj.toExponential([fractionDigits])
// fractionDigits: 0~20 사이의 정수값으로 소숫점 이하의 자릿수를 나타낸다. 옵션으로 생략 가능하다.  
```
### 6. Number.prototype.toFixed()
매개변수로 지정된 소숫점자리를 반올림해 문자열로 반환
```javascript
numObj.toFixed([digits])
// digits: 0~20 사이의 정수값으로 소숫점 이하 자릿수를 나타낸다. 기본값은 0이며 옵션으로 생략 가능하다.
```

### 7. Number.prototpye.toPrecision()
매개변수로 지정된 전체 자릿수 까지 유효하도록 나머지 자릿수를 반올림해 문자열로 반환한다.

```javascript
numObj.toPrecision([precision])
// precision: 1~21 사이의 정수값으로 전체 자릿수를 나타낸다. 옵션으로 생략 가능하다.
```

### 8. Number.prototype.toString()
숫자를 문자열로 반환해 반환한다.

```javascript
numObj.toString([radix])
// radix: 2~36 사이의 정수값으로 진법을 나타낸다. 옵션으로 생략 가능하다.
```
Num -> Str
- '' + num
- toString
- String(Num) : 금지된 사용법

Str -> Num
- 1*str (단, str 값이 숫자로 변환될 수 있다는 전제하)
- parseInt
- Number(str)
### 9. Number.prototype.valueOf()
Number객체의 기본자료형 값을 반환한다.
```javascript
numObj.valueOf()
```

사용빈도 높은 것: Number.EPSILON(입사용), NUMBER.PROTOTYPE.-