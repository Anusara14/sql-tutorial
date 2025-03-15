
# **SQL Commands Tutorial & Outputs**

---

## **1. Retrieving Data**

### **Basic SELECT Statements**

#### **Command:**
```sql
SELECT FirstName, LastName, Email FROM Students;
```

#### **Output:**
```
+-----------+----------+-----------------------------+
| FirstName | LastName | Email                       |
+-----------+----------+-----------------------------+
| Alice     | Johnson  | alice.johnson@example.com   |
| Bob       | Smith    | bob.smith@example.com       |
| Charlie   | Brown    | charlie.brown@example.com   |
| David     | White    | david.white@example.com     |
| Emma      | Davis    | emma.davis@example.com      |
+-----------+----------+-----------------------------+
```

---

## **2. Advanced Filtering**

### **Students Enrolled in March 2024**

#### **Command:**
```sql
SELECT * FROM Students WHERE EnrollmentDate BETWEEN '2024-03-01' AND '2024-03-31';
```

#### **Output:**
```
+-----------+-----------+----------+---------------------------+----------------+
| StudentID | FirstName | LastName | Email                     | EnrollmentDate |
+-----------+-----------+----------+---------------------------+----------------+
| 3         | Charlie   | Brown    | charlie.brown@example.com | 2024-03-05     |
+-----------+-----------+----------+---------------------------+----------------+
```

### **Students Whose First Name Contains 'A'**

#### **Command:**
```sql
SELECT * FROM Students WHERE FirstName LIKE '%A%';
```

#### **Output:**
```
+-----------+-----------+----------+-----------------------------+----------------+
| StudentID | FirstName | LastName | Email                       | EnrollmentDate |
+-----------+-----------+----------+-----------------------------+----------------+
| 1         | Alice     | Johnson  | alice.johnson@example.com   | 2024-01-10     |
| 3         | Charlie   | Brown    | charlie.brown@example.com   | 2024-03-05     |
| 4         | David     | White    | david.white@example.com     | 2024-04-12     |
| 5         | Emma      | Davis    | emma.davis@example.com      | 2024-05-20     |
+-----------+-----------+----------+-----------------------------+----------------+
```

---

## **3. DISTINCT and TOP**

### **Distinct Course Durations**

#### **Command:**
```sql
SELECT DISTINCT CourseDuration FROM Courses;
```

#### **Output:**
```
+----------------+
| CourseDuration |
+----------------+
| 12             |
| 10             |
| 8              |
| 14             |
| 16             |
+----------------+
```

### **Top 3 Newest Students**

#### **Command:**
```sql
SELECT TOP 3 * FROM Students ORDER BY EnrollmentDate DESC;
```

#### **Output:**
```
+-----------+-----------+----------+---------------------------+----------------+
| StudentID | FirstName | LastName | Email                     | EnrollmentDate |
+-----------+-----------+----------+---------------------------+----------------+
| 5         | Emma      | Davis    | emma.davis@example.com    | 2024-05-20     |
| 4         | David     | White    | david.white@example.com   | 2024-04-12     |
| 3         | Charlie   | Brown    | charlie.brown@example.com | 2024-03-05     |
+-----------+-----------+----------+---------------------------+----------------+
```

---

## **4. Sorting and Aggregation**

### **Sorting Courses by Duration**

#### **Command:**
```sql
SELECT * FROM Courses ORDER BY CourseDuration ASC;
```

#### **Output:**
```
+----------+---------------------------+----------------+
| CourseID | CourseName                | CourseDuration |
+----------+---------------------------+----------------+
| 3        | AI Ethics                 | 8              |
| 2        | Deep Learning             | 10             |
| 1        | Machine Learning          | 12             |
| 4        | Computer Vision           | 14             |
| 5        | Natural Language Processing| 16            |
+----------+---------------------------+----------------+
```

---

## **5. Aggregation (Separate Tables)**

### **Total Students**
```sql
SELECT COUNT(*) AS TotalStudents FROM Students;
```
```
+----------------+---------+
| Metric         |  Value  |
+----------------+---------+
| Total Students |    5    |
+----------------+---------+
```

### **Earliest Enrollment**
```sql
SELECT MIN(EnrollmentDate) AS FirstEnrollment FROM Students;
```
```
+---------------------+------------+
| Metric              | Value      |
+---------------------+------------+
| Earliest Enrollment | 2024-01-10 |
+---------------------+------------+
```

### **Latest Enrollment**
```sql
SELECT MAX(EnrollmentDate) AS LastEnrollment FROM Students;
```
```
+-------------------+------------+
| Metric            | Value      |
+-------------------+------------+
| Latest Enrollment | 2024-05-20 |
+-------------------+------------+
```

### **Average Course Duration**
```sql
SELECT AVG(CourseDuration) AS AvgCourseDuration FROM Courses;
```
```
+-------------------------+---------+
| Metric                  |  Value  |
+-------------------------+---------+
| Average Course Duration |   12    |
+-------------------------+---------+
```

---

## **6. GROUP BY and HAVING**

### **Enrollments Grouped by Course**
```sql
SELECT C.CourseName, COUNT(E.StudentID) AS EnrolledStudents
FROM Courses C
LEFT JOIN Enrollments E ON C.CourseID = E.CourseID
GROUP BY C.CourseName;
```
```
+---------------------------+------------------+
| CourseName                | EnrolledStudents |
+---------------------------+------------------+
| AI Ethics                 | 1                |
| Computer Vision           | 1                |
| Deep Learning             | 1                |
| Machine Learning          | 1                |
| Natural Language Processing| 1               |
+---------------------------+------------------+
```

### **Find Courses with More than 1 Student Enrolled**
```sql
SELECT CourseID, COUNT(StudentID) AS TotalEnrolled
FROM Enrollments
GROUP BY CourseID
HAVING COUNT(StudentID) > 1;
```
No courses with more than 1 student enrolled.

---

This is the **complete and final SQL tutorial** with structured commands and formatted output tables.
