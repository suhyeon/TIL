# ECMA SCRIPT 6 - ITERATION PROTOCOL & FOR-OF
## 1. 이터레이션 프로토콜 
- 이터러블 
  - 순회 가능한 자료구조
  - Symbol.iterator를 프로퍼티 key로 사용한 메소드를 구현
- 이터레이터
  - Symbol.iterator를 프로퍼티 key로 사용한 메소드는 이터레이터를 반환
  - 순회 가능한 자료구조인 이터러블의 요소를 탐색하기 위한 포인터
  - next()메소드를 갖는 객체
  - next() : value, done 프로퍼티를 갖는 객체를 반환
  - 이 메소드를 통해 이터러블 객체를 순회할 수 있다.
value : 순회할 자료  
done : 끝까지 순회하면 true, 아직 남았다면 false
- Array
- String
- Map
- Set
- DOM DATA STRUCTURE
> 이터레이션 프로토콜은 이터레이터의 NEXT()메소드를 통해 다양한 데이터 소스에 순차적으로 접근할 수 있는 일관된 방법을 제시
```javascript
// 이터러블
// Symbol.iterator를 프로퍼티 key로 사용한 메소드를 구현하여야 한다.
// 배열에는 Array.prototype[Symbol.iterator] 메소드가 구현되어 있다.
const iterable = ['a', 'b', 'c'];

// 이터레이터
// 이터러블의 Symbol.iterator를 프로퍼티 key로 사용한 메소드는 이터레이터를 반환한다. 
const iterator = iterable[Symbol.iterator]();

// 이터레이터는 순회 가능한 자료 구조인 이터러블의 요소를 탐색하기 위한 포인터로서 value, done 프로퍼티를 갖는 객체를 반환하는 next() 함수를 메소드로 갖는 객체이다. 이터레이터의 next() 메소드를 통해 이터러블 객체를 순회할 수 있다.
console.log(iterator.next()); // { value: 'a', done: false }
console.log(iterator.next()); // { value: 'b', done: false }
console.log(iterator.next()); // { value: 'c', done: false }
console.log(iterator.next()); // { value: undefined, done: true }

// 이터러블
const iterable = ['a', 'b', 'c'];

// 이터레이터
const iterator = iterable[Symbol.iterator]();

// 이터레이터의 next() 메소드를 통해 이터러블 객체를 순회
for (;;) {
  const res = iterator.next();
  console.log(res);
  if (res.done) break;
}
```
## 2. for-of 루프
이터러블 객체를 순회한다.
> for-of루프는 이터레이터의 next메소드를 호출하고 next메소드가 반환하는 객체의 done프로퍼티가 true가 될때까지 루핑한다.
```javascript
// 배열
for (const val of ['a', 'b', 'c']) {
  console.log(val);
}

// 문자열
for (const val of 'abc') {
  console.log(val);
}

// Map
//디스트럭처링
for (const [key, value] of new Map([['a', '1'], ['b', '2'], ['c', '3']])) {
  console.log(`key : ${key} value : ${value}`); // key : a value : 1 ...
}

// Set
for (const val of new Set([1, 2, 3])) {
  console.log(val);
}
```
FIBONACCI
```javascript
const fibonacci = {
  [Symbol.iterator]() {
    let [prev, curr] = [0, 1];
    // 순회 카운터
    let step = 0;
    // 최대 순회수
    const maxStep = 10;
    return {
      // fibonacci 객체가 순회할 때마다 next 함수가 호출된다.
      next() {
        [prev, curr] = [curr, prev + curr];
        return { value: curr, done: step++ >= maxStep };
      }
    };
  }
};

for (const num of fibonacci) {
  console.log(num);
}

// spread 연산자
const arr = [...fibonacci];
console.log(arr); // [ 1, 2, 3, 5, 8, 13, 21, 34, 55, 89 ]

// 디스트럭처링
const [first, second, ...rest] = fibonacci;
console.log(first, second, rest); // 1 2 [ 3, 5, 8, 13, 21, 34, 55, 89 ]
```