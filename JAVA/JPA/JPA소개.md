# JPA 시작

회원 테이블

```sql
CREATE TABLE MEMBER(
	ID VARCHAR(255) NOT NULL,
	NAME VARCHAR(255),
	AGE INTEGER,
	PRIMARY KEY (ID)
)
```

회원 클래스

```java
Public class Member{
	private String id;
	private String username;
	private Integer age;
	
	//Getter, Setter
	//~
}
```

| 매핑정보 | 회원 객체 | 회원 테이블 |
| --- | --- | --- |
| 클래스와 테이블 | Member | MEMBER |
| 기본 키 | id | ID |
| 필드와 컬럼 | username | NAME |
| 필드와 컬럼 | age | AGE |

매핑 정보가 포함 된 회원 클래스

```java
@Entity
@Table(name="MEMBER")
public class Member{
	@Id
	@Column(name="ID")
	private String id;
	
	@Column(name="NAME")
	private String username;
	
	@Column(name="AGE")
	private Integer age;
}
```

- @Entity : 이 클래스를 테이블과 매핑한다고 JPA에게 알려준다. 이렇게 @Entity가 사용된 클래스를 엔티티 클래스라고 한다.
- @Table : 엔티티 클래스에 매핑할 테이블 정보를 알려준다. 여기선 name 소겅을사용해서 Member 엔티티를 MEMBER 테이블에 매핑했다. 이 어노테이션을 생략하면 클래스 이름을 테이블 이름으로 매핑한다.
- @Id : 엔티티 클래스의 필드를 테이블의 기본 키에 매핑한다.
- @Column : 필드를 컬럼에 매핑한다. 여기서는 name 속성을 사용해서 Member 엔티티의 username 필드를 MEMBER 테이블의 name 컬럼에 매핑했다.
- 매핑 정보가 없는 필드 : 매핑 어노테이션 생략 시 필드명을 사용해서 컬럼명으로 매핑한다. 여기서는 필드명이 age이므로 age 컬럼으로 매핑했다. 이때 데이터베이스가 대소문자를 구분하지 않는다고 가정했다. 대소문자를 구분하는 데이터베이스 사용 시 명시적으로 매핑해야한다.