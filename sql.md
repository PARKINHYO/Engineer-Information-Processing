## 데이터 조회(SELECT) 절

### 테이블 구조 조회
```sql
DESC 테이블명
```

### 테이블에서 데이터 검색

학생 테이블에서 나이가 10 이상인 이름, 나이 컬럼을 출력
```sql
SELECT 이름, 나이 
FROM 학생
WHERE 나이 >= 10;
```

학생 테이블에서 모든 컬럼을 출력

```sql
SELECT *
FROM 학생;
```

### 테이블에서 중복값을 제거하고 검색

사원 테이블에서 사원번호를 출력하되, 중복되는 사원번호는 한 번만 출력
```sql
SELECT DISTINCT 사원번호
FROM 사원;
```

## WHERE(조건)절

### WHERE절에서 조건이 상수인 경우

사원 테이블에서 부서번호가 90인 사원번호, 이름, 부서번호를 출력

```sql
SELECT 사원번호, 이름, 부서번호
FROM 사원
WHERE 부서번호 = 90;
```

### WHERE절 조건에 조건이 문자열인 경우

학생 테이블에서 이름이 Gildong인 학생의 이름, 학번, 교실을 출력

```sql
SELECT 이름, 학번, 교실
FROM 사원
WHERE 이름 = 'Gildong';
```

### WHERE절 조건에 BETWEEN 연산자 사용

사원 테이블에서 월급이 2500이상 3500이하인 사원의 이름, 월급 출력

```sql
SELECT 이름, 월급
FROM 사원
WHERE 월급 BETWEEN 2500 AND 3500;
```

### WHERE절 조건에 IN 연산자 사용

사원 테이블에서 사수번호가 100, 101, 201인 사원의 사원번호, 이름, 월급, 사수번호를 출력

```sql
SELECT 사원번호, 이름, 월급, 사수번호
FROM 사원
WHERE 사수번호 IN(100, 101, 201);
```

### WHERE절 조건에 패턴 연산자(_, %) 사용

사원 테이블에서 이름의 두번째 자리가 o로 시작하는 모든 사원의 이름 출력
```sql
SELECT 이름 
FROM 사원
WHERE 이름 LIKE '_o%';
```

_ : 한자리의 문자
% : 0~n자리 문자
%o% : o가 들어가는 모든 데이터를 검색

employees 테이블에서 입사월이 MAY(5월)인 직원들의 입사일 출력

```sql
SELECT 입사일
FROM employees
WHERE 입사일 LIKE '%MAY%';
```

### WHERE절 조건에 IS NULL / IS NOT NULL 사용

사원 테이블에서 사수번호가 없는 사원의 이름, 사수번호를 출력

```sql
SELECT 이름, 사수번호
FROM 사원
WHERE 사수번호 IS NULL;
```

IS NULL : 이 없다
IS NOT NULL : 이 없지 않다(있다)

### WHERE절 조건에 논리 연산자(AND, OR, NOT) 사용

사원 테이블에서 월급이 10000 이상이고, 직무번호에 'MAN'이 들어가는 사원의 사원번호, 이름, 직무번호, 월급을 출력

```sql
SELECT 사원번호, 이름, 직무번호, 월급
FROM 사원
WHERE 월급 >= 10000 AND 직무번호 LIKE '%MAN%';
```

사원 테이블에서 월급이 10000 이상이거나, 직무번호에 'MAN'이 들어가는 사원의 사원번호, 이름, 직무번호, 월급을 출력

```sql
SELECT 사원번호, 이름, 직무번호, 월급
FROM 사원
WHERE 월급 >= 10000 OR 직무번호 LIKE '%MAN%';
```

NOT 연산자 : 조건이 아닌 것

⭐사원 테이블에서 이름에 'A'가 들어가지 않는 사원의 사원번호, 이름, 직무번호, 월급을 출력

```sql
SELECT 사원번호, 이름, 직무번호, 월급
FROM 사원
WHERE 이름 NOT LIKE '%A%';
```

## ORDER BY절(정렬)

내용 출력 시, 정렬하여 출력하는 문법
위치 : SELECT 구문의 가장 마지막에 위치
기본값은 ASC(오름차순)으로 적용

<종류>
ASC : 오름차순
DESC : 내림차순

### 내림차순 기본구문

사원 테이블에서 이름, 직무번호, 부서번호, 입사일을 입사일 기준으로 내림치순하여 출력

