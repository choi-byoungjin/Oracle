# Oracle

##데이터베이스란 - 데이터들이 모여있는 집합소

##데이터베이스에서 데이터들은 무작위로 들어있지않고 테이블에 담겨있다 (데이터베이스가 집이라면 테이블은 방)
##방의 용도가 있듯이(침실, 화장실, 놀이방 등) 용도를 정해서 테이블을 작성한다.

##컬럼(세로) - 속성
##로우=레코드=튜플(가로) - 속성에대한 값

##하나의 컬럼은 도매인을 가지고있다.(도매인 = 컬럼이 가질 수 있는 범위)

##속성간의 관계(1:1, 1:N, N:M) = 릴레이션


##테이블의 제약조건(물리적) - 데이터의 무결성을 보장하기 위함
##무결성보장 = 데이터의 일관성, 유효성, 정확성을 보장 = 잘못된 데이터가 들어오지않게 막는다.

##PK(Primary Key) - 주 식별자(ex : 사원-사번, 학생-학번)의 무결성을 보장하는 제약
###*주식별자는 논리적 의미, PK는 물리적 의미
###*주식별자는 반드시 존재하지만 PK는 존재할 수도 있고 존재하지 않을 수도 있다.
###*테이블당 하나씩만 설정 가능, 중복과 NULL이 허용되지 않는다.
###*설정 명령어 = CONSTRAINT PK이름 PRIMARY KEY (PK컬럼);
###*Unique Index가 자동으로 생성됨

##UK(Unique Key) = 고유키
###*테이블당 여러개 설정가능
###*중복은 허용되지 않지만 NULL은 허용이 된다.
###*Unique Index가 자동으로 생성
###*설정 명령어 = CONSTRAINT UK이름 UNIQUE (UK컬럼);

##FK(Foreign Key) = 외래키
###*부모 테이블이 있다는 것을 의미
