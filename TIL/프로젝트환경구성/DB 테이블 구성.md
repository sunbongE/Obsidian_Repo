
가게 정보
``` sql
CREATE TABLE store_info (
    STORE_ID               VARCHAR2(500),     -- 상가업소번호
    STORE_NAME             VARCHAR2(500),    -- 상호명
    BRANCH_NAME            VARCHAR2(500),    -- 지점명
    CATEGORY_L_CODE        VARCHAR2(500),     -- 상권업종대분류코드
    CATEGORY_L_NAME        VARCHAR2(500),    -- 상권업종대분류명
    CATEGORY_M_CODE        VARCHAR2(500),     -- 상권업종중분류코드
    CATEGORY_M_NAME        VARCHAR2(500),    -- 상권업종중분류명
    CATEGORY_S_CODE        VARCHAR2(500),     -- 상권업종소분류코드
    CATEGORY_S_NAME        VARCHAR2(500),    -- 상권업종소분류명
    INDUSTRY_CODE          VARCHAR2(500),     -- 표준산업분류코드
    INDUSTRY_NAME          VARCHAR2(500),    -- 표준산업분류명
    SIDO_CODE              VARCHAR2(500),     -- 시도코드
    SIDO_NAME              VARCHAR2(500),    -- 시도명
    SIGUNGU_CODE           VARCHAR2(500),     -- 시군구코드
    SIGUNGU_NAME           VARCHAR2(500),    -- 시군구명
    ADMIN_DONG_CODE        VARCHAR2(500),     -- 행정동코드
    ADMIN_DONG_NAME        VARCHAR2(500),    -- 행정동명
    LEGAL_DONG_CODE        VARCHAR2(500),     -- 법정동코드
    LEGAL_DONG_NAME        VARCHAR2(500),    -- 법정동명
    JIBUN_CODE             VARCHAR2(500),     -- 지번코드
    LAND_DIV_CODE          VARCHAR2(500),      -- 대지구분코드
    LAND_DIV_NAME          VARCHAR2(500),     -- 대지구분명
    JIBUN_MAIN_NO          NUMBER,           -- 지번본번지
    JIBUN_SUB_NO           NUMBER,           -- 지번부번지
    JIBUN_ADDRESS          VARCHAR2(500),    -- 지번주소
    ROAD_CODE              VARCHAR2(500),     -- 도로명코드
    ROAD_NAME              VARCHAR2(500),    -- 도로명
    BUILDING_MAIN_NO       NUMBER,           -- 건물본번지
    BUILDING_SUB_NO        NUMBER,           -- 건물부번지
    BUILDING_MANAGE_NO     VARCHAR2(500),     -- 건물관리번호
    BUILDING_NAME          VARCHAR2(500),    -- 건물명
    ROAD_ADDRESS           VARCHAR2(500),    -- 도로명주소
    OLD_ZIP_CODE           VARCHAR2(500),     -- 구우편번호
    NEW_ZIP_CODE           VARCHAR2(500),     -- 신우편번호
    DONG_INFO              VARCHAR2(500),    -- 동정보
    FLOOR_INFO             VARCHAR2(500),     -- 층정보
    UNIT_INFO              VARCHAR2(500),     -- 호정보
    LNG                    NUMBER(20, 15),    -- 경도
    LAT                    NUMBER(20, 15)     -- 위도
);
COMMENT ON TABLE store_info IS '상권 업소 정보 테이블';

COMMENT ON COLUMN store_info.STORE_ID IS '상가업소번호';
COMMENT ON COLUMN store_info.STORE_NAME IS '상호명';
COMMENT ON COLUMN store_info.BRANCH_NAME IS '지점명';
COMMENT ON COLUMN store_info.CATEGORY_L_CODE IS '상권업종대분류코드';
COMMENT ON COLUMN store_info.CATEGORY_L_NAME IS '상권업종대분류명';
COMMENT ON COLUMN store_info.CATEGORY_M_CODE IS '상권업종중분류코드';
COMMENT ON COLUMN store_info.CATEGORY_M_NAME IS '상권업종중분류명';
COMMENT ON COLUMN store_info.CATEGORY_S_CODE IS '상권업종소분류코드';
COMMENT ON COLUMN store_info.CATEGORY_S_NAME IS '상권업종소분류명';
COMMENT ON COLUMN store_info.INDUSTRY_CODE IS '표준산업분류코드';
COMMENT ON COLUMN store_info.INDUSTRY_NAME IS '표준산업분류명';
COMMENT ON COLUMN store_info.SIDO_CODE IS '시도코드';
COMMENT ON COLUMN store_info.SIDO_NAME IS '시도명';
COMMENT ON COLUMN store_info.SIGUNGU_CODE IS '시군구코드';
COMMENT ON COLUMN store_info.SIGUNGU_NAME IS '시군구명';
COMMENT ON COLUMN store_info.ADMIN_DONG_CODE IS '행정동코드';
COMMENT ON COLUMN store_info.ADMIN_DONG_NAME IS '행정동명';
COMMENT ON COLUMN store_info.LEGAL_DONG_CODE IS '법정동코드';
COMMENT ON COLUMN store_info.LEGAL_DONG_NAME IS '법정동명';
COMMENT ON COLUMN store_info.JIBUN_CODE IS '지번코드';
COMMENT ON COLUMN store_info.LAND_DIV_CODE IS '대지구분코드';
COMMENT ON COLUMN store_info.LAND_DIV_NAME IS '대지구분명';
COMMENT ON COLUMN store_info.JIBUN_MAIN_NO IS '지번본번지';
COMMENT ON COLUMN store_info.JIBUN_SUB_NO IS '지번부번지';
COMMENT ON COLUMN store_info.JIBUN_ADDRESS IS '지번주소';
COMMENT ON COLUMN store_info.ROAD_CODE IS '도로명코드';
COMMENT ON COLUMN store_info.ROAD_NAME IS '도로명';
COMMENT ON COLUMN store_info.BUILDING_MAIN_NO IS '건물본번지';
COMMENT ON COLUMN store_info.BUILDING_SUB_NO IS '건물부번지';
COMMENT ON COLUMN store_info.BUILDING_MANAGE_NO IS '건물관리번호';
COMMENT ON COLUMN store_info.BUILDING_NAME IS '건물명';
COMMENT ON COLUMN store_info.ROAD_ADDRESS IS '도로명주소';
COMMENT ON COLUMN store_info.OLD_ZIP_CODE IS '구우편번호';
COMMENT ON COLUMN store_info.NEW_ZIP_CODE IS '신우편번호';
COMMENT ON COLUMN store_info.DONG_INFO IS '동정보';
COMMENT ON COLUMN store_info.FLOOR_INFO IS '층정보';
COMMENT ON COLUMN store_info.UNIT_INFO IS '호정보';
COMMENT ON COLUMN store_info.LNG IS '경도';
COMMENT ON COLUMN store_info.LAT IS '위도';
```

