# CSS - EFFECT

## 1. 벤더 프리픽스 (Vendor Prefix)
요소를 사용하려 할 때 요소 앞머리에 브라우저마다 정해진 접두사를 붙이는 것

실험적으로 제공하는 기능을 사용하기 위해서 사용한다.

ex)  
```
* {
  -webkit-user-select: none;  /* Chrome all / Safari all */
  -moz-user-select: none;     /* Firefox all */
  -ms-user-select: none;      /* IE 10+ */
  user-select: none;          /* Likely future */
} 
//-webkit-, -moz-, -ms- : 벤더 프리픽스
```
## 2. 그림자 (Shadow)
  텍스트나 요소에 그림자 효과를 부여하기 위한 프로퍼티를 선언한다.
---
### 1. text - shadow
텍스트에 그림자 효과를 부여하는 프로퍼티

```
선택자 { text-shadow: Horizontal-offset Vertical-offset Blur-Radius Shadow-Color; }
```
- horizontal-offset
    - 그림자를 텍스트의 오른쪽으로 지정값만큼 이동(px)
- vertical-offset
    - 그림자를 텍스트의 아래로 지정값만큼 이동(px)
- blur-radius
    - 그림자의 흐림정도를 지정(px)
- shadow-color
    - 그림자의 색상을 지정(color)

### 2. box - shadow
요소에 그림자 효과를 부여하는 프로퍼티
```
선택자 { box-shadow: Inset Horizontal-offset Vertical-offset Blur-Radius Spread Shadow-Color; }
```
- inset
    - 그림자가 요소안쪽에 위치(inset)
- horizontal-offset
    - 그림자를 텍스트의 오른쪽으로 지정값만큼 이동(px)
- vertical-offset
    - 그림자를 텍스트의 아래로 지정값만큼 이동(px)
- blur-radius
    - 그림자의 흐림정도를 지정(px)
- spread
    - 그림자를 더크게 확장(px)
- shadow-color
    - 그림자의 색상을 지정(color)

## 3. 그레디언트 (Gradient)
2가지 이상의 색상을 혼합해 부드러운 색감의 배경을 생성
- 선형 그레디언트
- 방사형 그레디언트

[그레디언트 툴](http://www.colorzilla.com/gradient-editor/)

## 4. 트렌지션 (Transition)
css 프로퍼티 변경에 따른 표시의 변화를 부드럽게 하기 위해 에니메이션 속도를 조절

```
    div{      /* 트랜지션 효과: 모든 프로퍼티의 변화를 2초에 걸쳐 전환한다. */
      transition: all 2s;}
```
> div:hover 에 설정하면 hover off에는 발생하지 않는다.

- transition-property
        - 트랜지션의 대상이 되는 css 프로퍼티를 지정(all)
- transition-duration
        - 트랜지션이 일어나는 지속시간을 초단위로 지정(0s)
- transition-timing-function
        - 트렌지션 효과를 위한 수치 함수를 지정(ease)
- transition-delay
        - 프로퍼티가 변화한 시점과 트렌지션이 실제로 시작하는 사이에 대기하는 시간(0s)
- transition
        - 모든 트렌지션 프로퍼티를 한번에 지정

> 가상클래스 선택자 또는 javascript onclick 이벤트를 사용해야 발동한다.
---
### 1. transition-property
- transition-property 프로퍼티는 트렌지션의 대상이 되는 css 프로퍼티명을 지정
- 여러개를 지정할 땐 , 로 연결한다.
- transition-duration은 반드시 지정
- display property는 변경할 수 없다.
- layout에 영향을 주는 트랜지션 효과는 회피하기 위한 노력이 필요하다.

layout에 영향을 주는 프로퍼티
```
width height padding margin border
display position float overflow
top left right bottom
font-size font-family font-weight
text-align vertical-align line-height
clear white-space
```

### 2. transition-duration
트렌지션에 일어나는 지속시간을 초단위로 지정

`프로퍼티값을 지정하지 않으면 기본값 0초가 적용되어 어떠한 트랜지션 효과도 볼수 없다.`

### 3. transition-timing-function
트렌지션 효과의 변화흐름, 시간에 따른 변화 속도와 같은 일종의 변화의 리듬을 지정
> 기본값 : ease

### 4. transition-delay
변화한 시점과 트랜지션이 실제로 시작하는 사이에 대기하는 시간을 초단위로 지정

### 5. transition
모든 트렌지션 프로퍼티를 한번에 지정할 수 있는 shorthand 이다.

`지정방법`
```
transition: property duration function delay
```

> transition은 자동 발생하지 않는다.  
즉, transition-duration은 반드시 지정해야 한다.

`기본값(transition-duration)`
```
all 0 ease 0
```
  [코드펜 참조](https://codepen.io/)  
 
## 5. 애니메이션
html 요소에 적용되는 css 스타일을 다른  css 스타일로 부드럽게 변화시킨다.

> css 스타일과 애니메이션의 시퀀스를 나타내는 복수의 키프레임들로 이루어진다.(@keyframs)

- transition 프로퍼티
    - 단순히 요소의 프로퍼티 변화에 주안
- animation 프로퍼티
    - 하나의 줄거리를 구성해 줄거리 내에서 세부 움직임을 시간 흐름단위로 제어할 수 있고, 전체 줄거리의 재생과 정지, 반복까지 제어할 수 있다.

`장단점 특징`
- css를 사용할 때:
    - 비교적 작은 효과나 css만으로도 충분한 효과를 볼 수 있는 것 ex) 요소의 width변경 애니메이션
- javascript를 사용할 때:
    - 세밀한 제어가 필요할 때 ex) 바운스, 중지, 일시중지, 되감기, 감속, 고급효과

