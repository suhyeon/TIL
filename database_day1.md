# DataBase

## 데이터베이스와 테이블의 생성

### CREATE DATABASE는 데이터베이스를 만드는 명령어입니다. 워크벤치에서 root 계정으로 로그인한 후, 아래의 SQL을 실행해보세요.

```sql
-- 데이터베이스 생성
CREATE DATABASE my_db;

-- 모든 데이터베이스의 목록
SHOW DATABASES;
```

### CREATE TABLE은 테이블을 만드는 명령입니다. 아래 명령을 차례로 실행해보세요.

```sql
-- 테이블 생성
CREATE TABLE my_db.users (
  -- `name`이라는 이름의 문자열 컬럼을 생성합니다. NULL을 허용하지 않습니다.
  name VARCHAR(30) NOT NULL,
  -- `job`이라는 이름의 문자열 컬럼을 생성합니다. NULL을 허용합니다.
  job VARCHAR(30),
  -- `age`라는 이름의 양수 컬럼을 생성합니다. NULL을 허용합니다.
  age INTEGER UNSIGNED,
  -- `name` 컬럼을 기본 키로 지정합니다.
  PRIMARY KEY (name)
);

-- my_db 데이터베이스에 있는 모든 테이블의 목록
SHOW TABLES FROM my_db;

-- my_db.users 테이블에 대한 자세한 정보
DESCRIBE my_db.users;
SHOW CREATE TABLE post;
```


### USE [database]는 기본 데이터베이스를 설정하는 명령입니다. 즉, SQL을 작성할 때 데이터베이스 이름을 생략할 수 있게 만들어줍니다. 워크벤치에서는 사이드바의 데이터베이스 이름을 더블 클릭해도 같은 동작을 합니다. 기본 데이터베이스를 선택한 후 아래 명령을 실행해보세요.

```sql
DESCRIBE my_table;

```


## 데이터 추가하기

```sql
-- 하나의 레코드 추가하기
INSERT INTO users (name, job, age)
VALUES ('윤민지', '프론트엔드 개발자', 32);

-- 여러 개의 레코드 추가하기
INSERT INTO users (name, job, age)
VALUES ('한주원', '프론트엔드 개발자', 39),
('박현숙', '백엔드 개발자', 48),
('정병언', NULL, 25),
('임동면', '디자이너', NULL);
```

## 데이터 불러오기

```sql
-- 모든 컬럼을 포함시켜 불러오기
SELECT * FROM users;
-- 특정 컬럼만 포함시켜 불러오기
SELECT name, job FROM users;
```

## 데이터 수정하기

```sql
UPDATE users
SET job = '프로그래머'
WHERE name = '정병언';
```

## 데이터 삭제하기

```sql
DELETE FROM users
WHERE name = '정병언';
```

## 데이터베이스와 테이블의 삭제

```sql
DROP DATABASE, DROP TABLE 명령은 각각 데이터베이스와 테이블을 삭제하는 명령입니다. 아래의 명령을 차례대로 실행해보세요.

-- users 테이블 삭제
DROP TABLE users;

-- my_db 데이터베이스 삭제
DROP DATABASE my_db;
```

## 관계형 데이터베이스의 구성요소

### Database (데이터베이스)

- 테이블 및 다른 구성요소들을 모아놓은 집합입니다.  
- 스키마라고도 불리는데, 스키마라는 용어는 '데이터베이스'를 의미하기도 하고 **'데이터베이스의 구조'**를 의미하기도 합니다.  
- 하나의 DBMS는 여러 개의 데이터베이스를 가질 수 있으며, 데이터베이스 단위로 `권한 설정`이 이루어집니다.  


### User & Privilege (사용자 & 권한)

- 하나의 DBMS는 여러 개의 사용자 계정을 가질 수 있습니다.  
- DBMS를 사용하려면 사용자 계정을 이용해 DBMS에 접속해야 합니다.  
- 사용자 계정은 데이터베이스 별로 다른 권한을 가집니다.  
- root 유저는 DBMS 초기 설치 시에 만들어지는 계정이며, DBMS에 대한 모든 권한을 부여받습니다.  

