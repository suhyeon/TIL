# JAVASCRIPT - OBJECT ORIENTED PROGRAMMING

## 1. 객체지향 프로그래밍 개요
> this는 method, 생성자함수에서만 사용하는 것이 좋다.

데이터는 멤버변수다 라고도 부른다.

사물의 특성을 분석,분해하고 인지할 필요가 있다.

> 어떠한 행위나 행동을 하는 것을 메소드라고 일컫기도 한다.

추상화 : 핵심적인 개념 또는 기능만을 추출 (중요한 특성들만 집어낸다.)  
상속 : 어떠한 중복되는 속성을 포괄적으로 개념을 정의해 하부에게 내리사용할 수 있는 특성,데이터 구조  
캡슐화, 정보은닉 : 비공개를 할 정보를 감춘다.

## 2. 클래스 기반 vs 프로토타입 기반

### 1. 클래스 기반언어
클래스로 객체의 자료구조와 기능을 정의하고 생성자를 통해 인스턴스를 생성한다.

> 클래스 : 같은 종류의 집단에 속하는 속성과 행위를 정의한 것으로 객체지향프로그램의 기본적인 사용자 정의 데이터형이라고 할 수 있다.

`모든 인스턴스는 오직 클래스에서 정의된 범위내에서만 작동하고 런타임에 그 구조를 변경할 수 없다.`

```java
class Person {
  private String name;

  public Person(String name) {
    this.name = name;
  }

  public void setName(String name) {
    this.name = name;
  }

  public String getName() {
    return this.name;
  }

  public static void main(String[] args) {
    Person me = new Person("Lee");

    String name= me.getName();
    System.out.println(name); // Lee
  }
}
```

>ES6로 작성한 후 바벨을 사용해서 ES5로 컴파일을 해서 사용하면 훨씬 나은 프로그래밍이 될 수 있다.

### 2. 프로토타입 기반 언언
javascript : 멀티 패러다임 언어, 명령형, 함수형, 절차적, 프로토타입 기반 객체지향 언어

> 클래스라는 개념이 없다.

객체 생성방법
- 객체리터럴
- object()생성자 함수
- 생성자함수

```javascript
// 객체 리터럴
var obj1 = {};
obj1.name = 'Lee';

// Object() 생성자 함수
var obj2 = new Object();
obj2.name = 'Lee';

// 생성자 함수
function F() {}
var obj3 = new F();
obj3.name = 'Lee';
```

## 3. 생성자 함수와 인스턴스의 생성
생성자 함수와 new 연산자를 통해 인스턴스를 생성할 수 있다.
>생성자 함수는 클래스이자 생성자의 역할을 한다.

```javascript
// 생성자 함수(Constructor)
function Person(name) {
  // 프로퍼티
  this.name = name;

  // 메소드
  this.setName = function (name) {
    this.name = name;
  };

  // 메소드
  this.getName = function () {
    return this.name;
  };
}

// 인스턴스의 생성
var me = new Person('Lee');
console.log(me.getName()); // Lee

// 메소드 호출
me.setName('Kim');
console.log(me.getName()); // Kim
```

> 메소드를 빼내어서 프로토타입에 위치해야 한다.

## 4. 프로토타입 체인과 메소드의 정의

중복을 제거하기 위해 유용하다.

```javascript
function Person(name) {
  this.name = name;
}

// 프로토타입 객체에 메소드 정의
Person.prototype.setName = function (name) {
  this.name = name;
};

// 프로토타입 객체에 메소드 정의
Person.prototype.getName = function () {
  return this.name;
};

var me  = new Person('Lee');
var you = new Person('Kim');
var him = new Person('choi');

console.log(Person.prototype); 
// Person { setName: [Function], getName: [Function] }

console.log(me);  // Person { name: 'Lee' }
console.log(you); // Person { name: 'Kim' }
console.log(him); // Person { name: 'choi' }
```

