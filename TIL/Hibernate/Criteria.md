
---

## 🔍 **Hibernate Criteria API란?**

`Criteria`는 Hibernate에서 동적 쿼리를 생성할 수 있도록 지원하는 API입니다. SQL을 직접 작성하지 않고도 다양한 조건을 추가하여 객체 지향적으로 조회할 수 있습니다.

`Criteria`는 Hibernate 5 이후 `CriteriaBuilder`와 `CriteriaQuery`로 대체되었지만, 여전히 많이 사용됩니다.

---

# ✅ **1. Criteria 생성**

### 🔹 `createCriteria(Class)` - 특정 엔티티에 대한 Criteria 생성

```java
Criteria criteria = session.createCriteria(User.class);
```

- `User` 엔티티 테이블을 조회하기 위한 `Criteria` 객체 생성
- 이후 여기에 다양한 조건을 추가하여 원하는 데이터를 가져올 수 있음

---

# ✅ **2. Criteria 조건 추가**

### 🔹 `add(Restrictions.xxx())` - WHERE 조건 추가
> **검색 조건(제약 조건, WHERE 절)을 추가하는 역할**

```java
criteria.add(Restrictions.eq("username", "leo"));
criteria.add(Restrictions.gt("age", 18));
```

- `WHERE username = 'leo' AND age > 18` 조건 추가

---

# ✅ **3. 비교 연산**

### 1️⃣ `eq()` - **동등 조건 (=)**

```java
criteria.add(Restrictions.eq("status", "active"));
```

```sql
WHERE status = 'active'
```

### 2️⃣ `ne()` - **다른 값 (!=)**

```java
criteria.add(Restrictions.ne("status", "inactive"));
```

```sql
WHERE status != 'inactive'
```

### 3️⃣ `gt()` / `lt()` - **초과 / 미만 (>, <)**

```java
criteria.add(Restrictions.gt("age", 18));
criteria.add(Restrictions.lt("age", 30));
```

```sql
WHERE age > 18 AND age < 30
```

### 4️⃣ `ge()` / `le()` - **이상 / 이하 (>=, <=)**

```java
criteria.add(Restrictions.ge("salary", 5000));
criteria.add(Restrictions.le("salary", 10000));
```

```sql
WHERE salary >= 5000 AND salary <= 10000
```

---

# ✅ **4. 논리 연산**

### 5️⃣ `and()` - **AND 조건**

```java
criteria.add(Restrictions.and(
    Restrictions.eq("role", "admin"),
    Restrictions.ge("age", 25)
));
```

```sql
WHERE role = 'admin' AND age >= 25
```

### 6️⃣ `or()` - **OR 조건**

```java
criteria.add(Restrictions.or(
    Restrictions.eq("role", "admin"),
    Restrictions.eq("role", "manager")
));
```

```sql
WHERE role = 'admin' OR role = 'manager'
```

### 7️⃣ `not()` - **NOT 조건**

```java
criteria.add(Restrictions.not(Restrictions.eq("status", "banned")));
```

```sql
WHERE NOT status = 'banned'
```

---

# ✅ **5. 범위 연산**

### 8️⃣ `between()` - **범위 검색**

```java
criteria.add(Restrictions.between("age", 18, 30));
```

```sql
WHERE age BETWEEN 18 AND 30
```

---

# ✅ **6. 리스트 연산**

### 9️⃣ `in()` - **목록 포함 (IN)**

```java
criteria.add(Restrictions.in("status", new String[]{"active", "pending"}));
```

```sql
WHERE status IN ('active', 'pending')
```

### 🔟 `notIn()` - **목록 미포함 (NOT IN)**

```java
criteria.add(Restrictions.not(Restrictions.in("status", new String[]{"banned", "deleted"})));
```

```sql
WHERE status NOT IN ('banned', 'deleted')
```

---

# ✅ **7. 문자열 검색**

### 1️⃣1️⃣ `like()` - **부분 문자열 검색 (LIKE)**

```java
criteria.add(Restrictions.like("username", "leo%"));
```

```sql
WHERE username LIKE 'leo%'
```

- `"leo%"` → **"leo"로 시작하는 문자열 검색**

### 1️⃣2️⃣ `MatchMode` 활용 (`MatchMode.ANYWHERE`)

```java
criteria.add(Restrictions.like("username", "eo", MatchMode.ANYWHERE));
```

```sql
WHERE username LIKE '%eo%'
```

- `MatchMode.START`: `"leo%"` (leo로 시작)
- `MatchMode.END`: `"%leo"` (leo로 끝남)
- `MatchMode.ANYWHERE`: `"%leo%"` (leo 포함)

---

# ✅ **8. NULL 처리**

### 1️⃣3️⃣ `isNull()` - **NULL 값 조회**

```java
criteria.add(Restrictions.isNull("deletedAt"));
```

```sql
WHERE deletedAt IS NULL
```

### 1️⃣4️⃣ `isNotNull()` - **NULL이 아닌 값 조회**

```java
criteria.add(Restrictions.isNotNull("updatedAt"));
```

```sql
WHERE updatedAt IS NOT NULL
```

---

# ✅ **9. 정렬 및 페이징**

### 1️⃣5️⃣ `orderAsc()` - **오름차순 정렬**

```java
criteria.addOrder(Order.asc("username"));
```

```sql
ORDER BY username ASC
```

### 1️⃣6️⃣ `orderDesc()` - **내림차순 정렬**

```java
criteria.addOrder(Order.desc("createdAt"));
```

```sql
ORDER BY createdAt DESC
```

### 1️⃣7️⃣ `setFirstResult()` - **시작 인덱스 지정**

```java
criteria.setFirstResult(10);
```

```sql
OFFSET 10
```

- **10번째 데이터부터 조회** (0-based index)

### 1️⃣8️⃣ `setMaxResults()` - **최대 결과 개수 지정**

```java
criteria.setMaxResults(5);
```

```sql
LIMIT 5
```

- **최대 5개만 조회**

---

# ✅ **10. JOIN 및 Fetch**

### 1️⃣9️⃣ `createAlias()` - **JOIN 실행**

```java
criteria.createAlias("department", "dept");
criteria.add(Restrictions.eq("dept.name", "IT"));
```

```sql
SELECT * FROM User u
JOIN Department d ON u.department_id = d.id
WHERE d.name = 'IT'
```

- `department` 테이블을 `dept`로 별칭을 지정하고 조회

### 2️⃣0️⃣ `setFetchMode()` - **EAGER / LAZY 설정**

```java
criteria.setFetchMode("department", FetchMode.JOIN);
```

- 조인된 엔티티를 한 번에 가져올지 (EAGER) 나중에 가져올지 (LAZY) 설정 가능

---

# ✅ **11. 복합 검색 예제**

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

# 🔥 **결론**

- `Criteria` API는 **SQL 없이 동적 쿼리를 작성할 수 있도록 도와줌**
- **비교 (`eq`, `ne`, `gt`, `lt`, `between`)**
- **논리 (`and`, `or`, `not`)**
- **리스트 (`in`, `notIn`)**
- **문자열 (`like`)**
- **NULL 처리 (`isNull`, `isNotNull`)**
- **정렬 및 페이징 (`orderAsc`, `orderDesc`, `setFirstResult`, `setMaxResults`)**
- **Hibernate 5 이상에서는 `CriteriaBuilder` 사용 권장!** 🚀