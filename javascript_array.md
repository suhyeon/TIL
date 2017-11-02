# JAVASCRIPT- ARRAY
객체와 생성방식도 유사하고 생김새도 유사하다.

```javascript
var arr = [1,2,3];
//Array : object 타입

var numbersObject = {
  '0': 'zero',  '1': 'one',   '2': 'two',
  '3': 'three', '4': 'four',  '5': 'five',
  '6': 'six',   '7': 'seven', '8': 'eight',
  '9': 'nine' //유사배열 객체
}; //객체 리터럴로 유사하게 표현한 방식
```
>배열은 [대괄호 표기법]으로 사용하고 [안에는 인덱스번호가 온다].
## 1. 배열의 생성
### 1. 배열 리터럴
0개 이상의 값을 쉼표로 구분해 대괄호로 묶는다.
> 첫번째 값은 인덱스 '0'으로 읽을 수 있다.
`존재하지 않는 요소에 접근하면 undefined가 나온다.`

```javascript
var numbersObject = {
  '0': 'zero',  '1': 'one',   '2': 'two',
  '3': 'three', '4': 'four',  '5': 'five',
  '6': 'six',   '7': 'seven', '8': 'eight',
  '9': 'nine'
};
```
배열리터럴은 객체리터럴과 달리 프로퍼티 명이 없다.
> 각 요소의 값만이 존재, 대신 인덱스가 있다.

`요소들은 undefined까지도 올 수 있고 , 배열과 객체도 올 수 있다.`
```javascript
var emptyArr = [];
var emptyObj = {};

console.dir(emptyArr.__proto__);
console.dir(emptyObj.__proto__);
```

> 자바스크립트 배열은 어떤 데이터 타입의 조합이라도 포함할 수 있다.
### 2. Array() 생성자 함수
배열 리터럴 방식도 결국 내장함수 Array() 생성자 함수로 배열을 생성하는 것을 단순화시킨것

> Array()함수 : Array.prototype.constructor 프로퍼티로 접근할 수 있다.

`매개변수의 갯수에 따라 다르게 동작한다.`

- 매개변수가 1개이고 숫자인 경우
```javascript
new Array(arrayLength) // 인수에는 정수를 주게 되어있다.

// 매개변수로 전달된 숫자를 length 값으로 가지는 빈 배열 생성
var arr = new Array(2);
console.log(arr.length, arr); // 2 [undefined, undefined]
```

- 그 외의 경우
```javascript
new Array(element0, element1[, ...[, elementN]])

// 매개변수로 전달된 값을 요소로 가지는 배열을 생성
var arr = new Array(1, 2, 3);
console.log(arr.length, arr); // 3 [1, 2, 3]
```

## 2. 배열 요소의 추가와 삭제
### 1. 배열 요소의 추가
객체가 동적으로 프로퍼티를 추가할 수있는 것처럼 배열도 동적으로 요소를 추가할 수 있다.
> 순서에 맞게 값을 저장할 필요없이 인덱스위치에 값을 저장할 수 있다.

`값이 할당되지 않은 인덱스 위치의 요소값은 undefined가 되고 배열의 길이(length)는 최종 인덱스 위치의 기준으로 산정된다.`

```javascript
var arr = [];
console.log(arr[0]); // undefined

arr[0] = 'one';
arr[3] = 'three';
arr[7] = 'seven';

console.log(arr); // ["one", undefined × 2, "three", undefined × 3, "seven"]
```

### 2. 배열 요소의 삭제
배열은 객체이기 때문에 배열의 요소를 삭제하기 위해 delete연산자를 사용할 수 있다.

> 해당요소가 삭제되는 것이 아니라 요소 값이 삭제되어 undefined가 된다.

`해당 요소를 완전히 삭제하기 위해서 : Array.prototype.splice()`

```javascript
var numbersArr = ['zero', 'one', 'two', 'three'];

// 요소의 값만 삭제된다
delete numbersArr[2]; // ['zero', 'one', undefined, 'three']
console.log(numbersArr);

// 요소 일부를 삭제 (배열 시작점, 삭제할 요소수)
numbersArr.splice(2, 1); // ['zero', 'one', 'three']
console.log(numbersArr);
```