> 더글라스 크락포드가 제안한 프로토타입 객체에 메소드를 추가하는 방식
```javascript
/**
 * 모든 생성자 함수의 프로토타입은 Function.prototype이다. 따라서 모든 생성자 함수는 Function.prototype.method()에 접근할 수 있다.
 * @method Function.prototype.method
 * @param ({string}) (name) - (메소드 이름)
 * @param ({function}) (func) - (추가할 메소드 본체)
 */
Function.prototype.method = function (name, func) {
  // 생성자함수의 프로토타입에 동일한 이름의 메소드가 없으면 생성자함수의 프로토타입에 메소드를 추가
  // this: 생성자함수
  if (!this.prototype[name]) {
    this.prototype[name] = func;
  }
};

/**
 * 생성자 함수
 */
function Person(name) {
  this.name = name;
}

/**
 * 생성자함수 Person의 프로토타입에 메소드 setName을 추가
 */
Person.method('setName', function (name) {
  this.name = name;
});

/**
 * 생성자함수 Person의 프로토타입에 메소드 getName을 추가
 */
Person.method('getName', function () {
  return this.name;
});

var me  = new Person('Lee');
var you = new Person('Kim');
var him = new Person('choi');

console.log(Person.prototype);
// Person { setName: [Function], getName: [Function] }

console.log(me);  // Person { name: 'Lee' }
console.log(you); // Person { name: 'Kim' }
console.log(him); // Person { name: 'choi' }
```

## 5. 상속
코드 재사용의 관점에서 매우 유용하다.

### 1. 의사 클래스 패턴 상속 (pseudo-classical inheritance)
자식 생성자 함수의 prototype 프로퍼티를 부모 생성자 함수의 인스턴스로 교체해 상속을 구현하는 방법.

> 부모와 자식 모두 생성자 함수를 정의해야한다.
`문제점이 있기에 이러한 패턴은 사용하면 안된다.`

`즉시실행함수를 보면 return을 어떤것을 하는지 보아라!`

- 부작용
  - 자식이 constructor를 찾으면 다른 constructor가 나온다.(constructor의 링크가 깨진다.)
  - new를 사용해줘야만 한다.
  - 객체리터럴로 객체를 만들 수 없다.
      - 기본적으로 생성자함수를 사용하기 때문에 객체리터럴로 생성한 객체 생성자함수는 object()를 변경할 방법이 없다.

```javascript
// 부모 생성자 함수
var Parent = (function () {
  // Constructor
  function Parent(name) {
    this.name = name;
  }

  // method
  Parent.prototype.sayHi = function () {
    console.log('Hi! ' + this.name);
  };

  // return constructor
  return Parent;
}());

// 자식 생성자 함수
var Child = (function () {
  // Constructor
  function Child(name) {
    this.name = name;
  }

  // 자식 생성자 함수의 프로토타입 객체를 부모 생성자 함수의 인스턴스로 교체.
  Child.prototype = new Parent(); // ②

  // 메소드 오버라이드
  Child.prototype.sayHi = function () {
    console.log('안녕하세요! ' + this.name);
  };

  // sayBye 메소드는 Parent 생성자함수의 인스턴스에 위치된다
  Child.prototype.sayBye = function () {
    console.log('안녕히가세요! ' + this.name);
  };

  // return constructor
  return Child;
}());

var child = new Child('child'); // ①
console.log(child);  // Parent { name: 'child' }

console.log(Child.prototype); // Parent { name: undefined, sayHi: [Function], sayBye: [Function] }

child.sayHi();  // 안녕하세요! child
child.sayBye(); // 안녕히가세요! child

console.log(child instanceof Parent); // true
console.log(child instanceof Child);  // true
```

### 2. 프로토타입 패턴 상속

object.create 함수를 사용해 객체에서 다른 객체로 직접 상속을 구현하는 방식

[object.create 함수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/create)

> 개념적으로 의사 클래스 패턴 상속보다 더 간단하다.

```javascript
// 부모 생성자 함수
var Parent = (function () {
  // Constructor
  function Parent(name) {
    this.name = name;
  }

  // method
  Parent.prototype.sayHi = function () {
    console.log('Hi! ' + this.name);
  };

  // return constructor
  return Parent;
}());

// create 함수의 인수는 프로토타입이다. 
var child = Object.create(Parent.prototype);
child.name = 'child';

child.sayHi();  // Hi! child

console.log(child instanceof Parent); // true
```

