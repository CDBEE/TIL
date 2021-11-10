# SQL(DDL)

# SQL 정의어

## CREATE

```sql
CREATE TABLE 테이블_이름
({속성_이름 데이터_타입 [NOT NULL],}
	[PRIMARY KEY(속성 이름),]
	[UNIQUE(속성_이름),]
	[FOREIGN KEY(속성_이름) REFERENCES 참조테이블(속성_이름)]
		[ON DELETE CASCADE | SET NULL | SET DEFAULT | NO ACTION]
		[ON UPDATE CASCADE | SET NULL | SET DEFAULT | NO ACTION],
	[CONSTRAINT 제약조건_이름 CHECK(속성_이름=범위값)]
);
```

- 괄호의 의미 : { } → 반복, [ ] → 생략 가능, | → 선택
- 모든 SQL 명령문은 ; 까지가 하나의 문장이다.
- CREATE TABLE 테이블_이름 : 테이블_이름으로 테이블 생성
- {속성_이름 데이터_타입}
    - 테이블을 구성하는 속성 수 만큼 속성 이름과 데이터 타입 기입
    - [NOT NULL] : 테이블 생성 시 특정 속성 값에 NULL이 없도록 지정
- PRIMARY KEY(속성_이름) : 테이블에서 기본키 속성을 지정할 때 사용
- UNIQUE(속성_이름) : 대체키 지정 시 사용, 속성의 모든 값이 고유한 값을 가지도록 할 때 사용
- FOREIGN KEY(속성_이름) REFERENCES 참조테이블(속성_이름)
    - 외래키 지정 시 사용
    - FOREIGN KEY(속성_이름) : 외래키로 사용 될 속성 이름
    - 참조테이블(속성_이름) : 참조할 테이블 이름과 속성 이름 기입
- CONSTRAINT 제약조건_이름 CHECK(속성_이름=범위값) : 테이블 생성 시 특정 속성에 대해 속성 값의 범위를 지정할 때 사용

### 외래키 지정 시 옵션

- ON DELETE : 참조 테이블의 튜플이 삭제되면 기본 테이블은 어떤 형태로 대처할지 선택
- ON UPDATE : 참조 테이블의 튜플이 변경되면 기본 테이블은 어떤 형태로 대처할 지 선택
- CASCADE : 참조 테이블의 튜플에 삭제/변화가 있는 경우 기본 테이블도 같이 연쇄적으로 삭제/변화가 이루어지게 함
- SET NULL : 삭제/변화가 있는 경우 기본 테이블의 관련 속성 값을 NULL로 세팅함
- SET DEFAULT : 삭제/변화가 있는 경우 기본 테이블의 관련 속성 값을 기본값으로 변경함
- NO ACTION : 아무런 행동을 하지 않음

### 스키마 정의

```sql
CREATE SCHEMA 스키마_이름 AUTHORIZATION 사용자;
```

### 도메인 정의

```sql
CREATE DOMAIN 도메인_이름 데이터_타입
	[DEFAULT 기본값]
	[CONSTRAINT 제약조건_이름 CHECK(VALUE IN(범위값))];
```

### 인덱스 정의

```sql
CREATE [UNIQUE] INDEX 인덱스_이름
	ON 테이블_이름(속성_이름 [ASC|DESC]
	[CLUSTER];
```

- UNIQUE : 중복을 허용하지 않도록 인덱스를 생성
- ON 테이블_이름(속성_이름)
    - 지정된 테이블의 속성으로 인덱스를 생성
    - [ASC|DESC] : 인덱스로 사용될 속성 값의 정렬 방법을 지정
- CLUSTER : 인접된 튜블들을 물리적인 그룹으로 묶어 저장 시 사용

## ALTER

```sql
ALTER TABLE 테이블_이름 ADD 속성_이름 데이터_타입 [DEFAULT];
ALTER TABLE 테이블_이름 ALTER 속성_이름 [SET DEFAULT];
ALTER TABLE 테이블_이름 DROP 속성_이름 [CASCADE|DEFAULT];
```

## DROP

테이블, 스키마, 도메인, 인덱스, 뷰, 제약조건 등을 삭제할 때 쓴다.

```sql
DROP TABLE 테이블_이름 [CASCADE | RESTRICT];
```

- CASCADE 시 삭제 요소가 참조 중이더라도 삭제되며 삭제할 테이블을 참조중인 테이블도 삭제된다.
- RESTRICT 사용 시 삭제할 요소가 참조 중이면 삭제되지 않는다.