## 3. 배열요소의 열거
객체의 프로퍼티를 열거할 때 : for in 문을 사용
> 배열역시 객체이기에 사용가능

- for in 문을 사용하면 
  - 불필요한 프로퍼티까지 출력될 수 있고 `요소들의 순서를 보장하지 않으므로` 배열을 열거하는데 적합하지 않다.
- for문을 사용하면
  - 배열의 열거에 보다 나은 방법

```javascript
var numbersArr = ['zero', 'one', 'two', 'three'];
numbersArr.foo = 10;

for (var prop in numbersArr) {
  console.log(prop, numbersArr[prop]);
  // 0 zero / 1 one / 2 two / 3 three / foo 10
} //프로퍼티를 같이 불러온다.

for (var i = 0; i < numbersArr.length; i++) {
  console.log(i, numbersArr[i]);
  // 0 'zero' / 1 'one' / 2 'two' / 3 'three'
}//인덱스만 나온다.

//for-of문은 유용하다.
//유사배열들에 돌리기 위한 for문 방식이다.
```
## 4. Array property
### 1. Array.length
요소의 갯수(배열의 길이)를 나타낸다.
> 양의 정수,  2의 32승 미만이다.

`length 프로퍼티는 가장 큰 인덱스에 1을 더한 것 과 같다.`

- length프로퍼티의 값을 현재보다 큰 인덱스로 항목을 추가한다면
  - length프로퍼티는 새로운 항목을 추가할 수 있도록 자동으로 늘어난다.
- length프로퍼티의 값을 현재보다 작게 설정한다면
  - 설정한 값보다 크거나 같은 인덱스에 해당하는 요소는 모두 삭제된다.

```javascript
var arr = [
  'zero', 'one', 'two', 'three', 'four',
  'five', 'six', 'seven', 'eight', 'nine'
];

// 배열 길이의 명시적 설정
arr.length = 3; // [ 'zero', 'one', 'two' ]

// 배열 끝에 새 요소 추가
arr[arr.length] = 'san'; // [ 'zero', 'one', 'two', 'san' ]

arr.length = 5; // [ 'zero', 'one', 'two', 'san', undefined ]

// 배열 끝에 새 요소 추가
arr.push('go'); // [ 'zero', 'one', 'two', 'san', undefined, 'go' ]
```
>Array.prototype.push() : 매개변수로 전달된 값들을 배열의 마지막에 추가 (배열의 마지막 인덱스 위치에 값을 할당한 것과 같다.)

## 5. Array method
### 1. Array.isArray()
객체가 배열이면 true, 배열이 아니면 false를 반환

>static method : 생성자함수명.메소드
>method : 객체명.메소드  
>static의 생성자함수의 method는 new가 필요없이 GO에 이미 올라가 있다.
### 2. Array.prototype.indexOf()
배열에서 인수로 지정된 요소를 검색해 인덱스를 반환
> 중복된 요소가 있는 경우 첫번째 인덱스만 반환

- 해당하는 요소가 없는 경우
  - -1 을 반환
### 3. Array.prototype.concat(item..)
인수로 넘어온 값들을 자신의 복사본에 추가한 새로운 배열을 반환
> 인수는 배열 또는 값이다.

`원본 배열은 건드리지 않고 새로운 것을 만들어서 return한다.`

```javascript
var a = ['a', 'b', 'c'];
var b = ['x', 'y', 'z'];

var c = a.concat(b);
console.log(c); // ['a', 'b', 'c', 'x', 'y', 'z']

var d = a.concat('String');
console.log(d); // ['a', 'b', 'c', 'String']

var e = a.concat(b, true);
console.log(e); // ['a', 'b', 'c', 'x', 'y', 'z', true]

// 원본 배열은 변하지 않는다.
console.log(a); // [ 'a', 'b', 'c' ]
```
### 4. Array.prototype.join()
배열 요소 전체를 연결해 문자열을 만든다.
> 기본구분자 : ','

