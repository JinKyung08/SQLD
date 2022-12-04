# SQLD

###  ▷ SQL 기본

1. 관계형 데이터베이스 개요

- 데이터 베이스 

  - 특정 기업이나 조직 또는 개인이 필요에 의해 데이터를 일정한 형태로 저장해 놓은 것을 의미

  - 관계형 데이터베이스(Relational Database)

- SQL(Structured Query Language)
  - 관계형 데이터베이스에서 데이터 정의 데이터 조작 데이터 제어를 하기 위해 사용하는 언어
  - DML (데이터 조작어) - select, insert, update, delete
  - DDL (데이터 정의어) - create, alter, drop, rename
  - DCL (데이터 제어어) - grant, revoke
  - TCL (트랜잭션 제어어) - commit, rollback

- TABLE
  - 데이터는 관계형 데이터베이스의 기본 단위인 테이블 형태로 저장
  - 모든 자료는 테이블에 등록이 되고 우리는 테이블로부터 원하는 자료를 꺼내 올 수 있다.
  - 테이블은 어느 특정한 주제와 목적으로 만들어지는 일종의 집합
  - 세로 방향을 칼럼(Column), 가로 방향을 행(Row),  칼럼과 행이 겹치는 하나의 공간을 필드 (Field)
  - **정규화 - 테이블을 분할하여 데이터의 정합성을 확보하고, 불필요한 중복을 줄이는 프로세스**
  - **기본키(Primay Key) - 테이블에 존재하는 각 행을 한 가지 의미로 특정할 수 있는 한 개 이상의 칼럼**
  - **외부키(Foreign Key) - 다른 테이블의 기본키로 사용되고 있는 관계를 연결하는 칼럼**

- ERD(Entity Relationship Diagram)
  - EDR의 구성 요소 - 엔터티(Entity), 관계(Relationship),속성(Attribute)
  - IE 표기법 - 실선 : 식별관계 , 점선 : 비식별관계
  - Barker 표기법 - 수직바 : 식별관계



2. DDL(DATA DEFINITION LANGUAGE)

- 데이터 유형

  - CHARACTER(s)

    - 고정길이 문자열 정보 ( CHAR )
    - s는 기본길이 1바이트
    - s만큼 최대 길이를 갖고 고정 길이를 가지고 있으므로 할당된 변수 값의 길이가 s 보다 작을 경우에는 그 차이 길이만큼 공간으로 채워진다.

  - VARCHAR(s)

    - 가변 길이 문자열 정보 (VARCHAR)
    - s는 최소 길이 1바이트
    - s만큼 최대 길이를 갖지만 가변 길이로 조정이 되기 때문에 할당된 변수값의 바이트만 적용된다. (Limit 개념)

  - NUMERIC

    - 정수, 실수 등 숫자 정보 (Oracle - NUMBER, SQL Server- 10가지 이상의 숫자 타입을 가지고 있음)

  - DATETIME

    - 날짜와 시각 정보 (Oracle -DATE,  SQL Server- DATETIME)

    - Oracle - 1초단위 , SQL Server- 3.33ms 단위 관리

      