### Connection

- 사용자 계정을 이용해 데이터베이스에 접속하면, 새 `커넥션`이 만들어집니다.  
- 세션과 유사한 개념입니다.  
- 커넥션 별로 여러가지 옵션을 설정할 수 있고, `트랜잭션`도 커넥션 단위로 수행됩니다.  
- 하나의 클라이언트에서 여러 개의 트랜잭션을 수행하기 위해 여러 커넥션을 이용할 수 있습니다.  

### Table (테이블)

- 하나의 데이터베이스는 여러 개의 테이블을 가질 수 있습니다.  
- 표 형태로 구조화된 데이터가 테이블에 저장됩니다.  
- 테이블의 **행(row)**은 개별적인 레코드를 나타내며, 테이블의 **열(column)**은 레코드의 속성을 나타냅니다. 각각의 열에는 미리 정의된 자료형에 해당하는 데이터만 저장될 수 있습니다.  
- 테이블의 각 행은 기본 키(primary key)를 이용해 식별하고, 테이블 내에서 유일한 값이어야 합니다. 기본 키는 다른 테이블과의 관계를 나타낼 때 사용됩니다.  

### Constraint (제약 조건)

제약 조건을 지정하면 테이블에 특정한 방식으로만 데이터가 저장될 수 있도록 할 수 있습니다. 아래 제약 조건들이 자주 사용됩니다.  

- `NOT NULL` : 컬럼에 NULL 값이 저장되지 못하도록 막습니다.  
- `UNIQUE` : 한 테이블 내에서 컬럼에 저장된 모든 값이 유일하도록 강제합니다.  
- `PRIMARY KEY` : NOT NULL과 UNIQUE가 동시에 적용됩니다. PRIMARY KEY 제약 조건이 걸린 컬럼은 각 행의 식별자로 사용됩니다.  
- `FOREIGN KEY` : 다른 테이블의 primary key를 참조합니다. 해당 primary key를 가진 레코드가 변경되었을 때 특정 동작을 강제할 수 있습니다.  
- `DEFAULT` : INSERT 구문을 사용해서 레코드를 추가할 때, 컬럼에 아무런 값도 지정하지 않으면 DEFAULT 제약 조건으로 지정한 기본값이 저장되도록 합니다.  
- `CHECK` : 레코드가 주어진 계산식을 만족해야만 하도록 CHECK 제약 조건을 지정할 수 있습니다.  

```sql
CREATE TABLE adult (
  name varchar(255) NOT NULL,
  nationality varchar(255) DEFAULT '대한민국',
  age int,
  CHECK (age >= 18)
);
```

### Primary Key, Foreign Key

Primary Key(기본 키)로 지정된 컬럼에 저장되어 있는 값은 테이블에 저장되어 있는 레코드의 식별자 역할을 합니다. Foreign Key(외래 키)로 지정된 컬럼에는 다른 테이블의 기본 키 값이 저장되며, 다른 테이블의 레코드를 참조함으로써 해당 테이블과의 관계를 나타냅니다.  

여러 컬럼이 한꺼번에 기본 키로 지정될 수도 있습니다. 이를 Composite primary key(한국어로는 합성키, 혹은 슈퍼키라고 부름)라고 합니다.  


## 테이블 생성

테이블을 생성할 때는 `CREATE TABLE` 구문을 사용합니다.

