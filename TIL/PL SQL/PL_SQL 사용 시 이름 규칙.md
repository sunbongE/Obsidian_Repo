 

---

## 📘 PL/SQL Naming Conventions

|항목|규칙|예시|부연 설명|
|---|---|---|---|
|**패키지 이름 (Package Name)**|전부 대문자, 접두어 `PKG_`, 도메인 중심|`PKG_ORDER`, `PKG_CUST`|하나의 도메인 또는 기능 단위별로 관리. 시스템 규모가 클 경우 `PKG_모듈명_기능` 형태로 구성|
|**프로시저 이름 (Procedure Name)**|동사 + 명사 구조, 대문자 또는 스네이크 표기법|`INSERT_ORDER`, `UPDATE_MENU_PRICE`|기능을 명확히 드러내야 하며, CRUD 형태를 직관적으로 표현. 패키지 내부/외부에 따라 접두어 구분 가능|
|**함수 이름 (Function Name)**|동사 + 명사, `GET_`, `CALC_` 등의 접두어 사용|`GET_TOTAL_PRICE`, `CALC_DISCOUNT_RATE`|반환값을 가지므로 계산 또는 조회 성격이 드러나는 이름 사용 권장|
|**변수 이름 (Variable)**|소문자 + 접두어 `v_`, 스네이크 표기법|`v_order_id`, `v_total_price`|지역 변수는 `v_`, 전역 변수는 `g_` 사용. 소문자로 구성하는 것이 가독성 향상에 유리함|
|**상수 이름 (Constant)**|소문자 또는 대문자 + 접두어 `c_`|`c_tax_rate`, `C_MAX_VALUE`|변경되지 않는 고정 값은 `c_` 접두어로 명시하며, 일관성 유지를 위해 대문자도 많이 사용됨|
|**매개변수 이름 (Parameter)**|소문자 + 접두어 `p_`|`p_cust_id`, `p_ord_dt`|함수 또는 프로시저의 인자는 `p_`로 구분하며, 실제 테이블 컬럼명과 혼동 방지 목적|
|**커서 이름 (Cursor)**|대문자 + 접두어 `CUR_`|`CUR_ORDER_LIST`|명확하게 커서임을 나타내며, 조회 결과 대상이 무엇인지 나타냄|
|**커서 변수 (Cursor Variable)**|`cv_` 접두어 + 도메인명|`cv_menu`, `cv_result`|`REF CURSOR` 사용 시, 커서 변수임을 명시적으로 구분|
|**예외 이름 (Exception)**|`e_` 접두어, snake_case|`e_order_not_found`, `e_invalid_input`|사용자 정의 예외나 시스템 예외를 구분할 수 있도록 접두어 사용 권장|
|**레코드 타입 (Record Type)**|`rec_` 접두어 + 명사|`rec_customer`, `rec_order_detail`|%ROWTYPE 또는 RECORD TYPE 선언 시 사용. 테이블 구조 매핑임을 명확히 함|
|**컬렉션 (Collection / Array)**|`tbl_`, `arr_`, `list_` 접두어|`tbl_menu_id`, `arr_prices`|컬렉션의 성격을 드러내기 위한 접두어를 활용하여 코드의 의도를 명확히 함|
|**시퀀스 이름 (Sequence)**|대문자 + `_SEQ` 접미어|`ORDER_ID_SEQ`|고유 번호를 생성하는 객체임을 명시적으로 표현|
|**트리거 이름 (Trigger)**|`TRG_테이블명_이벤트`|`TRG_ORDER_BI`|BI = Before Insert, AU = After Update 등으로 트리거 이벤트를 줄여서 명시|
|**뷰 이름 (View)**|접두어 `VW_` 또는 `V_`|`VW_CUSTOMER_INFO`|실체 테이블과 구분되도록 명시적인 접두어 사용|
|**테이블 이름 (Table)**|복수형 명사, 대문자, 언더스코어 사용|`ORDERS`, `MENU_ITEMS`|실제 데이터 엔터티를 나타내며, 일반적으로 대문자 표기. 팀 규칙에 따라 단수형 사용도 가능|
|**인덱스 이름 (Index)**|`IDX_테이블명_컬럼명`|`IDX_ORDERS_CUST_ID`|해당 인덱스가 어떤 테이블과 컬럼을 위한 것인지 명확히 나타냄|
|**시노님 (Synonym)**|원본 오브젝트명을 따름|`ORDERS` → `ORD`|조직 규칙에 따라 간결하게 표현 가능하나, 충돌을 피하기 위해 주의 필요|

---

## 📌 추가 고려사항

|항목|권장 사항|
|---|---|
|**일관성**|프로젝트 내 모든 PL/SQL 코드에서 동일한 네이밍 규칙 적용|
|**가독성**|혼동되는 약어 사용 지양, 의미가 명확한 단어 선택|
|**표기법 선택**|대문자(SCREAMING_SNAKE_CASE), 소문자(snake_case), 카멜케이스 중 팀 내 표준 준수|
|**언어**|대부분 영어 사용. 한글은 주석에만 사용 권장|

---

## 📙 예시: 패키지와 그 내부 구성

```sql
-- 패키지 선언
CREATE OR REPLACE PACKAGE PKG_ORDER AS
    PROCEDURE MAKE_ORDER(p_cust_id IN VARCHAR2, r_rtn_code OUT VARCHAR2, r_rtn_msg OUT VARCHAR2);
    FUNCTION GET_ORDER_INFO(p_order_id IN NUMBER) RETURN VARCHAR2;
END PKG_ORDER;
```

```sql
-- 변수 예시
DECLARE
    v_order_id NUMBER;
    v_total_price NUMBER;
    c_tax_rate CONSTANT NUMBER := 0.1;
BEGIN
    NULL;
END;
```

---

## ✅ 결론

PL/SQL에서의 이름 규칙은 **정확한 의미 전달, 유지보수 용이성, 협업 효율성**을 높이기 위한 필수 요소입니다. 실무에서는 개발 조직의 코딩 컨벤션 문서를 기반으로 위와 같은 네이밍 원칙을 세우고 준수합니다. 프로젝트 착수 전 명확한 네이밍 가이드 문서를 작성하여 개발자 간 혼선을 방지하는 것이 좋습니다.

 