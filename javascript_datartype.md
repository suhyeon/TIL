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