```sql
SELECT 이름, 직무번호, 부서번호, 입사일
FROM 사원
ORDER BY 입사일 DESC;
```

### 아무런 조건을 붙이지 않았을 시, 오름차순으로 정리됨

사원 테이블에서 사원번호, 이름, 월급을 월급 기준으로 오름차순하여 출력

```sql
SELECT 사원번호, 이름, 월급
FROM 사원
ORDER BY 월급;
```

### 오름차순과 내림차순이 교집합일 때

사원 테이블에서 사원번호, 부서번호, 월급을 부서번호 기준으로 오름차순한 후, 월급 기준으로 내림차순하여 출력
정렬 기준이 여러개인 경우 왼쪽에 있는 정렬기준이 우선 적용되며, 정렬 기준에서 같은 값을 가진 행이 있을 경우 후 순위의 정렬기준이 적용

```sql
SELECT 사원번호, 부서번호, 월급
FROM 사원
ORDER BY 부서번호, 월급 DESC;
```

## GROUP BY절, HAVING 절

출력할 데이터를 그룹으로 묶는 조건을 설정하는 GROUP BY - HAVING 절. 
GROUP BY가 보이면 조건 자리에 HAVING이 와야한다. 

### 그룹 함수

* 그룹단위로 값을 받아서 연산하는 함수
* GROUP BY를 사용하지 않을 때, 하나의 테이블 = 하나의 그룹이 됨.
* NULL 값을 가진 행은 연산에서 제외함
* 중복 값을 제거하는 DISTINCT도 사용 가능