- CREATE TABLE

  - 테이블과 칼럼 정의

    - 테이블에 존재하는 모든 데이터를 고유하게 식별할 수 있으면서 반드시 값이 존재하는 단일 칼럼이나 칼럼의 조합들 후보키 중에 하나를 선정하여 기본키 칼럼으로 지정
    - 테이블과 테이블 간에 정의된 관계는 기본키 와 외부키 를 활용해서 (PRIMARY KEY) (FOREIGN KEY) 설정

  - CREATE TABLE

    ~~~
    CREATE TABLE ( 　 　테이블이름
    칼럼명 형식 1 DATATYPE [DEFAULT ],
    칼럼명 형식 2 DATATYPE [DEFAULT ],
    칼럼명 형식 2 DATATYPE [DEFAULT ]
    ) ;
    ~~~

    - 규칙

      - 테이블명은 객체를 의미할 수 있는 적절한 이름을 사용한다 가능한 단수형을 권고한다 . 

      - 다른 테이블명과 중복 X

      - 한 테이블내에 칼럼명 중복 X

      - 테이블 이름을 지정하고 각 칼럼들은 괄호"()" 로 묶어 지정

      -  각 칼럼들은 콤마"," 로 구분 , 마지막 칼럼 콤마 X

      - 테이블 생성문의 끝은 항상 세미콜론";" 으로 끝난다 

      - 일관성

      - 칼럼 뒤에 데이터 유형은 꼭 지정

      - 테이블명과 칼럼명은 반드시 문자로 시작

      - 벤더에서 사전에 정의한 예약어 는 쓸 수 없다

      -  A-Z, a-z, 0-9, _, $, # 문자만 허용된다

      - 테이블 생성시 대 소문자 구분 x, 기본적으로 테이블이나 칼럼명은 대문 자로 만들어진다.

      - DATETIME 데이터 유형에는 별도로 크기 지정 X

      - 문자 데이터 유형 - 반드시 가질 수 있는 최대 길이 표시

      - 칼럼에 대한 제약조건이 있으면 를 이용하여 추가할 수 있다

   - 제약조건(CONSTRAINT)

     - 사용자가 원하는 조건의 데이터만 유지하기 위한 즉, 데이터의 무결성을 유지하기 위한 데이터베이스의 보편적인 방법으로 테이블의 특정 칼럼에 설 정하는 제약
     - 종류
     
       - PRIMARY KEY (기본키) 
     
         - 데이터를 고유하게 식별하기 위한 기본키
     
         - 하나의 테일에 하나의 키본키 제약만 정의
         - 자동으로 UNIQUE 생성 
         - NULL X
         - 고유키 제약 & NOT NULL 제약
        - UNIQUE KEY (고유키)
  	     - 데이터를 고유하게 식별하기 위한 고유키
          - NULL 가능
        - NOT NULL
          - NULL X
          - 필수 입력
        - CHECK
          - 입력할 수 있는 값의 범위등을 제한 
          - TRUE or FALSE로 평가 할 수 있는 논리식을 지정
        - FOREIGN KEY(외래키)
          - 테이블 간의 관계를 정의하기 위해 기본키를 다른 테이블의 외래키로 복사하는 경우 외래키 생성
          - 참조 무결성 제약 옵션 선택할 수 있다.
     - NULL 의미
       - 공백이나 숫자 '0' 과는 전혀 다른 값
       - 조건에 맞는 데이터가 없을 때의 공집합과도 다르다.
       - **아직 정의되지 않은 미지의 값**
       - 현재 데이터를 입력하지 못하는 경우
     - DEFAULT 의미
       - 기본값
     
   - 생성된 테이블 구조 확인
  
     - Oracle  - DESCRIBE 테이블 명; or DESC 테이블명 ;
     - SQL Server -  sp_help ‘dbo.테이블명'
     
     
  
