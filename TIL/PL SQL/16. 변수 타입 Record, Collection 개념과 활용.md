
## 일반 타입, 로우 타입 사용 예시

``` sql
CREATE OR REPLACE PROCEDURE SP_SECTION6_1 AS 
     -- 일반변수 
     p_cst_id cst_info.cst_id%type;
     v_name cst_info.name%type;
     
     -- rowtype 변수 
     p_cst_info cst_info%rowtype;
     r_cst_info cst_info%rowtype;
BEGIN
   p_cst_id := 'C002';
    
    -- 일반변수 이용  
    v_name := f_get_name1(p_cst_id);
    dbms_output.put_line('v_name > '||v_name);
    
    -- Rowtype 이용
    p_cst_info.cst_id:='C004'; -- 값을 초기화 해줘야함.
    r_cst_info := f_get_name2(p_cst_info);
    dbms_output.put_line('r_cst_info.name > '||r_cst_info.name);
    
    -- chr(13): 커서를 가장 앞으로 이동, 
    --- chr(10) : 개행
    dbms_output.put_line(chr(10) || chr(13));
    
    -- 프로시저 일반 변수 사용. 
    p_cst_id := 'C001';
        -- 일반변수 이용  
    sp_get_name1(p_cst_id,v_name);
    dbms_output.put_line('sp v_name > '||v_name);
    
        -- 프로시저 row변수 사용. 
    p_cst_info.cst_id := 'C003';
        -- 일반변수 이용  
    sp_get_name2(p_cst_info, r_cst_info);
    dbms_output.put_line('sp r_cst_info.name > '||r_cst_info.name);
END SP_SECTION6_1;
```


---

함수를 프로시저로 변경 및 차이 파악.

``` sql 

create or replace FUNCTION f_get_name1 
(
  P_CST_ID IN CST_INFO.CST_ID%TYPE
) RETURN VARCHAR2 
AS 
    v_name cst_info.name%type;
BEGIN  
      select name 
    into v_name 
    from cst_info 
    where cst_id=p_cst_id;
    
    return v_name;
END f_get_name1;
/

-- 프로시저로 만들기.

create or replace PROCEDURE SP_get_name1 
(
  P_CST_ID IN CST_INFO.CST_ID%TYPE,
    v_name OUT cst_info.name%type
) 
AS 
BEGIN  
    select name 
    into v_name 
    from cst_info 
    where cst_id=p_cst_id;
    
    
END SP_get_name1;
/

-- 

create or replace FUNCTION f_get_name2 
(
  P_CST_INFO IN CST_INFO%ROWTYPE
) RETURN CST_INFO%ROWTYPE 
  AS 
  r_cst_info cst_info%rowtype;
BEGIN
  select * 
    into r_cst_info
    from cst_info 
    where cst_id=P_CST_INFO.cst_id;
    
    return r_cst_info;
END f_get_name2;
/

create or replace procedure sp_get_name2 
(
  P_CST_INFO IN CST_INFO%ROWTYPE,
  r_cst_info out cst_info%rowtype
)
  AS 
BEGIN
  select * 
    into r_cst_info
    from cst_info 
    where cst_id=P_CST_INFO.cst_id;
    
END sp_get_name2;
/
```