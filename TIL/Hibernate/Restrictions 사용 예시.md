`Restrictions`는 Hibernate의 **Criteria API**에서 다양한 조건을 추가할 때 사용하는 유틸리티 클래스입니다. `WHERE` 절에 들어갈 다양한 조건을 만들 수 있으며, 주요 메서드는 다음과 같습니다.

---

## ✅ **1. 동등/비교 연산**

### 1️⃣ `eq()` - **같음 (=)**

```java
criteria.add(Restrictions.eq("username", "leo"));
```

```sql
WHERE username = 'leo'
```

- 특정 컬럼 값이 지정한 값과 같은 경우 조회

### 2️⃣ `ne()` - **같지 않음 (!=)**

```java
criteria.add(Restrictions.ne("status", "inactive"));
```

```sql
WHERE status != 'inactive'
```

- 특정 컬럼 값이 지정한 값과 **다른 경우** 조회

### 3️⃣ `gt()` - **초과 (>)**

```java
criteria.add(Restrictions.gt("age", 18));
```

```sql
WHERE age > 18
```

- 특정 값보다 **큰 경우** 조회

### 4️⃣ `ge()` - **이상 (>=)**

```java
criteria.add(Restrictions.ge("age", 18));
```

```sql
WHERE age >= 18
```

- 특정 값보다 **크거나 같은 경우** 조회

### 5️⃣ `lt()` - **미만 (<)**

```java
criteria.add(Restrictions.lt("age", 30));
```

```sql
WHERE age < 30
```

- 특정 값보다 **작은 경우** 조회

### 6️⃣ `le()` - **이하 (<=)**

```java
criteria.add(Restrictions.le("age", 30));
```

```sql
WHERE age <= 30
```

- 특정 값보다 **작거나 같은 경우** 조회

---

## ✅ **2. 범위 연산**

### 7️⃣ `between()` - **범위 조건**

```java
criteria.add(Restrictions.between("age", 18, 30));
```

```sql
WHERE age BETWEEN 18 AND 30
```

- 특정 값이 **지정한 범위 안에 있는 경우** 조회

---

## ✅ **3. 리스트 연산**

### 8️⃣ `in()` - **목록 포함 (IN)**

```java
criteria.add(Restrictions.in("status", new String[]{"active", "pending"}));
```

```sql
WHERE status IN ('active', 'pending')
```

- 특정 값이 **주어진 리스트에 포함되는 경우** 조회

### 9️⃣ `notIn()` - **목록 미포함 (NOT IN)**

```java
criteria.add(Restrictions.not(Restrictions.in("status", new String[]{"banned", "deleted"})));
```

```sql
WHERE status NOT IN ('banned', 'deleted')
```

- 특정 값이 **주어진 리스트에 포함되지 않는 경우** 조회

---

## ✅ **4. 문자열 관련 연산**

### 🔟 `like()` - **부분 문자열 검색 (LIKE)**

```java
criteria.add(Restrictions.like("username", "leo%"));
```

```sql
WHERE username LIKE 'leo%'
```

- `%`는 SQL의 와일드카드 문자로, `"leo%"`는 `"leo"`로 시작하는 모든 문자열을 의미

**📌 `MatchMode` 활용 (`MatchMode.ANYWHERE` 추천)**

```java
criteria.add(Restrictions.like("username", "eo", MatchMode.ANYWHERE));
```

```sql
WHERE username LIKE '%eo%'
```

- `MatchMode.START`: `"leo%"` (leo로 시작)
- `MatchMode.END`: `"%leo"` (leo로 끝남)
- `MatchMode.ANYWHERE`: `"%leo%"` (leo가 포함됨)

---

## ✅ **5. 논리 연산**

### 1️⃣1️⃣ `and()` - **AND 조건**

```java
criteria.add(Restrictions.and(
    Restrictions.eq("role", "admin"),
    Restrictions.ge("age", 25)
));
```

```sql
WHERE role = 'admin' AND age >= 25
```

- 두 개 이상의 조건이 **모두 참인 경우** 조회

### 1️⃣2️⃣ `or()` - **OR 조건**

