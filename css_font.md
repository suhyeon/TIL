# CSS - FONT & TEXT
폰트의 크기, 지정, 스타일, 정렬등을 정의한다.

## 1.font-size 프로퍼티
텍스트의 크기를 정의한다.

```
    .font-size-40 { font-size: 40px; }
    .font-size-2x { font-size: 2.0em; }
    .font-size-150ps { font-size: 150%; }
    .font-size-large { font-size: large; }
```
## 2. font-family 프로퍼티
폰트를 지정한다. 
>컴퓨터에 해당폰트가 설치되어 있지않으면 적용되지 않는다.

```
    .serif {
      font-family: "Times New Roman", Times, serif;
    }

    .sans-serif {
      font-family: Arial, Helvetica, sans-serif;
    }

    .monospace {
      font-family: "Courier New", Courier, monospace;
    }
    //대개 3개를 지정해주는 것이 좋다고 한다.
```

## 3. font-style / font-weight 프로퍼티
이텔릭체의 지정, 폰트 굵기 지정에 사용된다.

```
    /* 
      font-style 
      normal / italic / oblique
    */
    .italic {
      font-style: italic;
    }

    /* 
      font-weight 
      100 ~ 900 or normal / bold / lighter / bolder
    */
    .light {
      font-weight: lighter;
    }
```

## 4. font Shorthand

형식
> mandatory : 반드시 지정해야 하는 것  
> optional : 생략가능한 것
```
ont : font-style(optional) font-variant(optional) font-weight(optional) font-size(mandatory) line-height(optional) font-family(mandatory)
```

## 5. line-height 프로퍼티
텍스트의 높이를 지정한다.   
텍스트의 수직정렬에 응용된다.

> 요소의 line-height 값과 부모요소의 height 값을 일치시킨다.
```
//수직중앙정렬예제
 .button {
      height: 70px;
    }
.button > a {
      font: italic bold 2em/70px Arial, Helvetica, sans-serif;
      text-align: center;
    }
```

## 6. letter-spacing 프로퍼티
글자 사이의 간격을 지정한다.
## 7. text-align 프로퍼티
텍스트의 수평정렬을 정의한다.
## 8. text-decoration 프로퍼티
링크 underline을 제거할 수 있다.
underline, overline, line-through를 추가할 수 있다.
## 9. white-space 프로퍼티
공백, 들여쓰기, 줄바꿈을 의미한다.  
기본동작을 제어하기 위한 프로퍼티

## 10. text-overflow 프로퍼티
부모 영역을 벗어난 wrapping이 되지 않은 텍스트의 처리방법을 정의한다.
>사용하기 위한 조건은 다음과 같다.
- overflow 프로퍼티에 반드시 visible 이외의 값이 지정되어 있어야 한다.
- width 프로퍼티가 지정되어 있어야 한다.
- 자동줄바꿈을 방지하기 위해 white-space 프로퍼티를 nowrap으로 설정한다.
## 11. word-wrap 프로퍼티
한 단어의 길이가 길어서 부모 영역을 벗어난 텍스트의 처리방법을 정의한다.
## 12. word-break 프로퍼티
word-wrap과 비슷하지만 단어를 고려하지 않고 부모영역에 맞춰 강제 개행을 한다.
<!--2017.07.22 SuhyeonJo --!>