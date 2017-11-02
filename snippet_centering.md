# SNIPPET - CENTERING 
## 1. 수평정렬
---
### 1. INLINE/INLINE-BLOCK요소
정렬 대상요소의 부모 요소에 text-align: center; 를 지정
```
.container {
  text-align: center;
}
```
- margin-bottom/top을 줄 수 없다.
- margin-left/right을 줄 수 있다.

### 2. BLOCK요소
정렬대상 요소에 너비를 명시적으로 지정하고 margin-left, margin-right에 auto지정
> 정렬대상에 너비를 명시적으로 지정하지 않으면 너비는 fullwidth 가 되서 중앙정렬이 필요없다.
```
.item {
  width: 200px;
  margin: 20px auto;
}
```
### 3. 복수의 block 요소
정렬 대상 block 요소를 inline-block 으로 바꾸고 부모 요소에 text-align: center;를 지정

>정렬 대상요소에 width를 지정하지 않으면 컨텐츠에 너비를 맞춰 결정되므로 지정하라.

```
.container {
  text-align: center;
}
.item {
  width: 150px;
  display: inline-block;
}
```
---
## 2. 수직 정렬
---
### 1.1 Single line
정렬 대상의 부모 요소에 padding-top과 padding-bottom값을 똑같이 한다.

패딩을 사용할 수 없는 경우, heigh = line-height를 적용.
> 텍스트가 한줄일 때만 사용할 수 있다. (클랙 데드존의 이슈 발생)

### 1.2 여러줄
padding-top과 padding-bottom을 동일하게 적용
vertical-align 프로퍼티를 사용하라.
>이방법으 table 속성을 사용해야 한다.
```
.parent {
  display: table;
  height: 100px;
}
.child {
  display: table-cell;
  vertical-align: middle;
}
```
## 2. block 요소
### 2.1 요소의 높이가 고정되어 있는 경우
부모요소를 기준으로 절대 위치를 지정한다.

### 2.2 요소의 높이가 불확정 상태의 경우
부모요소를 기준으로 절대 위치를 지정한다.

## 3. 수평/수직 정렬
요소의 너비와 높이가 고정되어 있는 경우, 요소의 너비와 높이가 불확정 상태일 경우 모두 사용 가능한 방법이다.
```
.parent {
  position: relative;
}
.child {
  position: absolute;
  top: 50%;
  left: 50%;
  /*요소의 높이/너비의 반(50%)만큼 위/왼쪽으로 이동*/
  transform: translate(-50%, -50%);
}
```