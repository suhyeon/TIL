# NodeJs - day3
# HTML FORM 의 기본동작
- HTML FORM을 전송하면 입력된 정보가 기본적으로 PERCENT ENCODING 되어 요청됨
  - GET METHOD
```javascript
    GET /search?query=%EA%B0%9C&sort=latest HTTP/1.1
... //쿼리스트링 안에 정보가 다있다.
 ```
  - POST METHOD 
```javascript
POST /form HTTP/1.1
Content-Type: application/x-www-form-urlencoded
...//헤더를 다 적고 난 이후에 작성한다.

home=Cosby&favorite+flavor=flies
```

## Multipart/form-data
- 기본 설정으로는 폼으로 파일을 업로드하는 것은 불가능
- (클라이언트 측)form 태그에 enctype="multipart/form-data"속성을 적용하면 파일 업로드 가능
- (서버 측) body-parser 미들웨어는 multipart/form-data형태의 요청을 지원하지 않음(multer 필요)
[multer 란?](https://www.npmjs.com/package/multer)