- ALTER TABLE
  
  - 칼럼을 추가 /삭제하거나 제약조건을 추가 /삭제하는 작업
  
  - ADD COLUMN
  
    ~~~
    ALTER TABLE 테이블명
    ADD 추가할 칼럼명 데이터유형;
    ~~~
  
  - DROP COLUMN
  
    - 테이블에서 필요 없는 칼럼을 삭제
  
    ~~~
    ALTER TABLE 테이블명
    DROP COLUMN 삭제할 칼러명;
    ~~~
  
  - MODIFY COLUMN
  
    - 칼럼에 대한 정의를 변경
  
    ~~~
    -ORACLE
    ALTER TABLE 테이블명
    MODIFY ( 칼럼명1 데이터 유형 [DEFAULT식] [NOT NULL], 
    		 칼럼명2 데이터 유형 ... );
    ~~~
  
    ~~~
    - SQL Server
    ALTER TABLE 테이블명
    ALTER ( 칼럼명1 데이터 유형 [DEFAULT식] [NOT NULL], 
    		칼럼명2 데이터 유형 ...)
    ~~~
  
    - 컬럼 변경시 고려사항
      - 해당 칼럼의 크기를 늘릴 수는 있지만 줄이지는 못한다 (기존 데이터 훼손될 수 있음)
      - 해당 칼럼이 값만 가지고 있거나 테이블에 아무 행도 없으면 칼럼의 폭을 줄일 수 있다
      - 해당 칼럼이 NULL값만을 가지고 있으면 데이터 유형을 변경할 수 있다
      - 해당 칼럼의 DEFAULT 값을 바꾸면 변경 작업 이후 발생하는 행 삽입에만 영향을 미치게 된다.
      - 해당 칼럼에 NULL 값이 없을 경우에만 NOT NULL 제약조건 추가 가능
  
  - RENAME COLUMN
  
    - 컬럼명 변경
  
    ~~~
    ALTER TABLE 테이블명
    RENAME COLUMN 변경해야 할 칼럼명 TO 새로운 칼럼명; 
    ~~~
  
    - SQL Server에서는 sp_rename 저장 프로시저를 이요하여 컬럼 이름 변경 가능
  
    ~~~
    sp_rename 변경해야 할 칼럼명, 새로운 칼럼명 , 'COLUMN';
    ~~~
  
  - DROP CONSTRAINT
  
    - 제약조건 삭제
  
    ~~~ 
    ALTER TABLE 테이블명  DROP CONSTRAINT 제약조건명 ; 
    ~~~
  
  - ADD CONSTRAINT
  
    - 제약조건 추가
  
    ~~~
    ALTER TABLE 테이블명
    ADD CONSTRAINT 제약조건명 제약조건(칼럼명);
    ~~~
  
  - RENAME TABLE
  
    - 테이블명 변경
  
    ~~~
    - Oracle
    RENAME 변경전 테이블명 TO 변경후 테이블명 ;
    ~~~
  
    ~~~
    - SQL Server
    sp_rename 변경전 테이블명, 변경후 테이블명;
    ~~~
  
  - DROP TABLE
  
    - 테이블 삭제
  
    ~~~
    DROP TABLE 테이블명 [CASCADE CONSTRAINT];
    ~~~
  
    - **DROP 명령어를 사용하면 테이블의 모든 데이터 및 구조를 삭제한다. CASCADE CONSTRAINT 옵션은 해당 테이블과 관계가 있었던 참조되는 제약조건에 대해서도 삭제한 다는 것을 의미**
  
  - TRUNCATE TABLE
  
    - 테이블 자체가 삭제 X , 모든 행 제거,  저장공간을 재사용 가능하도록 해제 
  
    ~~~ 
    TRUNCATE TABLE 테이블명;
    ~~~



3. DML(DATA MANIPULATION LANGUAGE)

-  입력 수정 삭제 조회

- INSERT

  - 데이터 입력

  ~~~
  ▶ INSERT INTO (COLUMN_LIST) 테이블명 (COLUMN_LIST) 
  VALUES (COLUMN_LIST에 넣을 VALUE_LIST);
  ▶ INSERT INTO 테이블명
  VALUES (전체 COLUMN에 넣을 VALUE_LIST);
  ~~~

- UPDATE

  - 수정

  ~~~
  UPDATE 테이블명
  SET 수정되어야 할 칼럼명 = 수정되기를 원하는 새로운 값;
  ~~~

- DELETE

  - 데이터 삭제

  ~~~
  DELETE [FROM] 삭제를 원하는 정보가 들어있는 테이블명; 
  ~~~

- SELECT

  - 조회

  ~~~
  SELECT [ALL/DISTINCT] 보고 싶은 칼럼명, 보고 싶은 칼럼명, ...
  FROM 해당 칼럼들이 있는 테이블명;
  
  SELECT *
  FROM 테이블명;
  ~~~

  - ALL : Default옵션이므로 별도로 표시하지 않아도 된다. 중복된 데이터가 있어도 모두 출력한다.
  - DISTINCT : 중복된 데이터가 있는 경우 1건으로 처리해서 출력한다.
  - WILDCARD  - (*) 애스터 리스크 : 모든 칼럼 정보를 보고싶을 경우 사용
  - ALIAS 
    - 별명 , 칼럼명 바로 뒤에 온다. 
    - 이중 인용부호 는 가 공백 특수문자를 포함할 경우와 대소문자 구분이 필요할 경우 사용된다.

- 산술 연산자와 합성 연산자
  - 산술 연산자
    - (), *, /, +, -  의 우선순위를 가진다
  - 합성 연산자
    - 문자 연결  : CONCAT (string1, string2) - (공통) , || - (Oracle),  '+' - (SQL Server)  

4.  TCL(TRANSACTION CONTROL LANGUAGE)