`+ 연산자보다 빠르다`
```javascript
var arr = ['a', 'b', 'c', 'd'];

var x = arr.join();
console.log(x);  // 'a,b,c,d';

var y = arr.join('');
console.log(y);  // 'abcd'

var z = arr.join(':');
console.log(z);  // 'a:b:c:d'
```
### 5. Array.prototype.pop()
push와 함께 배열을 스택(LIFO)처럼 동작하게한다. `후입선출`
> POP : 배열에서 마지막 요소를 제거하고 제거한 요소를 반환

- 빈 배열일 경우 
  - UNDEFINED 반환

> POP 메소드를 호출한 배열 자체가 수정된다.

### 6. Array.prototype.push(item..)
인수로 넘어온 항목을 배열의 끝에 추가

> contact메소드와 다르게 배열자체를 수정해 넘어온 인수 전체를 배열에 추가
`반환값은 새로운 length`

- 배열의 마지막에 값을 추가할 때
  - Array.prototype.push()
- 선두에 추가할 때
  - Array.prototype.unshift()
- 중간에 추가할 때 
  - Array.prototype.splice()

> push, unshift : 사용하기 간편하지만 performance 면에서 좋은 방법이 아니다.

```javascript
var a = ['a', 'b', 'c'];
var b = ['x', 'y', 'z'];

// push는 원본 배열을 직접 변경하고 변경된 배열의 length를 반환한다.
var c = a.push(b, true);
console.log(a); // a --> ['a', 'b', 'c', ['x', 'y', 'z'], true]
console.log(c); // c --> 5;

// concat은 원본 배열을 직접 변경하지 않고 복사본을 반환한다.
console.log([1, 2].concat([3, 4])); // [ 1, 2, 3, 4 ]

var arr = [1, 2, 3, 4, 5];

arr.push(6);
arr[arr.length] = 6; // 43% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1

arr.unshift(0);
[0].concat(arr); // 98% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
### 7. Array.prototype.reverse()
배열 요소의 순서를 반대로 변경
> 반환값은 배열이다. 

`원본배열이 변경된 배열이다.`

### 8. Array.prototype.shift()
push 와 함께 배열을 큐(FIFO) 처럼 동작하게 한다. `선입선출`
> 배열에서 첫 요소를 제거하고 제거한 요소를 반환

- 빈 배열일 경우
  - undefined를 반환
- Array.prototype.pop()
  - 마지막 요소를 제거하고 제거한 요소를 반환

```javascript
var a = ['a', 'b', 'c'];
var c = a.shift();

// 원본 배열이 변경된다.
console.log(a); // a --> [ 'b', 'c' ]
console.log(c); // c --> 'a'

var a = ['a', 'b', 'c'];
var c = a.pop();

// 원본 배열이 변경된다.
console.log(a); // a --> ['a', 'b']
console.log(c); // c --> 'c'
```

> pop은 마지막 요소를 제거하고 제거한 요소를 반환한다.
### 9. Array.prototype.slice(start,end)
배열의 특정부분에 대한 복사본을 생성

> 첫번째 매개변수 start에 해당하는 인덱스를 갖는 요소부터 end 에 해당하는 인덱스를 가진 요소전까지 복사

- 매개변수 
  - start : 음수인 경우 배열의 끝에서의 인덱스를 나타냄
    - ex) 배열의 마지막2개의 요소를 반환
  - end : 옵션이며 기본값 : length값이다.

```javascript
var items = ['a', 'b', 'c'];

// items[0]부터 items[1] 이전(items[1] 미포함)까지 반환
var res1 = items.slice(0, 1);
console.log(res1);  // [ 'a' ]

// items[1]부터 items[2] 이전(items[2] 미포함)까지 반환
var res2 = items.slice(1, 2);
console.log(res2);  // [ 'b' ]

// items[1]부터 이후의 모든 요소 반환
var res3 = items.slice(1);
console.log(res3);  // [ 'b', 'c' ]

// 인자가 음수인 경우 배열의 끝에서 2개의 요소를 반환
var res4 = items.slice(-2);
console.log(res4);  // [ 'b', 'c' ]

// 모든 요소를 반환
var res5 = items.slice();
console.log(res5);  // [ 'a', 'b', 'c' ]

