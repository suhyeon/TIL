# JAVASCRIPT - OBJECT
## 1. 객체란?

객체 기반의 스크립트언어. 거의 모든 것은 객체이다.  

` 데이터를 한곳에 모으고 구조화 하는데 유용하다.`

### 1. 프로퍼티
객체는 이름과 값의 쌍인 프로피티들을 포함하는 컨테이너라고 할 수 있다. 
> 프로퍼티는 프로퍼티 이름과 프로퍼티 값으로 구성된다.
- 프로퍼티 이름 : 빈 문자열을 포함하는 문자열과 숫자
- 프로퍼티 값 : undefined 를 제외한 모든 값
> undefined를 값으로 매기는 건 아예 안만드는 것과 같다

### 2. 메서드

#### 1. 객체 리터럴로 객체생성
가장 일반적인 간편한 자바스크립트의 객체 생성방식

`프로퍼티 이름 : 프로퍼티값`

```
var emptyObject = {};
console.log(typeof emptyObject); // object

var person = {
  name: 'Lee',
  gender: 'male',
  sayHello: function () {
    console.log('Hi! My name is ' + this.name);
  }
};

console.log(typeof person); // object
console.log(person); // { name: 'Lee', gender: 'male', sayHello: [Function: sayHello] }

person.sayHello(); // Hi! My name is Lee
```

#### 2. Object()생성자 함수로 객체 생성하기
new 연산자와 object()생성자 함수를 사용해 빈 객체를 생성한다.
빈 객체 생성이후 프로퍼티와 메서드를 추가해 객체를 완성하는 방법

```
// 빈 객체의 생성
var person = new Object();
// 프로퍼티 추가
person.name = 'Lee';
person.gender = 'male';
person.sayHello = function () {
  console.log('Hi! My name is ' + this.name);
};

console.log(typeof person); // object
console.log(person); // { name: 'Lee', gender: 'male', sayHello: [Function] }

person.sayHello(); // Hi! My name is Lee
```

`객체를 생성하는 방법은 객체 리터럴을 사용하는 게 더 편하다.`

> 객체 리터럴 방식으로 생성된 객체는 결국 내장(Built-in) 함수인 Object() 생성자 함수로 객체를 생성하는 것을 단순화 시킨 short-hand(축약법)이다. 

#### 3. 생성자 함수로 객체 생성하기
```
// 생성자 함수
function Person(name, gender) {
  this.name = name;
  this.gender = gender;
  this.sayHello = function(){
    console.log('Hi! My name is ' + this.name);
  };
}

// 인스턴스의 생성
var person1 = new Person('Lee', 'male');
var person2 = new Person('Kim', 'female');

console.log('person1: ', typeof person1);
console.log('person2: ', typeof person2);
console.log('person1: ', person1);
console.log('person2: ', person2);

person1.sayHello();
person2.sayHello();
```

- 생성자 함수 이름은 일반적으로 대문자로 시작.
    - 생성자 함수임을 인식하도록 도움을 준다
- 프로퍼티 또는 메소드명 앞에 기술한 this는 생성자 함수로 생성될 인스턴스를 가리킨다.
    - this에 연결되어 있는 프로퍼티와 메서드는 public이다.
- 생성자 함수내에서 선언된 일반 변수는 private이다.
    - 생성자 함수 내부에서는 자유롭게 접근이 가능하지만 외부에서 접근할 방법이 없다.

### 3. 객체 프로퍼티 접근

#### 1. 프로퍼티 이름
프로퍼티 이름에 따옴표는 자바스크립트에서 사용할 수 있는 유효한 이름이고 예약어가 아닌 경우 생략할 수 있다.

> 프로퍼티 값은 undefined를 제외한 모든 값과 표현식이 올수 있으며 프로퍼티 값이 함수인 경우 : 메서드

` last-name : 이건 안된다. 연산자이기 때문, 그렇기에 네이밍을 할 때 underscore를 사용하는 snake 케이스나 camel케이스를 사용해라!`

> 예약어 사용도 금물!
```
abstract	arguments	boolean	break	byte
case  catch	char	class*	const
continue	debugger	default	delete	do
double	else	enum*	eval	export*
extends*	false	final	finally	float
for	function	goto	if	implements
import*	in	instanceof	int	interface
let	long	native	new	null
package	private	protected	public	return
short	static	super*	switch	synchronized
this	throw	throws	transient	true
try	typeof	var	void	volatile
while	with	yield
// *는 ES6에서 추가된 예약어
```

#### 2. 프로퍼티 값 읽기
객체의 프로퍼티에 접근하는 방법

- 마침표(.) 표기법
- 대괄호([]) 표기법

```
var person = {
  'first-name': 'Ung-mo',
  'last-name': 'Lee',
  gender: 'male',
};

console.log(person);

console.log(person.first-name);    // NaN: undefined-name
console.log(person[first-name]);   // ReferenceError: first is not defined
console.log(person['first-name']); // 'Ung-mo'

console.log(person.gender);    // 'male'
console.log(person[gender]);   // ReferenceError: gender is not defined
console.log(person['gender']); // 'male'
```

`대괄호 내에 들어가는 프로퍼티 이름은 반드시 문자열이어야 한다.`

>객체에 존재하지 않는 프로퍼티를 참조하면 undefined를 반환한다.

#### 3. 프로퍼티 값 갱신
객체가 소유하고 있는 프로퍼티에 새로운 값을 할당하면 프로퍼티 값은 갱신된다.
```
var person = {
  'first-name': 'Ung-mo',
  'last-name': 'Lee',
  gender: 'male',
};

person['first-name'] = 'Kim';
console.log(person['first-name'] ); // 'Kim'
```

#### 4. 프로퍼티 동적 생성
객체가 소유하고 있지 않은 프로퍼티에 값을 할당하면 해당 프로퍼티를 객체에 추가하고 값을 할당한다.

```
var person = {
  'first-name': 'Ung-mo',
  'last-name': 'Lee',
  gender: 'male',
};

person.age = 20;
console.log(person.age); // 20
```

#### 5. 프로퍼티 삭제
delete 연산자를 사용하면 객체의 프로퍼티를 삭제할 수 있다.

```
var person = {
  'first-name': 'Ung-mo',
  'last-name': 'Lee',
  gender: 'male',
};

delete person.gender;
console.log(person.gender); // undefined

delete person;
console.log(person); // Object {first-name: 'Ung-mo', last-name: 'Lee'}
```

#### 6. for-in 문
객체에 포함된 모든 프로퍼티에 대해 루프를 수행할 수 있다.

```
var person = {
  'first-name': 'Ung-mo',
  'last-name': 'Lee',
  gender: 'male'
};

for(var prop in person) {
  console.log(prop + ': ' + person[prop]);
}
```
`이것은 쓰지 말아라! ES6에 새로 추가된 for-of을 사용하라`

### 4. Pass-by-reference
참조형 : 객체의 모든 연산이 실제값이 아닌 참조값으로 처리됨을 의미