- 트랜잭션 개요

  -  데이터베이스의 논리적 연산단위

  - 밀접히 관련되어 분리될 수 없는 한 개 이상의 데이터베이스 조작을 가리킨다

  - **특성**

    - 원자성 - 트랜잭션에서 정의된 연산들은 모두 성공적으로 실행되던지 아니면 전혀 실행되지 않은 상태로 남아 있어야 한다. (all or nothing)

    - 일관성 - 트랜잭션이 실행되기 전의 데이터베이스 내용이 잘못 되어 있지 않다면 트래잭션이 실행된 이후에도 데이터베이스의 내용에 잘못이 있으면 안된다.

    - 고립성 - 트랜잭션이 실행되는 도중에 다른 트랜잭션의 영향을 받아 잘못된 결과를 만들어서는 안된다.

    - 지속성 - 트랜잭션이 성공적으로 수행되면 그 트랜잭션이 갱신한 데이터베이스의 내용은 영구적으로 저장된다.

      

- COMMIT

  - 입력한 자료나 수정한 자료에 대해서 또는 삭제한 자료에 대해서 전혀 문제가 없다고 판단 되었을 경우 COMMIT 명령어를 통해서 트랜잭션을 완료할 수 있다.
  - 단지 메모리 BUFFER에만 영향을 받았기 때문에 데이터의 변경 이전 상태로 복구 가능하다
  - COMMIT이나 ROLLBACK 이전의 데이터 상태 
    - 현재 사용자는 SELECT문장으로 결과를 확인 가능하다.
    - 다른 사용자는 현재 사용자가 수행한 명령의 결과를 볼 수 없다.
    - 변경된 행은 잠금(LOCKING)이 설정되어서 다른 사용자가 변경할 수 없다
  - COMMIT명령어는 이처럼  INSERT 문장, UPDATE 문장, DELETE  문장을 사용한 후에 이런 변경 작업이 완료되었음을 데이터베이스에 알려 주기 위해 사용
  - COMMIT 이후의 데이터 상태
    - 데이터에 대한 변경 사항이 데이터베이스에 반영된다 
    - 이전 데이터는 영원히 잃어버리게 된다 
    - 모든 사용자는 결과를 볼 수 있다 
    - 관련된 행에 대한 잠금이 풀리고 다른 사용자들이 행을 조작할 수 있게 된다.
  - SQL Server 는 기본적으로 AUTO COMMIT 모드 -> DML 수행후 COMMIT ROLLBACK 처리 필요 없음
  - SQL Server 트랜잭션 3가지 방식
    - AUTO COMMIT - 기본방식 , 자동 commit 수행, 오류발생 자동 rollback 수행
    - 암시적 트랜잭션 - oracle과 같은 방식 / 트랜잭션의 시작은 DBMS가 처리하고 트랜잭션의 끝은 사용자가 명시적으로 커밋 또는 롤백 처리 
    - 명시적 트랜잭션
      - 트랜잭션의 시작과 끝을 모두 사용자가 명시적으로 지정하는 방식
      - BEGIN TRANSACTION으로 트랜잭션을 시작 ,COMMIT TRANSACTION 또는 ROLLBACK TRANSACTION 으로 트랜잭션 종료
      - ROLLBACK 구문을 만나면 최초의 BEGIN TRANSACTION시점까지 모두 이 ROLLBACK이 수행된다

- ROLLBACK

  - 테이블 내 입력한 데이터나 수정한 데이터 삭제한 데이터에 대하여 COMMIT 이전에는 변경 사항을 취소할 수 있는데 데이터베이스에서는 롤백(ROLLBACK) 기능을 사용
  - SQL Server의 ROLLBACK
    - AUTO COMMIT이 기본 방식 
    - 임의적으로 롤백을 수행하려면 명식적으로 트랜잭션 선언해야 함
  - 데이터에 대한 변경 사항은 취소된다.
  - 이전 데이터는 다시 재저장된다.
  - 관련된 행에 대한 잠금(LOCKING) 이 풀리고 다른 사용자들이 행을 조작할 수 있게 된다.

- COMMIT 과 ROLLBACK 효과

  - 데이터 무결성 보장 
  - 영구적인 변경을 하기 전에 데이터의 변경 사항 확인 가능 
  - 논리적으로 연관된 작업을 그룹핑하여 처리 가능

- SAVEPOINT

  - 저장점
  - 롤백 할 때 전체 롤백X , 현 시점에서 SAVEPOINT까지 일부 롤백 할 수 있음
  - 복수의 저장점 정의 가능 / 동일 이름 저장점 정의 -> 나중에 정의한 저장점이 유효

  