![image](https://user-images.githubusercontent.com/47745785/100376221-7860e680-3052-11eb-97b2-e691d2ac94e2.png)

사원 테이블의 전체 행의 개수 출력

```sql
SELECT COUNT (*)
FROM 사원;
```

### GROUP BY절

* 테이블의 행을 그룹으로 묶을 때 그룹을 묶는 기준을 설정
* 기준 컬럼의 값이 동일한 행끼리 하나의 그룹으로 묶는다. 
* 기준 컬럼의 값이 그룹의 이름이 된다.
* 쿼리 구문에 WHERE절이 있는 경우 WHERE 행을 먼저 선택한 뒤 그룹이 묶이게 된다. 

기본 문법
```sql
SELECT 출력할 컬럼명, 그룹 함수
FROM 검색할 테이블명
[WHERE 조건]
[GROUP BY 그룹으로 묶을 컬럼명]
[HAVING GROUP조건]
[ORDER BY 정렬기준 컬럼명];
```

사원 테이블에서 같은 부서번호를 갖는 사람들을 그룹으로 묶어서 그룹 번호, 월급의 평균을 출력

```sql
SELECT 부서번호, AVG(월급)
FROM  사원
GROUP BY 부서번호;
```

사원 테이블에서 부서번호가 40보다 큰 사원을 부서번호와 직무번호로 묶어서 부서번호, 직무번호, 월급의 평균을 부서번호를 기준으로 오름차순하여 출력

```sql
SELECT 부서번호, 직무번호, AVG(월급)
FROM 사원
WHERE 부서번호 > 40
GROUP BY 부서번호, 직무번호
ORDER BY 부서번호;
```

### HAVING 절

* GROUP BY절을 통해 만들어진 그룹에 제한을 거는 절
* HAVING절의 조건의 기준으로 그룹함수만 사용가능하다. 
* WHERE절에는 그룹함수를 기준으로 사용할 수 없다.

사원 테이블에서 사수번호를 알 수 없는 사원은 제외하고 사수번호로 그룹화하여 사수번호별 최소 월급을 출력하되, 최소 월급이 6000 이상인 그룹을 최소 월급을 기준으로 내림차순으로 정렬하여 출력

```sql
SELECT 사수번호, MIN(월급)
FROM 사원
WHERE 사수번호 IS NOT NULL
GROUP BY 사수번호
HAVING MIN(월급) >= 6000
ORDER BY MIN(월급) DESC;
```



## 데이터 조작어(DML) : INSERT, UPDATE, DELETE 구문

### INSERT

테이블에 새로운 행 정보를 입
력할 때 사용하는 구문

```sql
INSERT INTO 학생(학과, 학번, 이름, 학년)
VALUES ('컴퓨터공학', 20201234, '홍길동', 1);
```

만약, 학생 테이블의 컬럼의 개수와 입력할 값의 개수가 일치할 경우 다음과 같이 입력 가능

```sql
INSERT INTO 학생 VALUES('컴퓨터공학', 20201234, '홍길동', 1);
```

### UPDATE

기존 행의 정보를 갱신할 때 사용하는 구문

SET 자리에 수정할 컬럼=값 리스트는 콤마를 사용하여 나열하고, AND를 사용하지 않음. 
학생 테이블에서 이름이 홍길동인 학생의 학점을 'A'로 갱신

```sql
UPDATE 학생
SET 학점='A'
WHERE 이름='홍길동';
```

사원 테이블에서 사원번호가 113인 사원의 부서번호를 50, 급여를 3000으로 갱신

```sql
UPDATE 사원
SET 부서번호=50,급여=3000
WHERE 사원번호=113;
```

### DELETE

기존의 행의 정보를 삭제할 떄 사용하는 구문

부서 테이블에서 부서번호가 300인 부서를 삭제
```sql
DELETE FROM 부서 WHERE 부서번호=300.
```

## 데이터 정의어(DLL) : CREATE, ALTER, DROP

### CREATE
새로운 테이블, 오브젝트(VIEW, INDEX, DATABASE 등)를 생성할 때 사용. 

기본 문법

```sql
CREATE TABLE 테이블명(
    컬럼명1 데이터타입(컬럼사이즈) [제약조건],
    ...
    컬럼명n번째 데이터타입(컬럼사이즈) [제약조건] );
```

순번(INT), 이름(VARCHAR(20)), 직무번호(INT), 입사일(DATE), 급여(INT) 컬럼이 존재하는 사원 테이블 생성

```sql
CREATE TABLE 사원(
    순번 INT,
    이름 VARCHAR(20),
    직무번호 INT,
    입사일 DATE,
    급여 INT);
```

제약조건(constraint)
테이블 생성 시, 각 컬럼에 제약 조건을 설정하여 조건에 맞지 않는 데이터는 DB차원에서 입력되지 않도록 제한하는 조건을 말한다.

NOT NULL : 칼럼에 NULL 값을 허용하지 않음
UNIQUE : 컬럼에 중복 값을 허용하지 않음
PRIMARY KEY(PK, 기본키) : 중복 값과 NULL 값을 허용하지 않음. 테이블 당 한번만 사용 가능. 테이블을 대표하는 컬럼에 설정.

⭐다음 제약 조건에 맞추어 member 테이블을 생성하시오. 
idx는 정수형으로 기본키로 설정한다. 
id는 가변문자열형 10자리로 NULL 값과 중복 값을 가질 수 없다.
name은 가변분자열형 10자리로 널값을 가질 수 없다. 
job은 가변문자열형 20자리이다. 
email은 가변문자열형 30자리이고, 중복값을 가질 수 없다. 
phone은 가변문자열형 20자리이고, NULL값과 중복값을 가질 수 없다. 
start_date는 날짜형으로 지정. 

```sql
CREATE TABLE member(
    idx INT constraint mem_id_pk PRIMARY KEY,
    id VARCHAR(10) NOT NULL, UNIQUE,
    name VARCHAR(10) NOT NULL, 
    job VARCHAR(20),
    email VARCHAR(30) UNIQUE,
    phone VARCHAR(20) UNIQUE, NOT NULL,
    start_date DATE);
```

idx 컬럼 뒤에 붙은 constraint mem_id_pk는 제약조건을 붙일 경우 제약조건의 이름을 뜻하고 유지 보수를 위해 입력이 권장되지만, 입력하지 않아도 제약조건은 설정된다. 

### ALTER
테이블 생성 이후, 테이블을 변경할 때 사용하는 구문

테이블에 컬럼 추가

```sql
ALTER TABLE 테이블 이름 
ADD (컬럼명 데이터타입(데이터크기));
```

학생 테이블에 학점 컬럼을 추가( 학점 컬럼은 : 크기 5인 가변문자열형으로 지정. )
```sql
ALTER TABLE 학생
ADD (학점 VARCHAR(5));
```

테이블의 기존 컬럼 수정

```sql
ALTER TABLE 테이블 이름
MODIFY (컬럼명 데이터타입(데이터크기));
```

학생 테이블의 이름 컬럼의 데이터형을 문자열형에서 가변 문자열형(30)으로 수정

```sql
ALTER TABLE 학생
MODIFY (이름 VARCHAR(30));
```

테이블의 기존 컬럼 삭제

```sql
ALTER TABLE 테이블명 
DROP COLUMN 컬럼명;
```

학생 테이블의 학점 컬럼을 삭제

```sql
ALTER TABLE 학생
DROP COLUMN 학점;
```


### DROP
테이블 삭제 명령어

```sql
DROP TABLE 테이블명;
```

학생 테이블을 삭제

```sql
DROP TABLE 학생;
```

⭐학생 테이블을 삭제하되, 테이블을 참조하는 외래키로 엮인 테이블을 모두 삭제. 테이블명 뒤에 CASCADE CONSTRAINTS를 붙임. 

```sql
DROP TABLE 학생 CASCADE CONSTRAINTS;
```

## 데이터 정의어(DDL) - VIEW, INDEX

### VIEW

VIEW는 물리적으로 존재하는 테이블이 아니라 논리적으로 존재하는 테이블

뷰 생성
```sql
CREATE [OR REPLACE] [FORCE | NOFORCE] VIEW 뷰 이름
AS 서브쿼리;
```

뷰 삭제

```sql
DROP VIEW 뷰이름;
```

서브 쿼리란? 
하나의 쿼리문 내에 포함되어 있는 또 하나의 쿼리문
SELECT절, WHERE절, FROM절 안에 쿼리문이 들어가면 통칭하여 서브쿼리라고 함. 

⭐선택과목 B 테이블에서 'MATH'를 선택한 학생들의 이름을 찾아, student A 테이블에서 모든 정보를 조회

```sql
SELECT *
FROM student A
WHERE A.student_name
IN (SELECT B.student_name
   FROM subject B
   WHERE B.subject_name = 'MATH');
```

⭐사원 테이블에서 부서번호가 80인 직원들의 아이디, 이름, 월급을 조회하는 회원 80 VIEW 생성

```sql
CREATE VIEW 회원 80
AS
 SELECT 아이디, 이름, 월급
 FROM 사원
 WHERE 부서번호=80;
```

### INDEX

INDEX는 검색 속도를 높이기 위해 사용하는 객체

INDEX 생성

```sql
CREATE INDEX 인덱스명
ON 테이블명(인덱스지정할 컬럼명);
```

⭐학생 테이블의 학번을 idx_num으로 인덱스 지정

```sql
CREATE INDEX idx_num
ON 학생(학번);
```

INDEX 삭제

```sql
DROP INDEX 인덱스명;
```

## 데이터 제어어(DCL) - GRANT, REVOKE

### GRANT
DB를 조작할 수 있는 권한을 부여
권한은 DML, DDL, ... 등등 100개 정도 존재

```sql
GRANT 권한
ON 테이블 TO 권한부여할계정명 [WITH GRANT OPTION];
```

⭐APPUSER 계정에 학생 테이블에 대한 SELECT, INSERT, UPDATE, DELETE를 수행할 수 있는 권한을 부여

```sql
GRANT SELECT, INSERT, UPDATE, DELETE
ON 학생 TO APPUSER:
```

APPUSER 계정에 학생 테이블에 대한 SELECT, INSERT, UPDATE, DELETE를 수행 할 수 있는 권한을 부여하되, APPUSER가 다른 유저에게 자신이 받은 권한을 줄 수 있도록 설정

```sql
GRANT SELECT, INSERT, UPDATE, DELETE
ON 학생 TO APPUSER WITH GRANT OPTION;
```

### REVOKE

GRANT로 부여한 권한을 회수

```sql
REVOKE 권한 ON 테이블 FROM 권한을회수할계정명 [CASCADE CONSTRAINTS];
```

APPUSER 계정에 부여된 권한 중, 학생 테이블에서 DELETE를 수행할 수 있는 권한을 회수 

```sql
REVOKE DELETE
ON 학생 FROM APPUSER;
```

APPUSER 계정에 부여된 권한 중, 학생 테이블에서 DELETE를 수행할 수 있는 권한을 회수하고 만약, APPUSER가 다른 유저에게 DELETE 권한을 부여했다면 함께 회수

```sql
REVOKE DELETE
ON 학생 FROM APPUSER CASCADE CONSTRAINTS;
```







