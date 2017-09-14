# KNEX - QUERY BUILDER
## KNEX 인스턴스 생성
KNEX를 이용해 MYSQL 서버에 접속하기 위해서는 우선 아래와 같이 인스턴스를 만들어야 한다.
```javascript
const knex = require('knex')({
  client: 'mysql',
  connection: {
    host: 'localhost',
    user: 'root', // 실제 서비스에서는 root 계정을 사용하지 않는 것이 좋습니다.
    password: 'rootpassword',
    database: 'employees'
  }
})
```
## CONNECTION POOL
KNEX 인스턴스를 생성하면 CONNECTION POOL이 만들어진다.
> 한번에 여러 커넥션을 맺어 놓는다는 의미이다.  
`해당 커넥션을 이요해 인스턴스 생성시 별도의 옵션을 주지않는다면 커넥션 풀은 2개의 커넥션으로 시작하며, 필요에 의해 10개까지 늘어날 수 있다.`

## KNEX를 이용한 쿼리 수행
KNEX인스턴스를 이용해 쿼리를 날릴 수 있다.
> `주의!`레코드가 수십만개 이상인 경우에는 결과를 받아오는데에 시간이 오래걸리니 `반드시 LIMIT 메소드를 사용해주어야한다.`

```javascript
knex('salaries').limit(3).then(console.log)

// 결과
[ { emp_no: 10001,
    salary: 60117,
    from_date: 1986-06-25T15:00:00.000Z,
    to_date: 1987-06-25T14:00:00.000Z },
  { emp_no: 10001,
    salary: 62102,
    from_date: 1987-06-25T14:00:00.000Z,
    to_date: 1988-06-24T14:00:00.000Z },
  { emp_no: 10001,
    salary: 66074,
    from_date: 1988-06-24T14:00:00.000Z,
    to_date: 1989-06-24T15:00:00.000Z } ]
```
크넥스 인스턴스는 메소드체이닝 방식으로 사용하도록 만들어져있다.
```javascript
// 1위부터 10위까지의 최고 연봉자의 연봉과 first_name을 출력합니다.
knex('employees')//크넥스 인스턴스
  .select('first_name')
  .max('salary as max_salary')
  .join('salaries', 'employees.emp_no', 'salaries.emp_no')
  .groupBy('salaries.emp_no')
  .orderBy('max_salary', 'desc')
  .limit(10)
  .then(...)
```
`주의! 표준 promise가 아니라 자체 promise구현을 사용한다.`
> 특이한점: then 메소드를 호출하기 전까지는 sql문을 실행 시키지 않는다는 것  
위 성질을 이용해 then 메소드를 호출하지 않은채로 toString 메소드를 호출하면, 쿼리를 실행시키기 전에 쿼리빌더가 어떤 쿼리를 생성하는지 알수 있다.
```javascript
knex('salaries').limit(3).toString()
// select * from `salaries` limit 3
```

