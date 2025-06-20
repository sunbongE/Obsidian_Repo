PL/SQL 블록은 DECLARE, BEGIN, EXCEPTION, END 로 구성
``` SQL 
DECLARE
	-- 변수 선언 : 변수명, 데이터 타입을 선언 
	NAME VARCHAR2(10)
	NAME2 VARCHAR2(10) := 'ANNA'; 
BEGIN
	-- 실행할 코드 IF, CASE, LOOP 문이 위치할 수 있음.
EXCEPTION
	-- 예외처리 코드
END; -- 블록의 끝을 의미
/   -- PL/SQL 블록을 실행하는 역할.
```

**[데이터 타입]**
- NUMBER: 숫자 타입으로 정수나 실수 값을 저장할 수 있습니다.
- VARCHAR2: 문자열 타입으로 변수 길이에 따라 가변적으로 저장할 수 있습니다.
- DATE: 날짜와 시간 값을 저장할 수 있습니다.
- CURSOR: 쿼리 결과를 가리키는 커서 값을 저장할 수 있습니다.




---

## 실습


2가지 실행 방법
1. 블록 실행 방식
2. 익명 블록 실행 방식

#### 블록 실행 방식
``` sql
SET SERVEROUTPUT ON; -- 변수 값 출력 설정.

DECLARE
    NAME VARCHAR(10);
    NAME2 VARCHAR(10) := 'ANNA';
BEGIN
    IF NAME2 = 'ANNA' THEN NAME := 'BEN';
    END IF;
    -- 변수 출력
    DBMS_OUTPUT.PUT_LINE('NAME: '||NAME); -- BEN
    
EXCEPTION
    WHEN OTHERS THEN 
    DBMS_OUTPUT.PUT_LINE('ERROR');

END;
/
```

#### 익명 블록 실행 방식
``` sql

CREATE OR REPLACE PROCEDURE test_proc IS
    NAME VARCHAR2(10);  -- VARCHAR이 아니라 VARCHAR2 사용
    NAME2 VARCHAR2(10) := 'ANNA';
BEGIN
    IF NAME2 = 'ANNA' THEN 
        NAME := 'BEN';  -- 대입 연산자는 := 사용
    END IF;

    -- 변수 출력
    DBMS_OUTPUT.PUT_LINE('NAME: ' || NAME);  -- 정상 출력 기대

EXCEPTION
    WHEN OTHERS THEN 
        DBMS_OUTPUT.PUT_LINE('ERROR');
END;
/ -- 먼저 실행 -> 컴파일
-- 컴파일 정상적으로 되었는지 확인 명령어 valid || invalid
SELECT OBJECT_NAME, STATUS FROM USER_OBJECTS WHERE OBJECT_TYPE = 'PROCEDURE';

EXEC test_proc; -- 실행
```