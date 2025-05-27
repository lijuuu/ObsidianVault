

## 🔁 **Why Normalize?**

- **Removes Redundancy** (no repeated data)
    
- **Avoids Anomalies** (insert/update/delete issues)
    
- **Improves Integrity** (consistent data)
    

---

## 🔹 **0NF (Zero Normal Form)**

**No rules. Raw unstructured data.**

```text
| ID | Name  | Address          | Orders           |
|----|-------|------------------|------------------|
| 1  | Alice | NY               | Shoes, Hat       |
```

---

## 🔹 **1NF (First Normal Form)**

**💡 Rule:** Only _atomic_ values. No arrays, no repeating groups.

🔸 **Shortcut:** **“Each cell = 1 value”**

### ❌ Bad (Not 1NF)

```text
| ID | Name  | Courses         |
|----|-------|-----------------|
| 1  | Liju  | Math, Physics    |
```

### ✅ Good (1NF)

```text
| ID | Name  | Course    |
|----|-------|-----------|
| 1  | Liju  | Math      |
| 1  | Liju  | Physics   |
```

🟩 **Why use:** Makes data queryable  
🟥 **Why not:** Increases row count, hurts performance in some cases

---

## 🔹 **2NF (Second Normal Form)**

**💡 Rule:** 1NF + _No Partial Dependency_

🔸 **Shortcut:** **“Whole key → all columns”**

> Applies **only** when primary key is **composite** (more than one column)

### ❌ Bad (Not 2NF)

```text
| OrderID | ProductID | ProductName | Quantity |
|---------|-----------|-------------|----------|
| 101     | 1         | Keyboard    | 2        |
```

> `ProductName` depends only on `ProductID`, not `OrderID + ProductID`

### ✅ Good (2NF)

**Products table:**

```text
| ProductID | ProductName |
|-----------|-------------|
| 1         | Keyboard    |
```

**OrderDetails table:**

```text
| OrderID | ProductID | Quantity |
|---------|-----------|----------|
| 101     | 1         | 2        |
```

🟩 **Why use:** Removes partial dependencies  
🟥 **Why not:** More tables → more joins

---

## 🔹 **3NF (Third Normal Form)**

**💡 Rule:** 2NF + _No Transitive Dependency_

🔸 **Shortcut:** **“Only key → non-key columns”**

> No non-key column should depend on another non-key column.

### ❌ Bad (Not 3NF)

```text
| EmpID | EmpName | DeptID | DeptName |
|-------|---------|--------|----------|
| 1     | Liju    | 10     | HR       |
```

> `DeptName` depends on `DeptID`, not on `EmpID` directly

### ✅ Good (3NF)

**Employees:**

```text
| EmpID | EmpName | DeptID |
|-------|---------|--------|
| 1     | Liju    | 10     |
```

**Departments:**

```text
| DeptID | DeptName |
|--------|----------|
| 10     | HR       |
```

🟩 **Why use:** Avoids update anomalies  
🟥 **Why not:** Even more joins, performance trade-offs

---

## 🔹 **BCNF (Boyce-Codd Normal Form)**

**💡 Rule:** 3NF + _Every determinant is a candidate key_

🔸 **Shortcut:** **“Super strict 3NF”**

> Happens when a non-primary candidate key determines another attribute

### ❌ Bad (Not BCNF)

```text
| Course | Instructor | Room  |
|--------|------------|-------|
| Math   | John       | 101   |
```

Assume:

- **1 instructor teaches only 1 course** ✅
    
- **1 course can be taught in different rooms** ❌  
    → Instructor → Course violates BCNF
    

### ✅ Good (BCNF)

Split `Instructor` and `Room` into separate tables.

🟩 **Why use:** Fully eliminates redundancy  
🟥 **Why not:** Overkill for most business apps

---

## 🔹 **4NF (Fourth Normal Form)**

**💡 Rule:** No **multi-valued dependencies**

🔸 **Shortcut:** **“1 fact per row”**

### ❌ Bad (Not 4NF)

```text
| Student | Hobby    | Language |
|---------|----------|----------|
| Liju    | Music    | English  |
| Liju    | Music    | French   |
| Liju    | Sports   | English  |
| Liju    | Sports   | French   |
```

> Multiple values of unrelated facts (Hobby, Language)

### ✅ Good (4NF)

**StudentHobbies:**

```text
| Student | Hobby  |
|---------|--------|
| Liju    | Music  |
| Liju    | Sports |
```

**StudentLanguages:**

```text
| Student | Language |
|---------|----------|
| Liju    | English  |
| Liju    | French   |
```

🟩 **Why use:** Avoids exponential rows  
🟥 **Why not:** Too theoretical for most OLTP systems

---

## 🔹 **5NF (Fifth Normal Form / PJNF)**

**💡 Rule:** No **join dependency** issues. All joins are **lossless**.

🔸 **Shortcut:** **“Split until only necessary joins remain”**

Mostly applies in extremely complex many-to-many relations (e.g., product, supplier, region).

🟩 **Why use:** Ultimate normalization  
🟥 **Why not:** Rarely needed unless doing advanced modeling

---

## ✅ Summary Table

|NF|Rule|Why Use|Why Not|
|---|---|---|---|
|1NF|Atomic values only|Simple, queryable data|More rows|
|2NF|No partial dependencies|Remove redundancy in composite keys|Extra tables|
|3NF|No transitive dependencies|Avoid anomalies|Join cost|
|BCNF|Every determinant is a key|Stronger integrity|Often overkill|
|4NF|No multi-valued dependencies|Avoid row multiplication|Rare in real-world|
|5NF|No join dependency|Only minimal joins needed|Theoretical, not usually practical|

---

## 🧠 Quick Mnemonic (for remembering the order)

**"A**ll **P**eople **T**ry **B**uying **M**any **J**ackets"

→  
**1NF = Atomic**  
**2NF = Partial (no)**  
**3NF = Transitive (no)**  
**BCNF = Boyce-Codd (strong 3NF)**  
**4NF = Multi-valued (no)**  
**5NF = Join dependency (no)**

---

Want cheat sheets, ER diagram examples, or real SQL examples next?