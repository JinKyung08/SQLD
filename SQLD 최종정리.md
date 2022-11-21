# SQLD 자격증

SQL 명령문 개괄

- 연산 순서 정렬

  - From- where - group by - having - select - orderby
  - DML - insert ,select, delete, update
  - DDL - alter, create, modify, drop
  - TCL - rollback, commit
  - DCL - grant, revoke

- SELECT 

  - distinct (집약) - > 10,10,20,20,30,->10, 20 , 30 (중복제거)

  - distinct deptno, mgr ≒ groupby deptno, mgr

  - AS -> Select -  as생략가능 , 컬럼명에 띄어쓰기 있는 경우 ex)"직원 번호"

    ​	 -> From - as 사용불가 

  - concat - concat (().()) 인수가 2개 - '+' : SQL server ,'||' : Oracle

- 논리연산자 

  - And  - A and B
  - or - A or B
  - not 
  - **연산순위** (nao)
    1. not
    2. and 
    3. or

- SQL 연산자
  - A between 1 and 2 :  1<= A <=2
  - A in (1,2,3) : A =1 or A=2 or A=3

- **★Like★**
  - _ : 미지의 한글자
  - % :  0이상의 글자
    - _L% : 이름의 두번째 글자가 L인 사람
  - escape : ex) ename like 'A_A' => 'A@\__A'  '@'_ escape '@' 
  - 와일드 카드(_,%)를 문자로 취급 해주는 함수 
  - Rownum (oracle) - where 조건에서 rownum =1 포함
  - top  (SQLserver) - select절 select TOP(n) <컬럼명> :  상위n개를 가져오겠다