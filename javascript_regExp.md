# JAVASCRIPT - RegEXP

## 1. 정규표현식(REGULAR EXPRESSION)
문자열에서 특정 내용을 찾거나 대체 또는 발췌하는데 사용한다.

> EX ) 회원가입화면에서 사용자로부터 입력받는 전화번호가 유효한지 체크할 때

```javascript
var tel = '0101234567팔';

var myRegExp = /^[0-9]+$/;

console.log(myRegExp.test(tel)); // false
```

`정규표현식 장단점`
- 장점
  - 복잡한 코드도 매우 간단하게 표현할 수 있다.
- 단점
  - 주석이나 공백을 허용하지 않고 여러가지 기호를 혼합해 사용하기 때문에 가독성이 떨어지는 문제가 있다.

```javascript
/pattern/flag;

var myRegExp = /regexr/i;

/ : 시작,종료기호
regexr : 패턴
i : 플래그(flag)
```

### 1. 플래그

종류
- i : ignorecase
  - 대소문자를 구별하지 않고 검색
- g : global
  - 문자열내의 모든 패턴을 검색
- m : multi line
  - 문자열의 행이 바뀌더라도 검색을 계속진행

> 플래그를 사용하지 않은 경우 문자열내 검색 매칭 대상이 1개 이상이더라도 첫번째 매칭한 대상만을 검색후 종료 

- match : 정규표현식으로 일치하는 것은 배열료 반환된다.

### 2. 패턴
찾고자 하는 대상을 문자열로 지정

> 특별한 의미를 가지는 메타문자 또는 기호로 표현할 수 있다.

```javascript
var targetStr = 'AA BB Aa Bb';
var regexr = /.../;  // 패턴과 일치하는 3자리 문자를 추출한다.
// . : 임의의 문자 한개를 의미
// 문자의 내용은 무엇이든지 상관없다.

console.log(targetStr.match(regexr)); // 'AA '

var regexr = /.../g;
console.log(targetStr.match(regexr)); // [ 'AA ', 'BB ', 'Aa ' ]
// g : 추출을 반복

var regexr = /./g;
console.log(targetStr.match(regexr));
// [ 'A', 'A', ' ', 'B', 'B', ' ', 'A', 'a', ' ', 'B', 'b' ]
// . g : 모든 문자를 선택

var regexr = /A/;
console.log(targetStr.match(regexr)); // 'A'
// /A/ : 일치하는 문자 또는 문자열을 추출(A)

var regexr = /A/ig;
console.log(targetStr.match(regexr)); // [ 'A', 'A', 'A', 'a' ]
// i : 대소문자를 구별하지 않게 하려하는것
// 패턴과 일치한 첫번째 결과만 반환

var regexr = /A+/g;
console.log(targetStr.match(regexr)); // [ 'AA', 'A' ]
// + : 앞선 패턴을 최소 한번 반복

var regexr = /A|B/g;
console.log(targetStr.match(regexr)); // [ 'A', 'A', 'B', 'B', 'A', 'B' ]
// | : or의 의미

var regexr = /A+|B+/g;
console.log(targetStr.match(regexr)); // [ 'AA', 'BB', 'A', 'B' ]
// + : 분해되지 않은 단어레벨로 추출 

var regexr = /[AB]+/g;
console.log(targetStr.match(regexr)); // [ 'AA', 'BB', 'A', 'B' ]
// 패턴을 or로 한번이상 반복하는것
//[]안의 문자는 or로 동작
// +를 사용하면 앞선 패턴을 한번 이상 반복

var regexr = /[A-Z]+/g;
console.log(targetStr.match(regexr)); // [ 'AA', 'BB', 'A', 'B' ]
// 범위를 지정하려면 [] 안에 -를 사용한다.
// 대문자 알파벳을 추출한다.

var regexr = /[A-Za-z]+/g;
console.log(targetStr.match(regexr)); // [ 'AA', 'BB', 'Aa', 'Bb' ]
// 대소문자르 구별하지 않고 알파벳을 추출하려는 것

var regexr = /[0-9]+/g;
console.log(targetStr.match(regexr)); // [ '24', '000' ]
//숫자를 추출하는 방법

var regexr = /[0-9,]+/g;
console.log(targetStr.match(regexr)); // [ '24,000' ]
// 컴마 때문에 결과과 분리되니 패턴에 포함시킨다.

var regexr = /[\d,]+/g;
console.log(targetStr.match(regexr)); // [ '24,000' ]
// \d : 숫자를 의미
// \D : \d와 반대로 동작

var regexr = /[\w,]+/g;
console.log(targetStr.match(regexr)); // [ 'AA', 'BB', 'Aa', 'Bb', '24,000' ]
// \w : 알파벳과 숫자를 의미 
// \W : /w과 반대로 동작
```

### 3. 자주 사용하는 정규 표현식

- 특정단어로 시작하는지 검사
```javascript
var targetStr = 'abcdef';
var regexr = /^abc/;
console.log(regexr.test(targetStr)); // true
```

- 특정단어로 끝나는지 검사
```javascript
var targetStr = 'abcdef';
var regexr = /ef$/;
console.log(regexr.test(targetStr)); // true
```

- 숫자인지검사
```javascript
var targetStr = '12345';
var regexr = /^\d+$/;
console.log(regexr.test(targetStr)); // true
```

- 공백으로 시작하는지 검사
```javascript
var targetStr = ' Hi!';
var regexr = /^[\s]+/;
console.log(regexr.test(targetStr)); // true
```

- 아이디로 사용가능한지 검사 ( 영문, 숫자만 허용, 4~10자리)
```javascript
var targetStr = 'abc123';
var regexr = /^[A-Za-z0-9]{4,10}$/
console.log(regexr.test(targetStr)); // true
```

- 메일 주소 형식에 맞는지 검사
```javascript
var targetStr = 'ungmo2@gmail.com';
var regexr =  /^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/i;
console.log(regexr.test(targetStr)); // true
```

- 핸드폰 형식에 맞는지 검사
```javascript
var targetStr = '010-1234-5678';
var regexr = /^\d{3}-\d{3,4}-\d{4}$/;
console.log(regexr.test(targetStr)); // true
```

- 특수 문자 포함 여부를 검사
```javascript
var targetStr = 'abc#123';
var regexr = /[\{\}\[\]\/?.,;:|\)*~`!^\-_+<>@\#$%&\\\=\(\'\"]/gi
console.log(regexr.test(targetStr)); // true
```

## 2. JAVASCRIPT REGULAR EXPRESSION

### 1. RegExp Constructor
RegExp 객체를 생성하기 위해 리터럴방식과 RegExp 생성자 함수를 사용할 수 있다.
> 일반적인 방법 : 리터럴 방식

```javascript
new RegExp(pattern[, flags])
```

- pattern 
  - 정규표현ㅅ기의 텍스트
- flag
  - 정규표현식의 플래그(g, i, m, u, y)

### 2. RegExp Method

#### 1. RegExp.prototype.exec()
문자열을 검색해 매칭 결과를 반환

>반환값은 배열 또는 null이다.

#### 2. RegExp.prototype.test()
문자열을 검색해 매칭 결과를 반환

> 반환값은 true 또는 false이다.