R_store_info
``` sql
create or replace TYPE R_STORE_INFO AS OBJECT(
        STORE_ID               VARCHAR2(500),     -- 상가업소번호
        STORE_NAME             VARCHAR2(500),    -- 상호명
        BRANCH_NAME            VARCHAR2(500),    -- 지점명
        CATEGORY_L_CODE        VARCHAR2(500),     -- 상권업종대분류코드
        CATEGORY_L_NAME        VARCHAR2(500),    -- 상권업종대분류명
        CATEGORY_M_CODE        VARCHAR2(500),     -- 상권업종중분류코드
        CATEGORY_M_NAME        VARCHAR2(500),    -- 상권업종중분류명
        CATEGORY_S_CODE        VARCHAR2(500),     -- 상권업종소분류코드
        CATEGORY_S_NAME        VARCHAR2(500),    -- 상권업종소분류명
        INDUSTRY_CODE          VARCHAR2(500),     -- 표준산업분류코드
        INDUSTRY_NAME          VARCHAR2(500),    -- 표준산업분류명
        SIDO_CODE              VARCHAR2(500),     -- 시도코드
        SIDO_NAME              VARCHAR2(500),    -- 시도명
        SIGUNGU_CODE           VARCHAR2(500),     -- 시군구코드
        SIGUNGU_NAME           VARCHAR2(500),    -- 시군구명
        ADMIN_DONG_CODE        VARCHAR2(500),     -- 행정동코드
        ADMIN_DONG_NAME        VARCHAR2(500),    -- 행정동명
        LEGAL_DONG_CODE        VARCHAR2(500),     -- 법정동코드
        LEGAL_DONG_NAME        VARCHAR2(500),    -- 법정동명
        JIBUN_CODE             VARCHAR2(500),     -- 지번코드
        LAND_DIV_CODE          VARCHAR2(500),      -- 대지구분코드
        LAND_DIV_NAME          VARCHAR2(500),     -- 대지구분명
        JIBUN_MAIN_NO          NUMBER,           -- 지번본번지
        JIBUN_SUB_NO           NUMBER,           -- 지번부번지
        JIBUN_ADDRESS          VARCHAR2(5000),    -- 지번주소
        ROAD_CODE              VARCHAR2(500),     -- 도로명코드
        ROAD_NAME              VARCHAR2(500),    -- 도로명
        BUILDING_MAIN_NO       NUMBER,           -- 건물본번지
        BUILDING_SUB_NO        NUMBER,           -- 건물부번지
        BUILDING_MANAGE_NO     VARCHAR2(500),     -- 건물관리번호
        BUILDING_NAME          VARCHAR2(500),    -- 건물명
        ROAD_ADDRESS           VARCHAR2(500),    -- 도로명주소
        OLD_ZIP_CODE           VARCHAR2(500),     -- 구우편번호
        NEW_ZIP_CODE           VARCHAR2(500),     -- 신우편번호
        DONG_INFO              VARCHAR2(500),    -- 동정보
        FLOOR_INFO             VARCHAR2(500),     -- 층정보
        UNIT_INFO              VARCHAR2(500),     -- 호정보
        LNG                    NUMBER(20, 15),    -- 경도
        LAT                    NUMBER(20, 15)     -- 위도
    );

```

