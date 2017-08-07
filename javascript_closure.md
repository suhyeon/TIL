# JAVASCRIPT - CLOSURE

## 1. 클로져의 개념

클로저 : 내부함수를 위한 외부함수의 지역변수가 외부함수에 의해 내부함수가 반환된 이후에도 LIFE-CYCLE이 유지되는 것을 의미

> 함수를 일급객체로 취급하는 함수형 언어에서 사용되는 중요한 특성

내부함수를 포함하는 형상
```javascript
function outerFunc() {
  var x = 10;
  var innerFunc = function () { console.log(x); };
  innerFunc();
}

outerFunc();
```

- innerFunc 함수내에서 변수x를 검색한다. 검색이 실패
- innerFunc 함수를 포함하는 외부 함수 outerFunc 에서 변수 x를 검색. 검색이 성공

내부함수를 리턴하는 예제
```javascript
function outerFunc() {
  var x = 10;
  var innerFunc = function () { console.log(x); };
  return innerFunc;
}

var inner = outerFunc(); // 클로저의 형성
inner(); // 10
```

클로저 : 외부함수는 외부함수의 지역변수를 사용하는 내부함수가 소멸될때까지 소멸되지 못하고 상태가 유지되며 내부함수에 의해서 소멸하게 되는 특성

> 클로저에 의해 참조되는 외부함수의 변수 : 자유변수

`클로저라는 이름은 자유변수에 함수가 닫혀있다는 의미로 의역하면 자유변수에 엮여있는 함수라는 뜻이다.`

## 실행컨텍스트의 관점
내부함수가 유효한 상태에서 외부함수가 종료해 외부함수의 실행 컨텍스트가 반환되어도 외부함수 실행컨텍스트 내의 AO는 유효해 내부함수가 SCOPE CHAIN을 통해 참조할 수 있는 것을 의미한다.

> 외부함수가 이미 반환되었어도 외부함수 내의 변수는 이를필요로 하는 내부함수가 하나 이상 존재하는 경우 계속 유지된다.

`외부함수가 종료하면 외부함수의 실행컨텍스트도 소멸되지만 함수 실행컨텍스트 AO는 유효하다.`

## 2. 클로저의 활용
자바의 강력한 기능이기는 하나 성능적인 면과 자원적인 면에서 손해를 볼 수 있다.

> 무분별한 클로저의 사용은 득보다는 실이 많다.

### 1. 전역 변수의 사용 억제
즉시실행함수는 한번만 실행되므로 함수가 호출 될때 마다 변수가 재차 초기화 될일이 없다. 

### 2. setTimeout()의 콜백 함수

이함수는 첫째 파라미터에 콜백함수를 전달하고, 두번째 파라미터에 시간 간경을 지정한다. 

> 지정된 시간간격으로 콜백함수를 호출한다.

```javascript
<!DOCTYPE html>
<html>
<body>
  <p>새로고침으로 다시 실행해 보세요</p>
  <script>
    var fade = function (node) {
      // 자유변수
      var level = 1; // ②
      var step = function() {
        var hex = level.toString(16); // ④
        
        // hex: '1' ~ 'f'
        node.style.backgroundColor = '#ff' + hex; // ⑤

        if(level < 15) { // ⑥
          level += 1;
          setTimeout(step, 100); // ⑦
        }
      };
      // setTimeout 호출 이후 fade 함수는 종료한다. 100ms 후 함수 step은 호출된다.
      // 즉 외부 함수 fade보다 내부 함수 step이 더 오래 유지된다.
      setTimeout(step, 100); // ③
    };

    fade(document.body); // ①
  </script>
</body>
</html>
```

- ① 함수 fade는 document.body를 인자로 전달받아 호출된다.
- ② 함수 fade의 지역변수 level은 1로 초기화되어 있다. 함수 step은 내부함수이며 외부함수 fade의 지역변수 level을 사용한다. level은 자유변수이다.
- ③ setTimeout 호출 이후 fade 함수는 종료한다. 100ms 후 함수 step은 호출된다. 즉 외부 함수 fade보다 내부 함수 step이 더 오래 유지된다.
- ④ 함수 step은 지역변수 hex을 갖는다. 이것은 16진수 문자열을 값으로 갖는다. 
- ⑤ 함수 fade의 매개변수 node(document.body)의 배경색을 변경한다.
- ⑥ 변수 level이 15(f)보다 작은지 다시말해 16진수 범위 내(1~f)인지 확인한다.
- ⑦ level을 1 증가시키고 다시 함수 step을 호출하여 같은 작업을 반복한다.

함수는 이미 반환되었지만, 외부함수 내의 변수는 이를 필요로 하는 내부함수가 하나 이상 존재하는 경우 계속 유지된다. 내부함수가 외부함수에 있는 변수의 복사본이 아니라 실제 변수에 접근한다는 것에 주의해야한다.

## 3. 자주 발생하는 실수 예제
실수 사례1
```javascript
var arr = [];

for (var i = 0; i < 5; i++) {
  arr[i] = function () {   //i는 전역변수
    return i;
  };
}

for (var index = 0; index < arr.length; index++) {
  console.log(arr[index]());
}
```

변경 사례
```javascript
var arr = [];

for (var i = 0; i < 5; i++){
  arr[i] = (function (id) { // ②
    return function () {
      return id; // ③
    };
  })(i); // ①
}

for (var index = 0; index < arr.length; index++) {
  console.log(arr[index]());
}
```

- ① 배열 arr에는 즉시실행함수에 의해 함수가 반환된다.
- ② 이때 즉시실행함수는 i를 인자로 전달받고 매개변수 id에 할당한 후 내부 함수를 반환하고 life-cycle이 종료된다. 매개변수 id는 자유변수가 된다.
- ③ 배열 arr에 할당된 함수는 id를 반환한다. 이때 id는 상위 스코프의 자유변수이므로 그 값이 유지된다.