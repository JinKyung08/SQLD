# SQLD

###  ▷ SQL 기본

5. WHERE 절

- WHERE절은 FROM절 다음에 위치 

- 조건식

  - 칼럼명 

  - 비교연산자

  - 문자,숫자,표현식

  - 비교 칼럼명 (join 사용시)
  
- 연산자 종류

  - 비교연산자 ( =,  >,  >=, < , <=)
  - SQL연잔사 (BETWEEN a AND b, Like '비교문자열', IS NULL)
  - 논리연산자 (AND, OR, NOT)
  - 부정비교연산자 ( !=, ^=, <>, NOT 칼럼명 =, NOT 칼럼명 >)
  - 부정 SQL연산자 (NOT BETWEEN a AND b, NOT IN (list), IS NOT NULL)

- 연산자의 우선순의

  1. 괄호()
  2. NOT 연산자
  3. 비교연산자, SQL 비교 연산자
  4. AND
  5. OR

- 문자 유형 비교 방법

  - 비교연산자의 양쪽이 모두 CHAR 유형 타입인 경우
    - 길이가 서로 다른 CHAR형 타입이면 작은 쪽에 SPACE를 추가 하여 길이를 같게 한 후 비교
    - 서로다른 문자가 나올 때까지 비교
    - 달라진 첫 번째 문자의 값에 따라 크기를 결정
    - BLANK의 수만 다르다면 서로 값은 값으로 결정
  - 비교연산자의 양쪽이 모두 VARCHAR 유형 타입인 경우
    -  서로 다른 문자가 나올 때까지 비교
    - 길이가 다르다면 짧은 것이 끝날 때까지만 비교한 후에 길이가 긴 것이 크다고 판단
    - 길이가 같고 다른 것이 없다면 같다고 판단
    - VARCHAR는 NOT NULL까지 길이를 말한다.

  - 상수값과 비교할 경우
    - 상수 쪽을 변수 타입과 동일하게 바꾸고 비교
    - 변수 쪽이 CHAR 유형 타입이면 위의 CHAR유형 타입의 경우를 적용
    - 변수 쪽이 VARCHAR 유형 타입이면 위의 VARCHAR유형 타입의 경우를 적용

- 와일드 카드의 종류

  - % - 0개 이상의 어떤문자를 의미
  - _  - 1개인 단일 문자를 의미

  

- ROWNUM

  - 임시로 부여되는 일련번호
  - WHERE 절에서 행의 개수를 제한하는 목적으로 사용
  - 고유한 키나 인덱스 값을 만들 수 있다

- TOP

  - TOP절을 사용하여 결과 집합으로 출력되는 행의 수를 제한할 수 있다.

  ~~~
  TOP (Expression) [PERCENT] [WITH TIES]
  ~~~

  - Expression - 반환할 행의 수를 지정하는 숫자이다
  - PERCENT - 쿼리 결과 집합에서 처음Expression%의 행만 반환됨을 나타낸다
  - WITH TIES -  ORDER BY절이 지정된 경우에만 사용할 수 있으며, TOP N(PERCENT)의 마지막 행과 같은 값이 있는 경우 추가 행이 출력되도록 지정할 수 있다.



6.  함수(FUNCTION)

- 내장 함수 (BUILT-IN FUNCTION) - 벤더에서 제공하는 함수

~~~
함수명 ( 칼럼이나 표현식 [, Arg1, Arg2, ... ])
~~~

- 단일행 함수

  - 문자형 함수
    - LOWER - 소문자로 변경
    - UPPER - 대문자로 변경
    - SUBSTR/SUBSTRING - m위치에서 n개의 문자길이에 해당하는 문자를 리턴 / n생략 - 마지막문자까지
    - LENGTH/LEN - 문자열의 개수
    - LTRIM - 문자열의 첫문자부터 확인해서 지정문자가 나타나면 해당문자 제거
      - SQL - Server : 지정문자 사용 x,공백만 제거
    - RTRIM - 문자열의 마지막문자부터 확인해서 지정문자가 나타나면 해당문자 제거
      - SQL - Server : 지정문자 사용 x,공백만 제거
    - TRIM - 문자열에서 머리말, 꼬리말, 또는 양쪽에 있는 지정문자 제거
      - SQL - Server : 지정문자 사용 x,공백만 제거
    - ASCH - ASCII 코드번호로 변경
    - CONCAT - 문자연결
  - 숫자형 함수
    - ABS - 절대값
    - MOD - 나누기
    - ROUND - 반올림
    - TRUNC - 소수 m자리에서 잘라서 버림 / m 생략 - 디폴트 0
    - SIGN -양수,음수, 0 구별
    - CEIL/CEILING - 숫자보다 크거나 같은 최소 정수 리턴
    - FLOOR - 숫자보다 작거나 같은 최대 정수 리턴
    - EXP, POWER , SQRT, LOG, LN  - 숫자의 지수, 거듭제곱,제곱근,자연로그 값은 리턴
    - SIN, COS, TAN - 숫자의 삼각함수값을 리턴
  - 날짜형 함수
    - SYSDATE/GETDATE / GETDATE() - 현재날짜와 시각 출력
    - EXTRACT/DATEPART - 날짜데이터에서 년/월/일 데이터 출력 / 시간,분,초 도 가능
    -  TO_NUMBER(TO_CHAR(d, 'YYYY'|'MM'|'DD')) / YEAR|MONTH/DAY - 년/월/일 데이터 출력
  - 변환형 함수
    - TO_NUMBER - alphanumeric 문자열을 숫자로 변환
    - TO_CHAR - 숫자나 날짜를 주어진 FORMAT형태로 문자열 타입으로 변환
    - TO_DATE - 문자열을 주어진 FORMAT형태로 날짜타입으로 변환
    - CAST (expression AS data_type[(length)]- expression을 목표 테이터 유형으로 변환
    - CONVERT (data_type [(length)], expression [style]) -expression을 목표 테이터 유형으로 변환
  - NULL 관련 함수
    - NVL/ISNULL  (표현식1, 표현식2) - 표현식1이 null 이면 표현식2 출력 (데이터타입 같아야 함)
    - NULLIF (표현식1, 표현식2) - 표현식1이 표현식2와 같으면 NULL , 같지않으면 표현식1 리턴
    - COALESCE (표현식1, 표현식2, ...) -  임의의 개수 표현식에서 NULL이 아닌 최초의 표현식을 나타냄, 모든 표현식이 NULL이라면 NULL 리턴

- 단일행 함수의 중요한 특징

  - SELECT, WHERE, ORDER BY 절에 사용가능
  - 각 행들에 대해 개별적으로 작용하여 데이터 값들을 조작하고, 각각의 행에 대한 조작 결과를 리턴
  - 여러 인자를 입력해도 단 하나의 결과만 리턴
  - 함수의 인자로 상수 변수 표현식이 사용 가능하고 하나의 인수를 가지는 경우도 있지만 여러 개의 인수를 가질 수도 있다
  - 특별한 경우가 아니면 함수의 인자로 함수를 사용하는 함수의 중첩이 가능

  

  