```sql
CREATE TABLE my_table (
  -- 일반적인 컬럼은 아래와 같의 정의합니다. 이 컬럼에는 NULL 값이 저장될 수 있습니다.
  my_col1 INTEGER,

  -- 컬럼의 기본값을 지정합니다.
  my_col2 INTEGER DEFAULT 0,

  -- 컬럼에 NULL 값이 저장될 수 없도록 제한을 둡니다.
  my_col3 INTEGER NOT NULL,

  -- UNIQUE 제약조건: 컬럼의 값은 테이블 내에서 유일해야 합니다.
  my_col4 INTEGER UNIQUE,

  -- 다양한 옵션을 한 번에 지정할 수 있습니다.
  my_col5 INTEGER NOT NULL DEFAULT 1,
  my_col6 INTEGER NOT NULL UNIQUE,

  -- 1부터 시작하는 식별자를 아래와 같이 정의합니다.
  -- PRIMARY KEY는 기본적으로 NOT NULL, UNIQUE 규칙이 적용됩니다.
  my_id INTEGER UNSIGNED AUTO_INCREMENT PRIMARY KEY,

  -- 컬럼 정의와 별도로, 여러가지 제약 조건과 인덱스를 아래에 지정할 수 있습니다.
  -- 제약 조건과 인덱스에 대해서는 추후 배울 것입니다.
  FOREIGN KEY (my_id) REFERENCES your_table(your_id) ON DELETE CASCADE,
  INDEX my_idx (my_col1, my_col2),
  ...
)
```

테이블이 이미 존재하는 경우에도 구문이 에러 없이 실행되도록 IF NOT EXISTS 구문을 사용할 수 있습니다.  

```sql
CREATE TABLE IF NOT EXISTS table_name (
  ...
)
```

## 테이블 수정

```sql
ALTER TABLE table_name
RENAME new_table_name, -- 테이블 이름 변경
ADD COLUMN column_name INTEGER NOT NULL, -- 컬럼 추가
ADD CONSTRAINT UNIQUE, -- 제약 조건 추가
CHANGE old_column_name new_column_name INTEGER, -- 컬럼 이름 변경
MODIFY column_name NEW_TYPE -- 컬럼 타입 변경
DROP COLUMN column_name; -- 컬럼 제거
```

자세한 사용법은 공식 문서를 참고해주세요.

## MySQL 데이터 타입

### 문자열

### VARCHAR

짧은 문자열을 저장하기 위해 가장 널리 사용되는 타입입니다. 컬럼 타입으로 지정할 때는 아래와 같이 문자열의 길이(바이트)를 명시해야 합니다.

```sql
VARCHAR(255) -- 255는 가장 널리 사용되는 길이입니다.
```

### TEXT

긴 문자열을 저장하기 위해 사용되는 타입입니다. TEXT 타입의 컬럼에는 64MB까지 저장할 수 있습니다. 요구사항에 따라 크기가 다른 다양한 종류의 TEXT 타입(TINYTEXT, TEXT, MEDIUMTEXT, LONGTEXT)을 사용할 수 있습니다.  

### 수

정수, 고정 소수점, 부동 소수점을 위한 타입이 있습니다. 모든 수 타입은 양수만을 저장하기 위해 타입 뒤에 UNSIGNED 지시자를 사용할 수 있습니다.  

### INTEGER

정수를 위한 타입입니다. INT로 줄여 쓸 수도 있습니다. 요구사항에 따라 크기가 다른 다양한 종류의 INT 타입(TINYINT, SMALLINT, MEDIUMINT, INT, BIGINT)을 사용할 수 있습니다.

```sql
INTEGER UNSIGNED -- INTEGER 타입의 양수를 저장할 수 있습니다.
```

MySQL에는 참, 거짓을 나타내는 boolean 관련 타입이 없습니다. 대신 TINYINT를 사용합니다.

### DECIMAL

고정 소수점 수를 위한 타입입니다. 십진수의 정확한 계산이 필요할 때 사용합니다. 정수부(최대 65), 소수부(최대 30, 정수부보다 짧거나 같아야 함)의 최대 길이를 각각 지정할 수 있습니다.  

```sql
DECIMAL(5, 2) -- 12345.67과 같은 수를 저장할 수 있습니다.
```

### DOUBLE

부동 소수점 수를 위한 타입입니다. 소수의 빠른 계산과 효율적 저장이 필요할 때 사용합니다.  

