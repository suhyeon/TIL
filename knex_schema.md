# KNEX - SCHEMA BUILDER
KNEX는 데이터를 읽어오고 조작하는 쿼리 뿐만 아니라 테이블을 생성하고 조작하는 쿼리도 지원한다.

> 스키마는 GETTER FUNCTION으로 반환된 객체는 재사용이 불가하다는 점을 주의!

## CREATE TABLE
다양한 타입의 컬럼을 만들 수 있다.
```javascript
knex.schema.createTable('table_name', function(table) {

  // INTEGER
  table.integer('column_name')

  // TEXT
  table.text('column_name')

  // VARCHAR(255) (255 생략 가능)
  table.string('column_name', 255)

  // FLOAT(8, 2) (8, 2 생략 가능)
  table.float('column_name', 8, 2)

  // DECIMAL(8, 2) (8, 2 생략 가능)
  table.decimal('column_name', 8, 2)

  // 저장은 TINYINT 타입으로 되나 JS 측에서 boolean으로 사용
  table.boolean('column_name')

  // DATETIME
  table.datetime('column_name')

  // TIMESTAMP (시각과 시간대를 같이 저장하는 타입)
  table.timestamp('column_name')

  // ENUM
  table.enum('column_name', ['M', 'F'])
})
```
제약조건은 다음과 같이 건다.
```javascript
knex.schema.createTable('table_name', function(table) {
  // `id` 라는 이름의 INTEGER UNSIGNED 컬럼을 만들고, PRIMARY KEY 및 AUTO_INCREMENT 제약조건을 지정합니다.
  table.increments();

  // `col1` 이라는 이름의 INTEGER 컬럼을 만들고, PRIMARY KEY 제약조건을 지정합니다.
  table.integer('col1').primary()

  // `col1`, `col2` 컬럼을 묶어서 PRIMARY KEY 제약조건을 지정합니다.
  table.primary(['col1', 'col2'])

  // `col2` 이라는 이름의 INTEGER UNSSIGNED 컬럼을 만듭니다.
  table.integer('col2').unssigned()

  // `col3` 이라는 이름의 INTEGER 컬럼을 만들고 기본값을 0으로 설정합니다.
  table.integer('col3').defaultTo(0)

  // `created_at` 컬럼을 만들고 기본값을 현재 시각으로 설정합니다.
  table.timestamp('creatd_at').defaultTo(knex.fn.now())

  // `col4` 이라는 이름의 INTEGER 컬럼을 만들고 NOT NULL 제약조건을 지정합니다.
  table.integer('col4').notNullable()

  // `other_table_id` 컬럼을 `other_table` 테이블의 `id`에 대한 FOREIGN KEY로 지정합니다.
  table.foreign('other_table_id').references('other_table.id')

  // 참조하고 있는 `other_table`의 레코드가 삭제되었을 때 어떻게 동작할 것인지를 지정할 수도 있습니다.
  table.foreign('other_table_id').references('other_table.id').onDelete('RESTRICT')

  // `col1` 컬럼에 UNIQUE 제약조건을 지정합니다.
  table.unique('col1')

  // `col1`, `col2` 컬럼을 묶어서 UNIQUE 제약조건을 지정합니다.
  table.unique(['col1', 'col2'])
})
```

## ALTER TABLE
이미 만들어진 테이블을 수정한다.
```javascript
knex.schema.alterTable('table_name', function(table) {
  // 컬럼의 이름을 변경합니다.
  table.renameColumn('old_column_name', 'new_column_name')

  // 새 컬럼을 추가합니다.
  table.integer('new_int_column')

  // 컬럼을 새로 생성하는 것이 아니라 이미 존재하는 컬럼을 수정하는 것임을 명시하기 위해
  // `alter` 메소드를 사용합니다.
  table.integer('old_int_column').notNullable().alter()
})
```

### 쓰기 vs 읽기
읽기가 많이 일어나는 서비스 : 인덱스를 걸어주는 것이 맞다.  
쓰기가 많이 일어나는 서비스 : 인덱스를 걸어주지 않는 것이 맞다.
> 속도차이가 나기 때문. 인덱스가 있다면 쓸때마다 그 인덱스를 다시 정렬하는 경우가 많기 때문에 쓰기가 많이 일어나는 서비스라면 인덱스가 없어야 맞다.

## MIGRATION
데이터 구조 변경, 재구축