### SELECT
SELECT 메소드를 사용하면 원하는 컬럼만 불러온다.
```javascript
knex('salaries')
  .select('emp_no', 'salary')
  .limit(3)
  .toString()
// select `emp_no`, `salary` from `salaries` limit 3

//결과값
knex('salaries')
  .select('emp_no', 'salary')
  .limit(3)
  .then(console.log)

// 결과
[ { emp_no: 10001, salary: 60117 },
  { emp_no: 10001, salary: 62102 },
  { emp_no: 10001, salary: 66074 } ]
```
select 메소드의 인자로 넘기는 문자열 뒤에 as를 붙여서, 반환되는 객체들의 속성이름을 바꿀 수 있다.
```javascript
knex('salaries')
  .select('emp_no as e', 'salary as s')
  .limit(3)
  .then(console.log)

// 결과
[ { e: 10001, s: 60117 },
  { e: 10001, s: 62102 },
  { e: 10001, s: 66074 } ]
```
distinct 메소드를 사용해 중복제거를 할 수 있다.
```javascript
knex('employees')
  .distinct('first_name')
  .limit(3)
  .toString()

/*
select distinct `first_name` from `employees`
limit 3
*/
```
### WHERE
where 메소드를 사용해 where구문을 빌드할 수 있다.
```javascript
knex('salaries')
  .where('emp_no', 20000)
  .limit(3)
  .toString()

/*
select * from `salaries`
where `emp_no` = 20000
limit 3
*/
// 연산자를 사용할 수 있다.
knex('salaries')
  .where('emp_no', '>', 20000)
  .limit(3)
  .toString()

/*
select * from `salaries`
where `emp_no` > 20000
limit 3
*/
```
add연산자를 사용하기 위해 where를 여러번 사용하거나, andwhere메소드를 사용할 수 있다.
```javascript
knex('salaries')
  .where('emp_no', '>', 20000)
  .where('salary', '>', 150000)
  .andWhere('from_date', '<', '1999-01-01')
  .limit(3)
  .toString()

/*
select * from `salaries`
where `emp_no` > 20000
  and `salary` > 150000
  and `from_date` < '1999-01-01'
limit 3
*/
//또는 where 메소드에 객체를 넘길 수도 있습니다.
knex('employees')
  .where({
    first_name: 'Georgi',
    last_name: 'Facello'
  })
  .toString()

/*
select * from `employees`
where `first_name` = 'Georgi' and `last_name` = 'Facello'
*/
//not 연산자를 사용하기 위해 wherenot메소드를 사용한다.
knex('salaries')
  .whereNot('emp_no', '>', 20000)
  .limit(3)
  .toString()

/*
select * from `salaries`
where not `emp_no` > 20000
limit 3
*/
//OR 연산자를 사용하기 위해 orWhere 메소드를 사용할 수 있습니다. 또한 연산이 복잡한 경우에는 함수를 인자로 넘겨서 여러 where의 결합을 나타낼 수 있습니다.

knex('salaries')
  .where(function() {
    // arrow function을 사용하면 안 됩니다! 이유: this때문이다.
    this
      .where('emp_no', '>', 20000)
      .andWhere('salary', '>', 150000)
  })
  .orWhere(function() {
    this
      .where('emp_no', '<', 11000)
      .andWhere('salary', '<', 60000)
  })
  .limit(3)
  .toString()

/*
select * from `salaries`
where (`emp_no` > 20000 and `salary` > 150000)
  or (`emp_no` < 11000 and `salary` < 60000)
limit 3
*/
```
> arrow 함수 : this: 코드를 작성할 때, 바인드를 하더라도 this는 바뀌지 않는다.
그 밖의 메소드
- whereIn
- whereNotIn
- whereNull
- whereNotNull
- whereExists
### INSERT
```javascript
knex('employees')
  .insert({
    emp_no: 876543,
    first_name: 'fast',
    last_name: 'campus',
    birth_date: '1960-01-01',
    hire_date: '1980-01-01',
    gender: 'M'
  })
  .toString()

/*
insert into `employees` (`birth_date`, `emp_no`, `first_name`, `gender`, `hire_date`, `last_name`)
values ('1960-01-01', 876543, 'fast', 'M', '1980-01-01', 'campus')
*/
```
### UPDATE
```javascript
knex('employees')
  .where({emp_no: 876543})
  .update({last_name: 'five'})
  .toString()

/*
update `employees`
set `last_name` = \'five\'
where `emp_no` = 876543
*/
```
### DELETE
```javascript
knex('employees')
  .where({emp_no: 876543})
  .delete()
  .toString()

/*
delete from `employees`
where `emp_no` = 876543
*/
```
### ORDER BY
ORDER BY 메소드를 사용해서 구문을 빌드할 수 있다
```javascript
knex('employees')
  .orderBy('first_name', 'desc')
  .orderBy('last_name')
  .limit(3)
  .toString()

/*
select * from `employees`
order by `first_name` desc, `last_name` asc
limit 3
*/
```

### LIMIT, OFFSET
LIMIT, OFFSET메소들르 사용해서 각각 LIMIT, OFFSET구문을 빌드할 수 있다.
```javascript
knex('employees')
  .limit(3)
  .offset(100)
  .toString()

/*
select * from `employees`
limit 3 offset 100
*/
```

### 집계함수
knex 인스턴스의 count, max, min, sum, avg등의 메소드를 통해 집계함수를 빌드할 수 있다.
```javascript
knex('salaries')
  .count('*')
  .toString()

/*
select count(*) as `c` from `salaries`
*/

knex('salaries')
  .max('salary')
  .toString()

/*
select max(*) as `m` from `salaries`
*/

knex('salaries')
  .max('salary')
  .then(console.log)

// 결과
[ { 'max(`salary`)': 158220 } ]

knex('salaries')
  .max('salary as s')
  .then(console.log)

// 결과
[ { s: 158220 } ]
```