// slice는 복사본을 반환한다. 원본은 변경되지 않는다.
console.log(items); // [ 'a', 'b', 'c' ]
```
> 배열엔 깊은 복사가 없다. 객체에서는 레스팅 되어있는 상황이 깊은 복사가 가능하다.
### 10. Array.prototype.splice(start, deleteCount, item..)
기존 배열의 내용을 추가 제거하고 새로운 항목으로 대체한다.

- 매개변수
  - start : 배열에서의 시작
  - deleteCount : start부터 제거할 요소의 수
  - item : 삭제한 위치에 추가될 요소들 (옵션)
- 반환값
  - 삭제한 요소들을 가진 배열

> 가장 일반적 사용 : 배열에서 요소를 삭제할 때

```javascript
var items = ['one', 'two', 'three', 'four'];

// items[1]부터 2개의 요소를 제거하고 제거된 요소를 배열로 반환
var res = items.splice(1, 2);

// 원본 배열이 변경된다.
console.log(items); // [ 'one', 'four' ]
// 제거한 요소가 배열로 반환된다.
console.log(res);   // [ 'two', 'three' ]
```
- 요소를 제거하고 제거한 위치에 다른 요소를 추가할 때
```javascript
var items = ['one', 'two', 'three', 'four'];

// items[1]부터 2개의 요소를 제거하고 그자리에 새로운 요소를 추가한다. 제거된 요소가 반환된다.
var res = items.splice(1, 2, 'x', 'y');

// 원본 배열이 변경된다.
console.log(items); // [ 'one', 'x', 'y', 'four' ]
// 제거한 요소가 배열로 반환된다.
console.log(res);   // [ 'two', 'three' ]
```
- 배열 중간에 새로운 요소를 추가할 때도 사용된다.
```javascript
var items = ['one', 'two', 'three', 'four'];

// items[1]부터 0개의 요소를 제거하고 그자리(items[1])에 새로운 요소를 추가한다. 제거된 요소가 반환된다.
var res = items.splice(1, 0, 'x');

// 원본 배열이 변경된다.
console.log(items); // [ 'one', 'x', 'two', 'three', 'four' ]
// 제거한 요소가 배열로 반환된다.
console.log(res);   // [ ]
```
- 배열중간에 새로운 배열을 추가할 때
```javascript
var items = ['one', 'four'];

// items[1]부터 0개의 요소를 제거하고 그자리(items[1])에 새로운 배열를 추가한다. 제거된 요소가 반환된다.
// var res = items.splice(1, 0, ['two', 'three']); // [ 'one', [ 'two', 'three' ], 'four' ]
var res = Array.prototype.splice.apply(items, [1, 0].concat(['two', 'three']));
// ES6
// var res = items.splice(1, 0, ...['two', 'three']);

console.log(items); // [ 'one', 'two', 'three', 'four' ]
console.log(res);   // [ ]
```
### 11. Array.prototype.sort(comparefunc)
배열의 내용을 적절하게 정렬
> 인자로 콜백함수를 주어야 한다.

> 인자가 없을 땐 오름차순으로 (알파벳순서)로 정렬한다.

```javascript
var fruits = ['Banana', 'Orange', 'Apple', 'Mango'];

// ascending(오름차순)
fruits.sort();
console.log(fruits); // [ 'Apple', 'Banana', 'Mango', 'Orange' ]

// descending(내림차순)
fruits.reverse();
console.log(fruits); // [ 'Orange', 'Mango', 'Banana', 'Apple' ]

var points = [40, 100, 1, 5, 25, 10];

points.sort();
console.log(points); // [ 1, 10, 100, 25, 40, 5 ]

// Syntax : array.sort(compareFunction)

// 숫자 배열 오름차순 정렬
// compareFunction의 반환값이 0보다 작은 경우, a를 우선한다.
points.sort(function (a, b) { return a - b; });
console.log(points); // [ 1, 5, 10, 25, 40, 100 ]

// 숫자 배열에서 최소값 취득
console.log(points[0]); // 1

// 숫자 배열 내림차순 정렬
// compareFunction의 반환값이 0보다 큰 경우, b를 우선한다.
points.sort(function (a, b) { return b - a; });
console.log(points); // [ 100, 40, 25, 10, 5, 1 ]

