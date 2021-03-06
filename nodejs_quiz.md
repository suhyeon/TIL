## 평가지
- 자바스크립트에서 긴 시간동안의 계산이 필요한 코드는 알고리즘을 최대한 효율적으로 수정해서 자바스크립트 엔진 내에서 직접 코드를 실행시키는 것이 최선의 전략이다. 
`아니오`
> python, c++등등으로 보내는게 최적
- Promise는 에러 처리를 위해 try, catch 구문을 사용한다. 
아니오
> then을 사용한다
- HTTP/2는 속도 개선에 중점을 두고 개발되었다. 
예

- HTTP 메소드의 성질 중 Safe는 여러 번 같은 요청을 해도 한 번 요청한 것과 같은 효과를 내는 성질을 가리킨다. 
아니오
>idempotent의 성질이다. 
> delete, put = idempotent
> get 은 safe하게 만들어야한다.
- 서버 구현 시 POST 메소드는 Idempotent 성질을 만족시켜야 한다. 
아니오
> post는 요청할 때마다 새로운 것을 생성해야 한다.
- 한글은 자유롭게 URL이나 application/x-www-form-urlencoded 형태의 요청 바디 내에 사용될 수 있다. 
아니오
- 301, 302 상태 코드를 갖는 응답의 경우, 실제 자료의 위치가 어디인지를 나타내기 위해 Location 헤더를 사용한다. 
예
- HTML form을 이용해 파일을 업로드하기 위해서는 form 태그의 enctype 속성에 multipart/form-data 를 설정해야만 한다. 
예
- UUID는 식별자로 사용하기 위해 고안된 수 형식이며, UUID 형식의 난수를 생성하기 위해 UUID version 4를 사용한다.  
예
- Express 미들웨어는 등록되는 순서에 관계 없이 잘 동작하도록 만들어졌다. 
아니오
- Express 라우트 핸들러도 next 함수를 인자로 받을 수 있으며, next 함수를 호출하면 요청을 처리하지 않고 다른 핸들러로 요청을 넘긴다. 
예
- 쿠키는 서버에 저장된다. 
아니오
- 쿠키는 처음부터 자바스크립트를 통해 저장하고 접근하려는 목적으로 설계되었다. 
아니오
> 오히려 자바스크립트를 통해 사용하는게 권장되지 않는다.
- 쿠키에 저장할 수 있는 자료의 용량에는 제한이 없다. 
아니오
> 4kb
- 동일 출처 정책(Same-origin Policy)는 웹 보안의 기본 원칙으로, 리소스의 출처가 웹페이지의 출처와 같을 때 해당 리소스가 안전하다고 보는 원칙이다. 
예
- 웹 페이지와 API 서버의 도메인이 같다면 자유롭게 Ajax 요청을 보낼 수 있다. 
아니오
> 프로토콜. 포트번호까지 같아야한다.
- Cross-origin Unsafe 요청(POST, PUT, PATCH, DELETE 등)에 대해서는 웹 브라우저가 서버에 본 요청을 보내기 전에 시험적으로 요청을 한 번 보내며, 그 요청의 메소드는 OPTIONS이다. 
예
- Cross-origin 요청에는 기본적으로 쿠키가 포함되지 않으나, 쿠키를 포함시킬 수 있는 방법은 존재한다. 
예
- 토큰 기반 인증을 하면 대부분의 보안 문제가 해결된다. 
아니오
- 토큰 기반 인증에서 토큰은 주로 자바스크립트 엔진의 변수에 저장한다. 
아니오
> localstroage에 저장하고 관리한다.
- React나 EJS 등의 템플릿 엔진을 사용하면, XSS 공격에 대한 방어는 충분하다. 
예
- JWT를 사용하면 서명을 통해 조작을 방지할 수 있다. 
예
- 관계형 데이터베이스는 UNIQUE KEY 제약조건을 사용해 테이블 간의 관계를 표현한다.
아니오
> pk, fk를 사용한다.
- 데이터베이스와 웹 서비스 연동 시에는 원활한 운영을 위해 root 계정을 이용하는 것이 좋다.
아니오
> 실제서비스 이용시에는 절대 사용하면 안된다.
- 테이블에 레코드를 하나 추가했다는 것은 테이블에 열(column)을 추가했다는 것과 같은 말이다.
아니오
> 레코드를 추가했다 : insert int를 했다의 의미와 같다.
> 행을 추가했다는 의미이다.
- MySQL의 DATETIME 타입에는 시간대 정보가 저장되지 않지만, TIMESTAMP 타입에는 시간대 정보가 저장된다.
예
> knex : 타임스탬프
> 시퀄라이저 : datetime이 디폴트
- DEFAULT 제약조건을 이용해 해당 열의 기본값을 지정할 수 있다.
예
- ORDER BY 구문에서 오름차순 정렬을 위해 사용하는 키워드는 DESC이다.
아니오
>asc : 오름차순, desc: 내림차순
- 어떤 열에 저장되어 있는 값이 NULL 인지 아닌지를 판별하기 위해서 = 혹은 != 연산자를 사용할 수 있다.
아니오
> null비교를 할때는 isnull, isNotNull을 사용해야 한다.
- 두 테이블을 조인할 때, 외래 키에 NULL이 저장되어 있어도 해당 레코드를 표시하는 조인 방식을 OUTER JOIN이라고 한다.
예
> inner join : 외래키에 null이 저장되어 있어도 표시 안해주는 조인 방식
- 서브쿼리로 짠 모든 SQL 구문은 조인을 이용해 다시 짤 수 있다.
아니오
> join으로 짤 수 있는 쿼리가 따로 있다.
- 인덱스는 읽기 효율을 희생시켜 쓰기 속도를 높인다.
아니오
> 반대로 쓰기 효율을 희생시켜 읽기 효율을 높인다.
- 여러 쿼리에 걸쳐 데이터 조작의 신뢰성을 확보하기 위해 트랜잭션을 사용하며, 트랜잭션 내의 변경사항을 모두 취소하고 원상복구 시키는 구문은 ROLLBACK 이다.
예
