# Oracle

## 데이터베이스란

- 데이터들이 모여있는 집합소
- 데이터베이스에서 데이터들은 무작위로 들어있지않고 테이블에 담겨있다 (데이터베이스가 집이라면 테이블은 방)  
방의 용도가 있듯이(침실, 화장실, 놀이방 등) 용도를 정해서 테이블을 작성한다.

## 테이블의 구성

- 컬럼(세로) - 속성
- 로우=레코드=튜플(가로) - 속성에대한 값
- 하나의 컬럼은 도매인을 가지고있다.(도매인 = 컬럼이 가질 수 있는 범위)
- 속성간의 관계(1:1, 1:N, N:M) = 릴레이션

## 테이블의 제약조건(물리적)

- 데이터의 무결성을 보장하기 위함
  - 무결성보장 = 데이터의 일관성, 유효성, 정확성을 보장  
  = 잘못된 데이터가 들어오지 않게 막는다.

### PK(Primary Key) - 주 식별자(ex : 사원-사번, 학생-학번)의 무결성을 보장하는 제약
- 주식별자는 논리적 의미, PK는 물리적 의미
- 주식별자는 반드시 존재하지만 PK는 존재할 수도 있고 존재하지 않을 수도 있다.
- 테이블당 하나씩만 설정 가능, 중복과 NULL이 허용되지 않는다.
- 설정 명령어 = CONSTRAINT PK이름 PRIMARY KEY (PK컬럼);
- Unique Index가 자동으로 생성됨

### UK(Unique Key) = 고유키
- 테이블당 여러개 설정가능
- 중복은 허용되지 않지만 NULL은 허용이 된다.
- Unique Index가 자동으로 생성
- 설정 명령어 = CONSTRAINT UK이름 UNIQUE (UK컬럼);

### FK(Foreign Key) = 외래키
- 부모 테이블이 있다는 것을 의미
- 참조 컬럼과 데이터 타입도 일치해야함
- 부모테이블에 참조되는 컬럼은 PK나 UK로 설정이 되어 있어야 함
- 설정 명령어 = CONSTRAINT FK이름 FOREIGN KEY (FK컬럼) REFERENCES 부모테이블(참조컬럼);

## 실습
- SYS테이블 생성
- CREATE USER 이름 IDENTIFIED BY 비밀번호;
- 만든 유저에게 세션, 테이블, 리소스 권한 부여해야 함

### 쿼리문
#### INSERT문  
- INSERT INTO 테이블명 VALUES (컬럼값1, 컬럼값2, 컬럼값3 ...);  
또는 INSERT INTO 테이블명 (컬럼명1, 컬럼명2, 컬럼명3) VALUES(컬럼값1, 컬럼값2, 컬럼값3)

#### SELECT문
- SELECT * FROM 테이블명  
모두 조회
- SELECT 컬럼명 FROM 테이블명  
컬럼명에대한 정보만 출력
- SELECT * FROM 테이블명 WHERE 조건  
조건에 따른 정보만 출력
- SELECT * FROM 테이블명 ORDER BY 컬럼 DESC/ASC  
지정 컬럼 순서에 따라 출력(내림차순/오름차순)

#### ORDER BY절
- 데이터양이 많은 테이블에 남발할 경우 소트부하가 발생해 성능의 저하를 가져올 수 있음  
자주 등장하는 컬럼을 인덱스로 설정을 해두면 성능에 유리함
- 여러 컬럼을 지정할 수 있음
- ORDER BY 컬럼명 NULLS LAST/FIRST  
지정컬럼으로 정렬하고 컬럼의 NULL값을 첫번째로/마지막으로 보냄

#### JOIN문
- INNER JOIN
  - SELECT 컬럼명.A, 컬럼명.B FROM 테이블명.A, 테이블명.B WHERE A.컬럼명 = B.컬럼명;
- OUTER JOIN
  - INNER JOIN 끝에 (+) 추가
  - SELECT * FROM 테이블명 A (LEFT/RIGHT) OUTER JOIN 테이블명 B ON B.컬럼명 = A.컬럼명;
- INNER JOIN은 교집합, FULL OUTER JOIN은 합집합, RIGHT/LEFT JOIN은 기준테이블의 값 + 테이블과 기준테이블의 중복된 값

#### UPDATE문
- UPDATE 테이블명 SET 컬럼명 = 변경하려는 값 WHERE 컬럼명 = 조건값;
- 마지막에 COMMIT해야 영구적으로 테이블이 변경됨

#### DELETE문
- DELETE FROM 테이블
모든 속성 삭제
- DELETE FROM 테이블 WHERE 조건
- DELETE, TRUNCATE, DROP 차이점
  - DELETE 명령어는 데이터는 지워지지만 테이블 용량은 줄어 들지 않는다. 원하는 데이터만 지울 수 있다. 삭제 후 잘못 삭제한 것을 되돌릴 수 있다.
  - TRUNCATE 명령어는 용량이 줄어 들고, 인덱스 등도 모두 삭제 된다. 테이블은 삭제하지는 않고, 데이터만 삭제한다. 한꺼번에 다 지워야 한다. 삭제 후 절대 되돌릴 수 없다.
  - DROP 명령어는 테이블 전체를 삭제, 공간, 객체를 삭제한다. 삭제 후 절대 되돌릴 수 없다.

### NULL 관련 함수

 #### NVL함수
- 데이터가 NULL이면 대체값을 출력하는 함수
- NVL(NULL값 있는 컬럼명, 대체컬럼) 출력할 컬럼명
- SELECT쿼리를 수정해 연산을 사용할 때 에러가 발생할 수 있기때문에 사용해야함

 #### NULLIF함수
- 데이터가 NULL이면 입력한 대체값을 출력하는 함수
- NULLIF(NULL값 있는 컬럼명, '대체값') 출력할 컬럼명

 #### COALESCE함수
- 데이터가 NULL이면 NULL이 아닌 최초의 값을 출력
- COALESCE(NULL, NULL값 있는 컬럼명, 대체컬럼)

### UNION VS UNION ALL
- UNION은 교집합을 DISTINCT, 데이터타입이 같아야함
- UNION ALL은 교집합에대해 가감없이 출력
- UNION(MINUS, INTERSECT)은 SORT 연산을 발생시키는 명령어이기 때문에 굳이 중복값을 제거하지 않아도 되는 상황이거나 PK컬럼이 있어서 row의 ㅇ니크함이 보장되는 상황일때는 UNION을 UNION ALL로 대체를 해서 쿼리를 작성하는게 성능에 도움이 됨

### SYNONYM
- 동의어라는 의미
- 계정이 두개일때 각자의 고유 비밀번호가 부여됨 
- 타 계정으로 접속시 접속권한을 부여할 수 있음
- 사용할 계정에서 생성
- 보안상 생길 수 있는 문제를 방지


