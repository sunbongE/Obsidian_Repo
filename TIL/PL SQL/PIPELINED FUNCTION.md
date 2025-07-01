## PIPELINED FUNCTION이란?

- 일반 함수는 **전체 결과를 메모리에 올려 한꺼번에 반환**
    
- **PIPELINED FUNCTION**은 **한 행씩 반환** (`TABLE 함수처럼 SELECT 가능`)
    
- 클라이언트나 SQL에서 `SELECT * FROM TABLE(함수명)` 형태로 사용 가능
    
- **메모리 효율적**, **속도도 빠름**, **커서 없이도 대체 가능**


## 구조 정리

1. **반환 타입 정의** (**OBJECT** + **TABLE** 타입)
    
2. **PIPELINED FUNCTION 구현**
    
3. `SELECT * from TABLE(pipelined_function_name)`으로 호출

# 예제: `real_ord` 테이블 100만 건 pipelined로 반환

먼저 `select * from real_ord` 했을 때 컴퓨터가 멈춰서 시간을 확인 못했다. 상당히 오래 기다림.

## STEP 1. 오브젝트 타입 선언

> 조회하려는 테이블과 동일하게 설정했다.
``` SQL
CREATE OR REPLACE TYPE ty_real_ord_row AS OBJECT (
    ord_seq     NUMBER,
    cst_id      VARCHAR2(20),
    mnu_id      VARCHAR2(20),
    mnu_size    VARCHAR2(1),
    mnu_ice     VARCHAR2(1),
    qty         NUMBER,
    price       NUMBER,
    total_price NUMBER,
    point_use   NUMBER,
    point_add   NUMBER
);
/
```

## STEP 2. 테이블 타입 선언
> 오브젝트 타입의 구조를 갖는 테이블을 생성

``` SQL

CREATE OR REPLACE TYPE ty_tbl_real_ord AS TABLE OF ty_real_ord_row;

```

## STEP 3. 파이프라인 함수 생성
``` sql
CREATE OR REPLACE FUNCTION f_pipe_real_ord
RETURN ty_tbl_real_ord PIPELINED
IS
BEGIN
    FOR rec IN (SELECT * FROM real_ord) LOOP
        PIPE ROW (
            ty_real_ord_row(
                rec.ord_seq,
                rec.cst_id,
                rec.mnu_id,
                rec.mnu_size,
                rec.mnu_ice,
                rec.qty,
                rec.price,
                rec.total_price,
                rec.point_use,
                rec.point_add
            )
        );
    END LOOP;
    RETURN;
END;
/
```

## 호출
``` SQL
SELECT * FROM TABLE(f_pipe_real_ord);
```
- 클라이언트에서 이 SELECT를 실행하면 `real_ord`의 데이터를 **스트리밍하듯** 받아갑니다.
    
- 내부적으로는 하나씩 처리되므로 **메모리 효율이 매우 높음**

---

**그럼 조회 결과가 달라지진 않으려나?**
``` SQL
select count(*) from real_ord where cst_id = 'C001'; -- 125299
select count(*) 
from (
    select * from table(f_pipe_real_ord)
) a
where a.cst_id = 'C001'; -- 125299 
```
 두 결과는 동일했다.
 