```java
criteria.add(Restrictions.or(
    Restrictions.eq("role", "admin"),
    Restrictions.eq("role", "manager")
));
```

```sql
WHERE role = 'admin' OR role = 'manager'
```

- 두 개 이상의 조건 중 **하나라도 참이면** 조회

### 1️⃣3️⃣ `not()` - **부정 (NOT)**

```java
criteria.add(Restrictions.not(Restrictions.eq("status", "banned")));
```

```sql
WHERE NOT status = 'banned'
```

- 특정 조건을 **부정** (반대)할 때 사용

---

## ✅ **6. NULL 처리**

### 1️⃣4️⃣ `isNull()` - **NULL 값 조회**

```java
criteria.add(Restrictions.isNull("deletedAt"));
```

```sql
WHERE deletedAt IS NULL
```

- 특정 컬럼이 `NULL`인 경우 조회

### 1️⃣5️⃣ `isNotNull()` - **NULL이 아닌 값 조회**

```java
criteria.add(Restrictions.isNotNull("updatedAt"));
```

```sql
WHERE updatedAt IS NOT NULL
```

- 특정 컬럼이 `NULL`이 아닌 경우 조회

---

## ✅ **7. 순서 정렬**

### 1️⃣6️⃣ `orderAsc()` - **오름차순 정렬**

```java
criteria.addOrder(Order.asc("username"));
```

```sql
ORDER BY username ASC
```

- 컬럼 값을 **오름차순 정렬** (A → Z, 1 → 9)

### 1️⃣7️⃣ `orderDesc()` - **내림차순 정렬**

```java
criteria.addOrder(Order.desc("createdAt"));
```

```sql
ORDER BY createdAt DESC
```

- 컬럼 값을 **내림차순 정렬** (Z → A, 9 → 1)

---

## ✅ **8. 페이징 처리**

### 1️⃣8️⃣ `setFirstResult()` - **시작 인덱스 지정**

```java
criteria.setFirstResult(10);
```

```sql
OFFSET 10
```

- **10번째 데이터부터 조회** (0-based index)

### 1️⃣9️⃣ `setMaxResults()` - **최대 결과 개수 지정**

```java
criteria.setMaxResults(5);
```

```sql
LIMIT 5
```

- **최대 5개만 조회**

### ✨ 페이징 예제 (페이지네이션)

```java
int pageNumber = 2;
int pageSize = 10;
criteria.setFirstResult((pageNumber - 1) * pageSize);
criteria.setMaxResults(pageSize);
```

- `pageNumber = 2`, `pageSize = 10`이면 **11~20번 데이터 조회**

---

## ✅ **9. 예제 코드 (복합 검색)**

```java
Criteria criteria = session.createCriteria(User.class);

// "leo" 포함하는 username, 나이 18~30, 활성화된 사용자만 조회
criteria.add(Restrictions.like("username", "leo", MatchMode.ANYWHERE));
criteria.add(Restrictions.between("age", 18, 30));
criteria.add(Restrictions.eq("isActive", true));

// 정렬 및 페이징 처리
criteria.addOrder(Order.asc("username"));
criteria.setFirstResult(0);
criteria.setMaxResults(10);

List<User> users = criteria.list();
```

```sql
SELECT * FROM User 
WHERE username LIKE '%leo%' 
AND age BETWEEN 18 AND 30 
AND isActive = true 
ORDER BY username ASC 
LIMIT 10 OFFSET 0;
```

---

## 🔥 **결론**

- `Restrictions`는 Hibernate Criteria API에서 **동적 쿼리**를 쉽게 만들 수 있도록 도와줍니다.
- **비교 연산 (`eq`, `ne`, `gt`, `lt`, `between`)**
- **논리 연산 (`and`, `or`, `not`)**
- **리스트 (`in`, `notIn`)**
- **문자열 (`like`)**
- **NULL 처리 (`isNull`, `isNotNull`)**
- **정렬 및 페이징 (`orderAsc`, `orderDesc`, `setFirstResult`, `setMaxResults`)**
- **Hibernate 5 이상에서는 `CriteriaBuilder` 사용이 권장됨!** 🚀