// 숫자 배열에서 최대값 취득
console.log(points[0]); // 100
```
### 12. Array.prototype.map()
배열을 순회하며 각 요소에 대해 인자로 주어진 콜백함수를 실행. 
> 결과가 반영된 새로운 배열을 반환

` 콜백함수의 인자로 요소값, 요소 인덱스, 순회할 배열을 전달할 수 있다.`

```javascript
var numbers = [1, 4, 9];
// 배열을 순회하며 각 요소에 대하여 인자로 주어진 콜백함수를 실행
var roots = numbers.map(Math.sqrt);
console.log(roots ); // [ 1, 2, 3 ]

function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  // 콜백함수의 인자로 요소값, 요소 인덱스, 순회할 배열을 전달할 수 있다.
  return arr.map(function (x) {
    // x는 요소값이다.
    // 3개 인자를 받을 수 있는데 이름은 상관없고 위는 요소값만 인자로 들어온 상태이다.
    return this.prefix + x; // 2번째 인자 this를 전달하지 않으면 this === window
  }, this);
};

var pre = new Prefixer('-webkit-');
var preArr = pre.prefixArray(['linear-gradient', 'border-radius']);
console.log(preArr);
// [ '-webkit-linear-gradient', '-webkit-border-radius' ]
```

> 첫번째 인자 : 콜백함수

> 두번째 인자 : this
### 13. Array.prototype.forEach()
배열을 순회하며 각 요소에 대해 인자로 주어진 콜백함수를 실행
` 콜백함수의 인자로 요소값, 요소 인덱스, 순회할 배열을 전달할 수 있다.`
> 일반 for문에 비해 성능이 좋지 않다.

>두 번째 인자로 this를 전달할 수 있다.

```javascript
var total = 0;

[1, 3, 5, 7, 9].forEach(function (element, index, array) {
  console.log('[' + index + '] = ' + element);
  total += element;
});

console.log(total);

function Counter() {
  this.sum = 0;
  this.count = 0;
}
Counter.prototype.add = function (array) {
  // entry는 array의 요소값
  array.forEach(function (entry) {
    this.sum += entry; // 2번째 인자 this를 전달하지 않으면 this === window
    this.count++;
  }, this);
};

var obj = new Counter();
obj.add([2, 5, 9]);
console.log(obj.count); // 3
console.log(obj.sum);   // 16
```
### 14. Array.prototype.filter()
배열을 순회하며 각요소에 대해 인자로 주어진 콜백함수의 실행결과가 true 인 요소값만을 모은 새로운 배열을 반환

> 배열에서 특정 케이스만 필터링조건으로 추출해 새로운 배열을 만들고 싶을 때 사용

` 콜백함수의 인자로 요소값, 요소 인덱스, 순회할 배열을 전달할 수 있다.`

```javascript
var result = [1, 2, 3, 4, 5].filter(function (element, index, array) {
  console.log('[' + index + '] = ' + element);
  return element % 2; // 홀수만을 필터링한다 (1은 true로 평가된다)
});

console.log(result);
```

> 두번째 인자로 this를 전달할 수 있다.
### 15. Array.prototype.reduce()
배열을 순회하며 각 요소에 대해 이전의 콜백함수 실행반환값을 전달해 콜백함수를 실행하고 그 결과를 반환

```javascript
/*
previousValue: 이전 콜백의 반환값
currentValue : 요소값
currentIndex : 인덱스
array        : 순회할 배열
*/
var result = [1, 2, 3, 4, 5].reduce(function(previousValue, currentValue, currentIndex, array) {
  console.log(previousValue + '+' + currentValue + '=' + (previousValue + currentValue));
  return previousValue + currentValue; // 결과는 다음 콜백의 첫번째 인자로 전달된다
});

console.log(result); // 15: 1~5까지의 합
/*
1: 1+2=3
2: 3+3=6
3: 6+4=10
4: 10+5=15
15
*/
```

### 16. Array.prototype.find()

>새로 도입된 메소드

배열을 순회하며 각 요소에 대해 인자로 주어진 콜백함수를 실행해 그 결과가 참인 첫번째 요소를 반환

> 콜백함수의 인자로 요소값,요소인덱스, 순회할 배열을 전달할 수 있다.