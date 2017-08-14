# SASS - SCRIPT

SASSSCRIPT 는 CSS에서는 불가능한 연산, 변수, 함수등의 확장기능을 의미한다.

## 1. DATA TYPE

## 2. 변수
변수명은 $로 시작한다.


## 4. 연산자
```css
$width: 100px;

#foo {
  width: $width + 10; // 110px
}
//변수는 좌측에 작성하는 것이 더 좋다.
#bar {
  width: $width + 10in; // 1060px
}
```
em은 해당 요소에 적용된 사이즈를 바탕으로 계산.
%는 부모의 %
rem은 root em 으로 html에 적용된 사이즈를 기본으로 한다.
html에 없다면 16px을 기준으로 한다.
vp : 뷰포트를 기준으로 한다.

```css
p {
  /*
    font: font-style font-variant font-weight font-size/line-height font-family
  */
  font: italic bold 12px/30px Georgia, serif;
}
```

- sass의 /연산자를 사용하기 위해선 몇가지 조건이 필요하다.
    - 변수에 대해 사용
    - 괄호내에서 사용
    - 다른 연산의 일부로서 사용

> 변수를 css의 /와 함께 사용하고자 하는 경우 #{}(interpolation)을 사용한다.

```css
p {
  $font-size: 12px;
  $line-height: 30px;
  font: #{$font-size}/#{$line-height};  // 12px/30px
}
```

### 2. 컬러 연산자
모든 산술 연산자는 컬러값에도 사용 할 수 있다.
```css
p {
  color: #010203 + #040506;
  // R: 01 + 04 = 05
  // G: 02 + 05 = 07
  // B: 03 + 06 = 09
  // => #050709
}

p {
  color: #010203 * 2;
  // R: 01 * 2 = 02
  // G: 02 * 2 = 04
  // B: x03 * 2 = 06
  // => #020406
}

p {
  color: rgba(255, 0, 0, 0.75) + rgba(0, 255, 0, 0.75);
  // alpha 값은 연산되지 않는다
  // color: rgba(255, 255, 0, 0.75);
}
```

- opacify 함수 : 첫번째 argument의 alpha 값에 두번째 argument를 더해 불투명도를 증가(불투명해진다.)
- transparentize 함수 : 첫번째 argument의 alpha 값에 두번째 argument를 빼서 불투명도를 감소(투명해진다.)

### 7. Ampersand(&)
부모요소를 참조하는 셀렉터

```css
a {
  color: #ccc;

  &.home {
    color: #f0f;
  }

  &:hover {
    text-decoration: none;
  }

  // & > span (X)
  > span {
    color: blue;
  }

  span {
    color: red;
  }
}
```
컴파일 결과
```css
a {
  color: #ccc;
}

a.home {
  color: #f0f;
}

a:hover {
  text-decoration: none;
}

a > span {
  color: blue;
}

a span {
  color: red;
}
```
html의 구조와 유사하게 맞춘다.

### !default
!default flag는 할당되지 않은 변수의 초기값을 설정한다.

파샬에 매우 유용하다.