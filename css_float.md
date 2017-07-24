# CSS - FLOAT
LAYOUT을 구성하기 위해 사용되는 핵심 기술

> 큰틀을 먼저 생각해서 만들어라!

- 목적 : 
    - 1개 이상의 요소를 원하는 위치에 정렬 시키는 것

> 본래 이미지와 텍스트가 있을 때 , 이미지 주위를 텍스트로 감싸기 위해 만들어진 것
---
- none
    - 요소를 떠있게 하지 않는다.(기본값)
- right
    - 요소를 오른쪽으로 이동시킨다.
- left
    - 요소를 왼쪽으로 이동시킨다.
- 중앙에 정렬
    - margin: auto;

## 1. 정렬

float를 사용하지 않는다 : 수직정렬  
float: left; : 왼쪽부터 정렬  
float: right; : 오른쪽부터 정렬

> 오른쪽 정렬의 경우, 먼저 기술된 요소가 가장 오른쪽에 출력되므로 출력순서가 역순이 된다.

```
      /*float: left;*/
      float: right;
```
`float 프로퍼티는 좌측, 우측 정렬만 할 수 있다.  
중앙 정렬은 margin프로퍼티를 사용해야 한다.`
---
## 2. float 프로퍼티 관련 문제 해결법
---
### 1. float 프로퍼티가 선언된 요소와 float 프로퍼티가 선언되지 않은 요소간 margin이 사라지는 문제

두 번쨰 요소에 float 프로퍼티를 선언하지 않아서 발생하는 박스 모델상의 문제 해결  
float 프로퍼티를 선언하지 않은 요소에 `overflow: hidden` 프로퍼티를 선언하는 것

>overflow: hidden은 자식 요소가 부모요소의 영역보다 클 경우 넘치는 부분을 안보이게 해주는 역할을 한다.

### 2. float 프로퍼티를 가진 자식 요소를 포함하는 부모요소의 높이가 정상적으로 반영되지 않는 문제
float 프로퍼티가 선언된 두개의 자식 요소를 포함하는 부모 요소의 높이가 정상적인 값을 가지지 못하는 문제
>  float 요소는 일반적인 흐름상에 존재하지 않기 때문에 float 요소의 높이를 알 수 없다.

해결법 : 
- float 프로퍼티를 가진 요소의 부모요소(wrap)에 overflow: hidden 프로퍼티를 선언한다.
- 부모요소에 float 프로퍼티를 부여하는 방법
    - 부모요소의 너비는 float 된 두개의 자식 요소의 컨텐츠를 표현할 수 있는 만큼만으로 작게 줄어들게 된다.(권장하지 않는다.)

- float 프로퍼티 대신 display: inline-block; 설정
    - inline-block 프로퍼티 요소를 연속 사용하는 경우, 좌우에 정의하지 않은 space가 자동 지정되는 것
- 부모 요소에 clearfix 클래스만 추가하거나, 해당 요소를 선택해 clear 문법을 선언한다.(추천)
```
    .clearfix:after {
      content: "";
      display: block;
      clear: both;
    }
```
```
selector:after {
  content: "";
  display: block;
  clear: both;
}
```
- float 대신 display: inline-block;을 선언
    - 주의 : 인라인블록을 연속사용하면, 좌우에 정의하지 않은 space(4px)가 자동지정된다.
    
[space(4px)를 회피하는 것 참조] (https://css-tricks.com/fighting-the-space-between-inline-block-elements/)
> overflow: hidden; 과 많이 사용되는 방법 : ::after 가상 요소 선택자를 이용하는 것

[layout example 참조] (http://poiemaweb.com/css3-float)
<!-- 2017.07.24 suhyeonjo --!>