table
``` sql
create or replace TYPE TB_STORE_INFO AS TABLE OF R_STORE_INFO;
```


---

Package
```
create or replace PACKAGE PKG_STORE AS 
  /* TODO enter package declarations (types, exceptions, methods etc) here */ 
    PROCEDURE STORE_INFO_SAVE(p_store_list IN TB_STORE_INFO);
END PKG_STORE;
```

body
``` sql
create or replace PACKAGE BODY PKG_STORE AS

  PROCEDURE STORE_INFO_SAVE(p_store_list IN TB_STORE_INFO) AS
  BEGIN

    FORALL IDX IN p_store_list.first.. p_store_list.count
        INSERT INTO STORE_INFO VALUES( 
            p_store_list(idx).STORE_ID,
            p_store_list(idx).STORE_NAME,
            p_store_list(idx).BRANCH_NAME,
            p_store_list(idx).CATEGORY_L_CODE,
            p_store_list(idx).CATEGORY_L_NAME,
            p_store_list(idx).CATEGORY_M_CODE,
            p_store_list(idx).CATEGORY_M_NAME,
            p_store_list(idx).CATEGORY_S_CODE  ,
            p_store_list(idx).CATEGORY_S_NAME ,
            p_store_list(idx).INDUSTRY_CODE      ,
            p_store_list(idx).INDUSTRY_NAME     ,
            p_store_list(idx).SIDO_CODE             ,
            p_store_list(idx).SIDO_NAME            ,
            p_store_list(idx).SIGUNGU_CODE        ,
            p_store_list(idx).SIGUNGU_NAME       ,
            p_store_list(idx).ADMIN_DONG_CODE  ,
            p_store_list(idx).ADMIN_DONG_NAME ,
            p_store_list(idx).LEGAL_DONG_CODE   ,
            p_store_list(idx).LEGAL_DONG_NAME , 
            p_store_list(idx).JIBUN_CODE            ,
            p_store_list(idx).LAND_DIV_CODE      ,
            p_store_list(idx).LAND_DIV_NAME     ,
            p_store_list(idx).JIBUN_MAIN_NO     ,
            p_store_list(idx).JIBUN_SUB_NO       ,
            p_store_list(idx).JIBUN_ADDRESS     ,
            p_store_list(idx).ROAD_CODE         ,
            p_store_list(idx).ROAD_NAME        ,
            p_store_list(idx).BUILDING_MAIN_NO,
            p_store_list(idx).BUILDING_SUB_NO  ,
            p_store_list(idx).BUILDING_MANAGE_NO,
            p_store_list(idx).BUILDING_NAME        ,
            p_store_list(idx).ROAD_ADDRESS        ,
            p_store_list(idx).OLD_ZIP_CODE          ,
            p_store_list(idx).NEW_ZIP_CODE         ,
            p_store_list(idx).DONG_INFO            ,
            p_store_list(idx).FLOOR_INFO           ,
            p_store_list(idx).UNIT_INFO             ,
            p_store_list(idx).LNG                    ,
            p_store_list(idx).LAT                    
        );

  END STORE_INFO_SAVE;

END PKG_STORE;
```