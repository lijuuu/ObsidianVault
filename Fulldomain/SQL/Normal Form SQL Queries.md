### ✅ **Normalization Cheatsheet with ER Diagrams & SQL Examples**

---

## 🔹 1NF (Atomic Values Only)

### ❌ Bad Table

```text
| ID | Name  | Phones        |
|----|-------|---------------|
| 1  | Alice | 123, 456      |
```

### ✅ Good 1NF

```text
| ID | Name  | Phone |
|----|-------|-------|
| 1  | Alice | 123   |
| 1  | Alice | 456   |
```

📌 **ER Diagram (1NF)**

```
Customer
---------
ID (PK)
Name

Phone
---------
ID (FK)
Phone
```

---

## 🔹 2NF (No Partial Dependency)

> Applies only if composite PK exists

### ❌ Bad Table

```text
| OrderID | ProductID | ProductName | Qty |
|---------|-----------|-------------|-----|
| 101     | 1         | Keyboard    | 2   |
```

### ✅ Good 2NF

```sql
CREATE TABLE Products (
  ProductID INT PRIMARY KEY,
  ProductName VARCHAR(100)
);

CREATE TABLE OrderDetails (
  OrderID INT,
  ProductID INT,
  Qty INT,
  PRIMARY KEY (OrderID, ProductID),
  FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);
```

📌 **ER Diagram (2NF)**

```
Orders           Products
--------         ---------
OrderID (PK)     ProductID (PK)
                 ProductName

OrderDetails
-------------
OrderID (PK, FK)
ProductID (PK, FK)
Qty
```

---

## 🔹 3NF (No Transitive Dependency)

### ❌ Bad Table

```text
| EmpID | EmpName | DeptID | DeptName |
|-------|---------|--------|----------|
| 1     | Liju    | 10     | HR       |
```

### ✅ Good 3NF

```sql
CREATE TABLE Departments (
  DeptID INT PRIMARY KEY,
  DeptName VARCHAR(50)
);

CREATE TABLE Employees (
  EmpID INT PRIMARY KEY,
  EmpName VARCHAR(50),
  DeptID INT,
  FOREIGN KEY (DeptID) REFERENCES Departments(DeptID)
);
```

📌 **ER Diagram (3NF)**

```
Employees        Departments
----------       ------------
EmpID (PK)       DeptID (PK)
EmpName          DeptName
DeptID (FK)
```

---

## 🔹 BCNF (Every Determinant is Candidate Key)

### ❌ Bad Case

If `Instructor → Course`, but `Course` is not the PK.

```text
| Course | Instructor | Room  |
|--------|------------|-------|
| Math   | John       | A1    |
```

### ✅ Fix by splitting:

```sql
CREATE TABLE Instructors (
  Instructor VARCHAR(50) PRIMARY KEY,
  Course VARCHAR(50)
);

CREATE TABLE CourseRooms (
  Course VARCHAR(50),
  Room VARCHAR(10),
  PRIMARY KEY (Course, Room)
);
```

📌 **ER Diagram (BCNF)**

```
Instructors       CourseRooms
------------      -------------
Instructor (PK)   Course (PK)
Course            Room (PK)
```

---

## 🔹 4NF (No Multi-Valued Dependencies)

### ❌ Bad Table

```text
| Student | Hobby   | Language |
|---------|---------|----------|
| Liju    | Music   | English  |
| Liju    | Music   | Hindi    |
| Liju    | Sports  | English  |
```

### ✅ Good 4NF

```sql
CREATE TABLE StudentHobbies (
  Student VARCHAR(50),
  Hobby VARCHAR(50),
  PRIMARY KEY (Student, Hobby)
);

CREATE TABLE StudentLanguages (
  Student VARCHAR(50),
  Language VARCHAR(50),
  PRIMARY KEY (Student, Language)
);
```

📌 **ER Diagram (4NF)**

```
StudentHobbies        StudentLanguages
---------------       -----------------
Student (PK)          Student (PK)
Hobby (PK)            Language (PK)
```

---

## 🔹 5NF (Join Dependency)

> Complex decompositions (very rare).

### Example:

A supplier supplies parts to projects.

```sql
-- Three separate relations to handle supplier-part-project
CREATE TABLE SupplierProject (
  SupplierID INT,
  ProjectID INT
);

CREATE TABLE SupplierPart (
  SupplierID INT,
  PartID INT
);

CREATE TABLE ProjectPart (
  ProjectID INT,
  PartID INT
);
```

📌 **Used in:** Advanced modeling (data warehouses, etc.)

---

## 🧠 Shortcuts Summary

| NF   | Rule                     | Think Like...                      |
| ---- | ------------------------ | ---------------------------------- |
| 1NF  | Atomic values            | "No commas inside cells"           |
| 2NF  | Full key dependency      | "Whole key → whole row"            |
| 3NF  | No transitive dependency | "Only keys link values"            |
| BCNF | Stronger 3NF             | "Everything that determines = key" |
| 4NF  | No multi-valued facts    | "1 fact per row"                   |
| 5NF  | No join dependency       | "Split to purest relations"        |