### 시각

MySQL에는 시각의 저장을 위한 타입들이 준비되어 있습니다. 주로 사용되는 아래의 두 타입은 시간대 정보를 저장하지 않기 때문에, 사용에 주의를 요합니다.  

### DATE

DATE 타입은 날짜를 위한 타입입니다.  

### DATETIME

DATETIME 타입은 날짜와 시각을 같이 저장해야 할 때 사용합니다.  

### 기타

ENUM: 열거형을 위한 타입입니다.  
JSON: MySQL 5.7에 JSON 지원이 추가되었으나, 널리 사용되지는 않습니다.  
POINT, GEOMETRY : 공간 정보를 위한 타입입니다.  

## 계정 만들기

실습하기에 앞서, employees 데이터베이스에만 접속할 수 있는 emplyees_user 계정을 만든 후 그 계정을 이용해 MySQL에 접속해봅시다.  

## SELECT

가장 단순한 SELECT 구문을 실행해보겠습니다.  

```sql
SELECT * FROM employees;
```

실행 후, 아래와 같이 결과가 나오면 성공입니다. employees 테이블에는 어떤 컬럼들이 있는지, 각 컬럼에는 어떤 형태의 데이터가 저장되고 있는지 파악해두도록 합시다.  

MySQL Workbench는 레코드의 갯수가 많을 경우에 1000개 단위로 페이지를 끊어서 보여주는 기능을 가지고 있습니다. 이미지의 우측 상단에 빨갛게 표시된 버튼들을 눌러서 페이지를 이동할 수 있습니다.  

이제 테이블의 일부 컬럼만 불러오는 구문을 실행해보겠습니다.  

```sql
SELECT first_name FROM employees;
```

위 명령은 employees 테이블에서 first_name 컬럼만을 불러옵니다. 아래와 같이 여러 개의 컬럼을 선택적으로 불러올 수 있습니다.  

```sql
SELECT first_name, last_name FROM employees;
```