객체 리터럴으로 생성한 객체에도 프로토타입 패턴상속이가능하다.
```javascript
var parent = {
  name: 'parent',
  sayHi: function() {
    console.log('Hi! ' + this.name);
  }
};

// create 함수의 인자는 객체이다. 
var child = Object.create(parent);
child.name = 'child';

// var child = Object.create(parent, {name: {value: 'child'}});

parent.sayHi(); // Hi! parent
child.sayHi();  // Hi! child

console.log(parent.isPrototypeOf(child)); // true
```

>IE9이상에서만 돌아간다.
`폴리필(polyfill) : 특정기능이 지원되지 않는 브라우저를 위해 사용할 수 있는 코드조각 이나 플러그인`

```javascript
// Object.create 함수의 폴리필
if (!Object.create) {
  Object.create = function (o) {
    function F() {}  // 1
    F.prototype = o; // 2
    return new F();  // 3
  };
}
```

- 1. 비어있는 생성자 함수 f를 생성한다.
- 2. 생성자 함수 F의 prototype 프로퍼티에 매개변수로 전달받은 객체를 할당한다.
- 3. 생성자 함수 F를 생성자로 하여 새로운 객체를 생성하고 반환한다.
>프로토타입 패턴 상속의 핵심을 담고있다.

## 6. 캡슐화와 모듈 패턴
`캡슐화 (정보 은닉)` : 관련있는 멤버 변수와 메소드를 클래스와 같은 하나의 틀안에 담고 외부에 공개될 필요가 없는 정보는 숨기는 것

> java의 경우, private으로 선언된 것들

자바스크립트에서는 public이나 private 키워드를 제공하지 않는다.  

```javascript
var Person = function(arg) { // Person 프로퍼티 = public
  var name = arg ? arg : ''; // ①

  this.getName = function() {
    return name;
  };

  this.setName = function(arg) {
    name = arg;
  };
}

var me = new Person('Lee');

var name = me.getName();

console.log(name);

me.setName('Kim');
name = me.getName();

console.log(name);
```
> this 는 기본이 public 처럼 사용되지만, var로 묶이면 private 처럼 사용된다.

```javascript
var person = function(arg) {
  var name = arg ? arg : ''; //결국 closure

  return {  //객체 리터럴을 반환
    getName: function() { // 두개다 함수
      return name;
    },
    setName: function(arg) {
      name = arg;
    } // 내부함수가 외부함수보다 오래 살아남는다.
  }
}

var me = person('Lee'); /* or var me = new person('Lee'); */

var name = me.getName();

console.log(name);

me.setName('Kim');
name = me.getName();

console.log(name);
```
위와 같은 방식이 모듈 패턴이라 한다.  
`주의 할 점`
- private 멤버가 객체나 배열일 경우, 반환된 해당 멤버의 변경이 가능하다. (객체는 참조형이기 때문에, 외부에서 수정하면 본래의 값도 수정된다.)
- person 함수가 반환한 객체는 person 함수 객체의 프로토타입에 접근할 수 없다. 이는 상속을 구현할 수 없음을 의미한다.
- 객체를 반환하는 것이 아니라 함수를 반환해야 한다.

```javascript
var person = function (personInfo) { 
  var o = personInfo;

  return { //본래의 의도는 참조하기만을 바랐다.
    getPersonInfo: function() {
      return o; //이 아이를 그대로 주지말고, copy해서 보낸다.(object.assign, json )
    }
  };
};

var me = person({ name: 'Lee', gender: 'male' });

var myInfo = me.getPersonInfo();
console.log('myInfo: ', myInfo);
// myInfo:  { name: 'Lee', gender: 'male' }

myInfo.name = 'Kim';

myInfo = me.getPersonInfo();
console.log('myInfo: ', myInfo);
// myInfo:  { name: 'Kim', gender: 'male' }
```

- 함수를 반환하는 방법
```javascript
var Person = function() { //기본적인 모듈패턴의 모습
  var name;

  var F = function(arg) { name = arg ? arg : ''; };

  F.prototype = {
    getName: function() {
      return name;
    },
    setName: function(arg) {
      name = arg;
    }
  };

  return F;
}();

var me = new Person('Lee');

console.log(Person.prototype === me.__proto__);

console.log(me.getName());
me.setName('Kim')
console.log(me.getName());
```