### GROUP BY & HAVING
GROUPBY 메소드를 통해 GROUP BY 구문을 빌드할 수 있다. 보통 위에서 다뤘던 집계함수와 함께 사용한다.
```javascript
knex('salaries')
  .select('emp_no')
  .max('salary as max_salary')
  .groupBy('emp_no')
  .limit(10)
  .toString()

/*
select `emp_no`, max(`salary`) as `max_salary`
from `salaries`
group by `emp_no`
limit 10
*/

// having 메소드를 통해 having 구문을 빌드할 수 있다. 사용법은 where메소드와 비슷하다.
knex('salaries')
  .select('emp_no')
  .max('salary as max_salary')
  .groupBy('emp_no')
  .having('max_salary', '>', 150000)
  .toString()

/*
select `emp_no`, max(`salary`) as `max_salary`
from `salaries`
group by `emp_no`
having `max_salary` > 150000
*/
```

### JOIN
JOIN 메소드를 이용해 INNER JOIN 구문을 빌드할 수 있다.
```javascript
knex('employees')
  .select('first_name', 'salary')
  .join('salaries', 'employees.emp_no', 'salaries.emp_no')
  .limit(10)
  .toString()

/*
select `first_name`, `salary` from `employees`
inner join `salaries` on `employees`.`emp_no` = `salaries`.`emp_no`
limit 10
*/
```

### 서브쿼리
단일 행 서브쿼리, 다중 행 서브쿼리 모두 자연스러운 방식으로 사용할 수 있다.
```javascript
// 1999년도 이전의 최고연봉보다 더 많은 연봉을 받은 사람들의 사원 번호를 출력합니다.
const subquery = knex('salaries')
  .max('salary')
  .where('from_date', '<', '1999-01-01')

knex('salaries')
  .distinct('emp_no')
  .where('salary', '>', subquery)
  .toString()

/*
select distinct `emp_no` from `salaries`
where `salary` > (
  select max(`salary`) from `salaries`
  where `from_date` < '1999-01-01'
)
*/

// first_name = 'Georgi' 를 만족하는 사람들의 last_name을 출력합니다.
const subquery = knex('employees')
  .select('emp_no')
  .where('first_name', 'Georgi')

knex('employees')
  .select('last_name')
  .whereIn('emp_no', subquery)
  .toString()

/*
select `last_name` from `employees`
where `emp_no` in (
  select `emp_no` from `employees`
  where `first_name` = 'Georgi'
)
*/
```

### UTILITY FUNCTION
#### .first()
knex를 통해 쿼리를 실행하면 보통 배열이 반환된다. 이 함수는 limit(1)처럼 하나의 행이 반환될 것이 확실한 경우에도 마찬가지이다.
```javascript
knex('employees')
  .select('emp_no')
  .limit(1)
  .then(console.log)

// 결과
[ { emp_no: 10001 } ]

// 매번 하나의 행이 들어있는 배열을 다루는 것은 불편하므로 아래와 같이 knex인스턴스의 first메소드를 이용해서 배열이 아닌 객체가 반환되도록 동작을 바꿀 수 있다.
knex('employees')
  .select('emp_no')
  .first()
  .then(console.log)

// 결과
{ emp_no: 10001 }
```
> 만약 반환된 행이 없다면 first의 결과는 undefined가 된다.

#### .raw()
직접 작성한 쿼리를 여러 메소드에서 사용할 수 있다.
```javascript
knex('users')
  .select(knex.raw('count(*) as user_count, status'))
  .where(knex.raw(1))
  .orWhere(knex.raw('status <> ?', [1]))
  .groupBy('status')
```
`주의!` 위예제와 같이 raw 관련 메소드는 특별한 방식으로 쿼리에 변수를 삽입하므로 SQL인젝션 공격에 무방비로 노출될 수 있다. 따라서 쿼리 문자열내에 변수를 삽입할 때는 `ES2015 TEMPLATE LITERAL을 사용하지 말고` RAW메소드가 제공하는 방식을 사용하라!