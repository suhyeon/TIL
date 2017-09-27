# `MONGO DB` 
## `MEAN STACK`
> sungback@naver.com  질문사항 : 연락 줄 것!!   
> blog.naver/sungback

Mongodb Express Angular Node STACK : 공통점 - JAVASCRIPT로 이루어진 기술
> MEAN STACK 개발을 할 수 있는 개발자 : FULL STACK 개발

## MONGODB?
- 크로스 플랫폼(윈도우, 리눅스, 맥)
- DOCUMENT (JSON과 같은 형태의 동적 스키마형 문서)지향
- NOSQL 데이터베이스 시스템
- 오픈소스
- C++로 작성됨(내부적구성언어)
- 높은 확장성
- 높은 성능
- 더 쉽고 빠르게 데이터 통합 가능

### IT
INFORMATION TECHNOLOGY
- 데이터 
  - 저장
    - 데이터 저장소
  - 처리
    - NOSQL(NOT ONLY SQL), SQL

- NOSQL
  - `키:값: READYS`
  - `문서기반(JSON) : JavaScript Object Notation`
  - column family
  - graphDB

## 데이터 저장소에 대한 CAP 이론
- 일관성(Consistency)
  - 모든 노드가 같은 순간에 같은 데이터를 볼 수 있다.
- 가용성(Availability)
  - 모든 요청이 성공 또는 실패 결과를 반환할 수 있다.
- 분할내성(Partition tolerance)
  - 메시지 전달이 실패하거나 시스템 일부가 망가져도 시스템이 계속 동작 할 수 있다.

> 세개를 다 동시에 성공할 수 없다.
- CAP분류 : 전통적인 RDBMS, 트렌젝션
- CP분류 : 구글BIGTABLE, HBASE
- AP분류 : Dynamo, Cassandra, MongoDB

## 몽고디비 설치 - MongoDB install

### summary
- [download](https://www.mongodb.com/download-center?jmp=nav#community) 
- install
- env setting
  - path : C:\Program Files\MongoDB\Server\3.4\bin 추가
  - 폴더 생성
    - C:\Users\(user명)> cd /
    - C:\> mkdir data
    - C:\> cd data
    - C:\data> mkdir db
- service apply
- test 
  - server : mongod.exe
  - 창을 하나 더 띄운다.
  - client : mongo.exe
```bin
C:\data> mongo.exe
    > show dbs  // > 은 몽고디비 프롬프트, show dbs 는 db 들을 보자는 명령
    > db.member.insert({"id":"hong", "email":"hong@naver.com"})  // 저장
    > db.meber.find()  // 확인
    { "_id" : ObjectId("59bdda299b9eaa64ea7e4238"), "id" : "hong", "email" : "hong@naver.com" }
    //_id: mongodb가 관리하는 pk
```
- GUI TOOL 
  - robomongo.org/download
> port: [thread1] waiting for connections on port `27017`

## RDBMS VS. MONGODB
- INSERT  
SQL :  insert into members ("name","email") values("홍길동","hong@aaa.com")  
MongDB : db.members.insert({name:"hong", email:"hong@aaa.com"})

- SELECT  
SQL : select * from members where name="홍길동"  
MongoDB : db.members.find({name:"홍길동"})

- Update  
SQL : update members set email="hong@aaa.com" where name="홍길동"  
MongoDB : db.members.update( {name:"홍길동"}, {$set :{email:"hong@aaa.com"} } )

- Delete  
SQL : delete from members where name="홍길동"  
MongoDB : db.members.remove({name:"홍길동"})


## REST API  AND MONGODB
- http method
  - post
  - get
  - put
  - delete
- role
  - resource create
  - resource search
  - resource alert
  - resource delete
- mongodb function
  - insert, save
  - find
  - update
  - delete

## blocking vs non-blocking
- blocking
  - 일반 교차로
  - 분류 8곳
  - 합류 8곳
  - 교차 16곳
- non blocking
  - 회전 교차로
  - 분류 4곳
  - 합류 4곳
  - 교차 0곳

## MONGOOSE
NODE.JS 와 연결하는 모듈
```javascript
var mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/test');

var Cat = mongoose.model('Cat', { name: String });

var kitty = new Cat({ name: 'Zildjian' });
kitty.save(function (err) {
  if (err) {
    console.log(err);
  } else {
    console.log('meow');
  }
});
```