`브라우저에서 애니매이션 효과가 부드럽게 실행되는 것이 제일 중요하다.`

---
### 1. @keyframes
애니메이션의 흐름중의 여러시점에서 css 프로퍼티값을 지정할 수 있다. 구간과 같다.

>@keyframes rule 은 시간의 흐름에 따라 애니메이션을 정의한다.

`from, to 키워드를 이용해서 정의해도 되고, %를 사용할 수 있다.`

```
@keyframes move {
  /* 애니메이션 시작 시점 */
  from { left: 0; }
  /* 애니메이션 종료 시점 */
  to   { left: 300px; }
}
@keyframes move {
  0%   { left: 0; }
  50%  { left: 100px; }
  100% { left: 300px; }
}
```
### 2. animation-name
애니메이션을 대표하는 임의의 이름을 부여한다.

```
     animation-name: move, fadeOut, changeColor;
```

### 3. animation-duration
한 싸이클의 애니메이션의 소요되는 시간을 초 단위로 지정
```
animation-duration: 5s;
```

### 4. animation-timing-function
애니메이션 효과를 위한 수치함수를 지정

>수치함수 설명은 트렌지션 transition-timing-function 을 참조

### 5. animation-delay
요소가 로드된 시점과 애니메이션이 실제로 시작하는 사이에 대기하는 시간을 초단위로 지정
```
animation-delay: 2s;
```

### 6. animation-iteration-count
애니메이션 주기의 재생횟수를 지정
> 기본값은 1, 무한반복할 수 있다.

```
animation-iteration-count: 3;
```

### 7. animation-direction
애니메이션이 종료된후 반복될 때 진행하는 방향을 지정

- normal 
    - 기본값으로 from에서 to 방향으로 진행
- reverse
    - to에서 from 방향으로 진행
- alternate
    - 홀수 번째: normal, 짝수번째 : reverse로 진행
- alternate-reverse
    - 홀수번째 : reverse, 짝수번째 : normal 로 진행

### 8. animation-fill-mode
애니메이션 미실행 시 (대기 또는 종료) 요소의 스타일을 지정

[5.8 참조](http://poiemaweb.com/css3-effect)

### 9. animation-play-state
애니메이션 재생 상태를 지정
기본값은 running이다.

### 10. animation
모든 애니메이션 프로퍼티를 한번에 지정한다.  
값을 지정하지 않은 프로퍼티엔 기본값이 지정된다.

```
animation: name duration timing-function delay iteration-count direction fill-mode play-state
```
>animation-duration은 반드시 지정해야한다. name도 마찬가지이다.

`기본값`
```
none 0 ease 0 1 normal none running
```

## 6. 트랜스폼 (Transform)
요소에 이동, 회전, 확대축소, 비틀기 효과를 부여하기 위한 함수를 제공한다.
> 단, 애니메이션 효과를 제공하지는 않기 때문에 정의된 프로퍼티가 바로 적용되어 화면에 표시된다.
---
### 1. 2D 트랜스폼 (2D Transform)
프로퍼티값으로 변환함수를 사용한다.  

[변환함수 참조 6.1](http://poiemaweb.com/css3-effect)  

`단위의 %는 `자신의` 퍼센트이다.`
---
#### 1. transform
변환 함수를 프로퍼티 값으로 쉼표없이 나열한다.  
나열 순서에 따라 차례로 효과가 적용된다.
```
transform: func1 func2 func3 ...;
```
#### 2. transform-origin
요소의 기본기준점을 설정할 때 사용한다.

어디를 중심으로 변형할 것인지가 관건.
> 기본기준점은 정중앙이다.(50%,50%).

이동은 기준점을 변경해 일정거리만큼 이동하기에 의미가 없다.

- 설정값
    - %, px, top left, bottom right

>0,0 : top left, 100% 100% : bottom right 와 같은 값이다.
### 2. 3D 트랜스폼(3D Transform)
프로퍼티값으로 변환함수를 사용한다.

<!-- 2017.0724 suhyoenjo --!>