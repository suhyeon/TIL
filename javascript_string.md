# JAVASCRIPT - STRING

기본자료형인 String을 다룰때 유용한 프로퍼티와 메소드를 제공하는 wrapper객체이다.

> `기본자료형이 wrapper객체의 메소드를 사용할 수 있는 이유`: 기본자료형으로 프로퍼티나 메소드를 호출할 때 기본자료형과 관련된 wrapper객체로 일시적으로 변환되 프로토타입 객체를 공유하게 되기 때문

## 1. String Constructor
String 객체 : String() 생성자 함수를 통해 생성할 수 있다.

> 전달된 인자는 모두 문자열로 변환된다.

```javascript
new String(value);

var strObj = new String('Lee');
console.log(strObj); // String {0: 'L', 1: 'e', 2: 'e', length: 3, [[PrimitiveValue]]: 'Lee'}

```
> 스트링도 유사배열이다.
`new 연산자를 사용하지 않고 String()생성자 함수를 호출하면 String 객체가 아닌 문자열 리터럴을 반환`
>이때 형변환이 발생할 수 있다.

## 2. String Property
### 1. String.length
문자열 내의 문자 갯수를 반환

## 3. String Method
### 1. String.prototype.charAt()
매개변수로 전달한 index번호에 해당하는 위치의 문자를 반환
>index번호는 0~(문자열 길이 -1)사이의 정수

```javascript
str.charAt(index)
```
> 지정한 index범위(0~str.length-1)를 벗어난 경우 빈문자열을 반환한다.

### 2. String.prototype.indexOf()
문자열 내에 매개변수로 전달된 문자 또는 문자열이 처음 발견된 곳의 index를 반환. 
> 발견하지 못할 경우 -1을 반환

```javascript
str.indexOf(searchValue[, fromIndex])
// searchValue: 검색할 문자 또는 문자열
// fromIndex : 검색 시작 index (생략할 경우, 0)
```

### 3. String.prototype.lastIndexOf()
문자열 내에 매개변수로 전달된 문자또는 문자열이 마지막으로 발견된 곳의 index를 반환
>발견하지 못할 경우 -1을 반환

- 2번째 인수가 전달되면 검색 시작위치를 fromIndex로 이동해 역방향으로 검색을 시작
> 이때 검색범위 : 0~fromIndex

```javascript
str.lastIndexOf(searchValue[, fromIndex])
// searchValue: 검색할 문자 또는 문자열
// fromIndex  : 검색 시작 index (생략할 경우, 문자열 길이 - 1)
```

### 4. String.prototype.replace()
첫번째 인수로 전달된 문자열 또는 정규표현식을 대상 문자열에서 검색후 두번째 인수로 전달된 문자열로 대체

> 검색된 문자열이 복수 존재할 경우 첫째로 검색된 문자열만 대체된다.
```javascript
str.replace(pattern, replacement[, flags])
// pattern: 검색 대상 문자열 또는 정규표현식
// replacement: 치환 문자열
```

첫번째 인자에는 문자열 또는 정규표현식이 전달된다.
- 문자열의 경우 
  - 첫번째 검색 결과만이 대체된다
- 정규표현식의 경우
  - 다양한 방식으로 검색할 수 있다.

> /hello/ : 패턴, 검색할 대상을 의미

> gi : flag라 하는데 g(global)은 문자열내에 패턴과 일치하는 모든 문자열을 검색하라는 의미

> i(ignore) : 대소문자를 구분하지 말라는 의미

### 5. String.prototype.split()
첫번째 인수로 전달된 문자열 또는 정규표현식을 대상 문자열에서 검색해 문자열을 구분한 후 분리된 각 문자열로 이루어진 배열을 반환

> 인수가 없는 경우, 대상 문자열 전체를 단일 요소로 하는 배열을 반환

```javascript
str.split([separator[, limit]])
// separator: 구분 대상 문자열 또는 정규표현식
// limit: 구분 대상수의 한계를 나타내는 정수

var str = 'How are you doing?';

var splitStr = str.split(' ');
console.log(splitStr); // [ 'How', 'are', 'you', 'doing?' ]

splitStr = str.split();
console.log(splitStr); // [ 'How are you doing?' ]

splitStr = str.split('');
console.log(splitStr); // [ 'H','o','w',' ','a','r','e',' ','y','o','u',' ','d','o','i','n','g','?' ]

splitStr = str.split(' ', 3);
console.log(splitStr); // [ 'How', 'are', 'you' ]

splitStr = str.split('o');
console.log(splitStr); // [ 'H', 'w are y', 'u d', 'ing?' ]
```

### 6. String.prototype.substring()
첫번째 인수로 전달된 index에 해당하는 문자부터 두번째 인수로 전달된 index에 해당하는 문자의 `바로 이전 문자까지`를 모두 반환한다.
>이때 첫번째 인수 < 두번째 인수의 관계가 성립된다.

- 첫번째 인수 > 두번째 인수 : 두 인수 모두 교환된다.
- 두번째 인수가 생략된 경우 : 해당 문자열의 끝까지 반환
- 인수 < 0 또는 NaN : 0으로 취급된다.
- 인수 > 문자열의 길이 (str.length) : 인수는 문자열의 길이로 취급된다.

```javascript
str.substring(indexA[, indexB])
// indexA: 0 ~ 해당문자열 길이 -1 까지의 정수
// indexB: 0 ~ 해당문자열 길이까지의 정수
```

### 7. String.prototype.toLowerCase()
문자열의 문자를 모두 소문자로 변경

### 8. String.prototype.toUpperCase()
문자열의 문자를 모두 대문자로 변경

### 9. String.prototype.trim()
문자열 양쪽 끝에 있는 공백 문자를 제거한 문자열을 반환
>이때 해당 문자열 자신은 변경되지 않는다.
`문자열은 변경 불가능한 값이기 때문!`