또는 SQL 실행 결과로 출력되는 테이블의 컬럼의 이름을 바꾸어 출력할 수도 있습니다. 아래와 같이 각 컬럼의 이름 뒤에 AS 구문을 사용하면 됩니다. backtick(`) 문자를 사용해 컬럼의 이름에 MySQL 예약어나 공백 문자를 넣을 수 있습니다. (권장되지는 않습니다.)  

```sql
SELECT first_name AS `family name`, last_name AS `given name` FROM employees;
```

AS를 생략하고 써도 같은 의미입니다.

```sql
SELECT first_name `family name`, last_name `given name` FROM employees;
```

## 정렬하기

ORDER BY 구문을 사용하면 특정 컬럼에 대한 정렬 기준을 세워 테이블을 출력할 수 있습니다. 아래와 같이 hire_date 컬럼을 기준으로 오름차순 정렬을 시킬 수 있습니다.  

```sql
SELECT emp_no, hire_date, birth_date FROM employees
ORDER BY hire_date;
```

ORDER BY 구문에 포함된 컬럼이 꼭 SELECT 구문에 포함될 필요는 없습니다. 아래와 같이 SELECT 구문에서 hire_date를 생략해도 문제 없습니다.  

```sql
SELECT emp_no FROM employees
ORDER BY hire_date;
```
ORDER BY 구문은 여러 개의 컬럼에 대해서 정렬하는 기능도 지원합니다. 아래와 같이 여러 개의 컬럼을 쉼표로 구분해서 ORDER BY 구문에 넣어 주면 됩니다. 이 때, hire_date로 먼저 오름차순 정렬 되고 난 후, 같은 hire_date를 가진 레코드끼리 birth_date를 기준으로 오름차순 정렬이 이루어집니다.  

```sql
SELECT emp_no, hire_date, birth_date FROM employees
ORDER BY hire_date, birth_date;
```

ORDER BY 구문은 기본적으로 오름차순 정렬을 하게끔 되어 있습니다. 아래와 같이 DESC 구문을 사용하면 특정 컬럼에 대해서 내림차순 정렬을 하도록 명령할 수 있습니다. DESC와 ASC는 각각 'descending'과 'ascending'의 약자입니다.  

```sql
SELECT first_name, hire_date, birth_date FROM employees
ORDER BY hire_date DESC, birth_date ASC; -- ASC는 생략 가능
```

## Character Set & Collation

MySQL은 날짜, 숫자 뿐 아니라 문자열에 대한 정렬도 지원합니다. 아래와 같이 이름을 이용해 정렬을 할 수도 있습니다.  

```sql
SELECT first_name, last_name FROM employees
ORDER BY last_name, first_name;
```

MySQL은 다양한 언어와 문자셋을 지원합니다. 그런데 언어나 문자셋별로 문자열의 정렬 기준이 달라야 할 필요가 있습니다. 이러한 정렬 기준을 MySQL에서는 collation이라고 부릅니다.  

한글의 경우, 문자셋은 utf8, collation은 utf8mb4_general_ci를 사용하면 됩니다.  

MySQL 사용 중에 불러온 문자열이 깨져 보인다거나 정렬이 제대로 되지 않는다면, 문자셋과 collation의 설정이 잘못되었을 확률이 높습니다. 현재 데이터베이스의 기본 문자셋과 collation을 확인하려면, 아래와 같이 워크벤치 좌측 데이터베이스 목록의 'i' 모양 아이콘을 클릭하세요.  

## 일부만 가져오기

LIMIT 구문을 사용하면 레코드의 일부분만 불러올 수 있습니다.  

```sql
SELECT * FROM employees
LIMIT 5;
```

LIMIT 구문은 정렬 순서에 영향을 받습니다. 예를 들어, 생일이 가장 빠른 1명의 기록을 불러오고 싶다면 아래와 같이 하면 됩니다.  

```sql
SELECT first_name, birth_date FROM employees
ORDER BY birth_date
LIMIT 1;
```

OFFSET 구문을 사용하면 앞쪽 기록의 일부분을 생략하고 나머지 기록들을 불러올 수 있습니다. 예를 들어, 생일이 열 번째로 빠른 1명의 기록을 불러오고 싶다면 아래와 같이 하면 됩니다.  

```sql
SELECT first_name, birth_date FROM employees
ORDER BY birth_date
LIMIT 1 OFFSET 9;
```

## 중복되는 값 제거하기

DISTINCT 구문을 사용하면 컬럼 내에 중복되는 값을 하나로 합쳐서 보여줍니다. 아래 두 쿼리의 결과를 비교해보세요.  

```sql
SELECT first_name FROM employees
ORDER BY first_name;

SELECT DISTINCT first_name FROM employees
ORDER BY first_name;
```
## 필터링과 연산자

WHERE 구문을 사용하면 특정 조건을 만족하는 기록만을 선택적으로 불러올 수 있습니다.  

```sql
SELECT * FROM employees
WHERE first_name = 'Shahid' AND hire_date > '1997-09-12';
```

위와 같이 WHERE 구문에서는 조건을 나타내기 위해 연산자를 사용합니다. WHERE 구문 내에서 자주 사용되는 연산자와 그 뜻을 아래 표에서 확인할 수 있습니다.  

## 연산자 우선순위

여느 프로그래밍 언어가 그렇듯이 SQL에도 연산자 우선순위가 존재합니다. 예를 들어, OR보다 AND가 먼저 연산되기 때문에 아래와 같이 사용할 때는 주의해야 합니다.  

```sql
-- first_name이 'Jeong' 혹은 'Shahid'인 사람들 중, 입사일이 '1997-09-12' 이후인 사람들을 불러오기 (틀림)
SELECT * FROM employees
WHERE first_name = 'Jeong' OR first_name = 'Shahid' AND hire_date > '1997-09-12';
-- 뒤쪽의 AND가 먼저 연산되어, 원래 의도와는 다르게 first_name이 'Jeong'인 모든 사람들이 포함된 결과가 나옵니다.
```

아래와 같이 괄호를 사용해서 특정 연산이 먼저 실행되도록 할 수 있습니다.

```sql
-- first_name이 'Jeong' 혹은 'Shahid'인 사람들 중, 입사일이 '1997-09-12' 이후인 사람들을 불러오기
SELECT * FROM employees
WHERE (first_name = 'Jeong' OR first_name = 'Shahid') AND hire_date > '1997-09-12';
```
연산자 우선순위의 전체 목록을 확인하려면 공식 문서를 참고하세요.  

## DATE, DATETIME 리터럴

DATE 타입과 DATETIME 타입을 요구하는 문맥에서 아래와 같은 형태의 문자열을 사용하면, 자동으로 DATE와 DATETIME 형태로 해석됩니다.  

```sql
'YYYY-MM-DD HH:MM:SS' -- DATETIME을 나타내는 문자열 형식
'YYYY-MM-DD' -- DATE를 나타내는 문자열 형식
```

문자열을 사용해서 아래와 같이 hire_date와 같은 DATE 형태의 컬럼에 대해 필터링을 할 수 있습니다.  

```sql
SELECT * FROM employees
WHERE hire_date > '1997-09-12';
```

## NULL

NULL 값은 '데이터가 없음'을 나타내기 위한 목적으로 다루어지는 값입니다. 그런데 이 값은 연산 과정에서 특별하게 취급됩니다. 대부분의 연산자에 대해, 어떤 연산의 피연산자가 NULL이면 해당 연산의 결과는 무조건 NULL이 되게 됩니다.  

```sql
1 > NULL -- 결과는 NULL이 됩니다.
1 = NULL -- 결과는 NULL이 됩니다.
NULL = NULL -- 심지어 이것도 NULL이 됩니다!
```

따라서, NULL 값을 허용하는 컬럼에 대해 연산을 할 때는 주의해야 합니다. 특히, 어떤 컬럼의 값이 NULL인지 아닌지 확인하기 위해서는 = 연산자 대신에 IS 혹은 IS NOT 연산자를 사용해야 합니다. 이를 테스트해보기 위해 NULL 값이 포함된 컬럼을 하나 추가합시다.  

```sql
INSERT INTO titles (emp_no, title, from_date, to_date)
VALUES (10001, 'new title', '2017-09-11', NULL);
```

TRUE 혹은 FALSE를 써야하는 문맥에 NULL을 쓰면, FALSE로 취급됩니다. 아래 SQL 명령의 결과를 비교해보시기 바랍니다.  

```sql
-- 이렇게 하면 안 됩니다!
SELECT * FROM titles
WHERE to_date = NULL; -- 무조건 FALSE로 취급됨
-- 반드시 이렇게 해야 합니다.
SELECT * FROM titles
WHERE to_date IS NULL;
-- 이렇게 하면 안 됩니다!
SELECT * FROM titles
WHERE to_date != NULL; -- 무조건 FALSE로 취급됨
-- 반드시 이렇게 해야 합니다.
SELECT * FROM titles
WHERE to_date IS NOT NULL;
```

## salaries 테이블

실습용 employees 데이터베이스의 salaries 테이블에는 각 사원의 연봉 변동 내역이 저장되어 있습니다. 본 문서에서는 salaries 테이블을 이용해 실습합니다.  

## 집계 함수 (Aggregate Function)

MySQL은 여러가지 집계 함수를 지원합니다.  

집계 함수	의미  
MAX(col_name)	최대값  
MIN(col_name)	최소값  
SUM(col_name)	합계  
AVG(col_name)	평균  
COUNT(col_name)	컬림에 NULL이 아닌 값이 저장되어 있는 행의 갯수  
COUNT(*)	행의 갯수  

```sql

SELECT MAX(salary) FROM salaries;
SELECT MIN(salary) FROM salaries;
SELECT SUM(salary) FROM salaries;
SELECT AVG(salar...