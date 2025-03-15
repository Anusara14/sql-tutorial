
# **SQL Commands Tutorial & Outputs**

---

## **1. Retrieving Data**

### **Basic SELECT Statements**

#### **Command:**
```sql
SELECT FirstName, LastName, Email FROM Students;
```

#### **Output:**
|    | FirstName   | LastName   | Email                     |
|---:|:------------|:-----------|:--------------------------|
|  0 | Alice       | Johnson    | alice.johnson@example.com |
|  1 | Bob         | Smith      | bob.smith@example.com     |
|  2 | Charlie     | Brown      | charlie.brown@example.com |
|  3 | David       | White      | david.white@example.com   |
|  4 | Emma        | Davis      | emma.davis@example.com    |

---

## **2. Advanced Filtering**

### **Students Enrolled in March 2024**

#### **Command:**
```sql
SELECT * FROM Students WHERE EnrollmentDate BETWEEN '2024-03-01' AND '2024-03-31';
```

#### **Output:**
|    |   StudentID | FirstName   | LastName   | Email                     | EnrollmentDate   |
|---:|------------:|:------------|:-----------|:--------------------------|:-----------------|
|  2 |           3 | Charlie     | Brown      | charlie.brown@example.com | 2024-03-05       |

### **Students Whose First Name Contains 'A'**

#### **Command:**
```sql
SELECT * FROM Students WHERE FirstName LIKE '%A%';
```

#### **Output:**
|    |   StudentID | FirstName   | LastName   | Email                     | EnrollmentDate   |
|---:|------------:|:------------|:-----------|:--------------------------|:-----------------|
|  0 |           1 | Alice       | Johnson    | alice.johnson@example.com | 2024-01-10       |
|  2 |           3 | Charlie     | Brown      | charlie.brown@example.com | 2024-03-05       |
|  3 |           4 | David       | White      | david.white@example.com   | 2024-04-12       |
|  4 |           5 | Emma        | Davis      | emma.davis@example.com    | 2024-05-20       |

---

## **3. DISTINCT and TOP**

### **Distinct Course Durations**

#### **Command:**
```sql
SELECT DISTINCT CourseDuration FROM Courses;
```

#### **Output:**
|    |   CourseDuration |
|---:|-----------------:|
|  0 |               12 |
|  1 |               10 |
|  2 |                8 |
|  3 |               14 |
|  4 |               16 |

### **Top 3 Newest Students**

#### **Command:**
```sql
SELECT TOP 3 * FROM Students ORDER BY EnrollmentDate DESC;
```

#### **Output:**
|    |   StudentID | FirstName   | LastName   | Email                     | EnrollmentDate   |
|---:|------------:|:------------|:-----------|:--------------------------|:-----------------|
|  4 |           5 | Emma        | Davis      | emma.davis@example.com    | 2024-05-20       |
|  3 |           4 | David       | White      | david.white@example.com   | 2024-04-12       |
|  2 |           3 | Charlie     | Brown      | charlie.brown@example.com | 2024-03-05       |

---

## **4. Sorting and Aggregation**

### **Sorting Courses by Duration**

#### **Command:**
```sql
SELECT * FROM Courses ORDER BY CourseDuration ASC;
```

#### **Output:**
|    |   CourseID | CourseName                  |   CourseDuration |
|---:|-----------:|:----------------------------|-----------------:|
|  2 |          3 | AI Ethics                   |                8 |
|  1 |          2 | Deep Learning               |               10 |
|  0 |          1 | Machine Learning            |               12 |
|  3 |          4 | Computer Vision             |               14 |
|  4 |          5 | Natural Language Processing |               16 |

---

## **5. Aggregation (Separate Tables)**

### **Total Students**
```sql
SELECT COUNT(*) AS TotalStudents FROM Students;
```
|    | Metric         |   Value |
|---:|:---------------|--------:|
|  0 | Total Students |       5 |

### **Earliest Enrollment**
```sql
SELECT MIN(EnrollmentDate) AS FirstEnrollment FROM Students;
```
|    | Metric              | Value      |
|---:|:--------------------|:-----------|
|  0 | Earliest Enrollment | 2024-01-10 |

### **Latest Enrollment**
```sql
SELECT MAX(EnrollmentDate) AS LastEnrollment FROM Students;
```
|    | Metric            | Value      |
|---:|:------------------|:-----------|
|  0 | Latest Enrollment | 2024-05-20 |

### **Average Course Duration**
```sql
SELECT AVG(CourseDuration) AS AvgCourseDuration FROM Courses;
```
|    | Metric                  |   Value |
|---:|:------------------------|--------:|
|  0 | Average Course Duration |      12 |

---

## **6. GROUP BY and HAVING**

### **Enrollments Grouped by Course**
```sql
SELECT C.CourseName, COUNT(E.StudentID) AS EnrolledStudents
FROM Courses C
LEFT JOIN Enrollments E ON C.CourseID = E.CourseID
GROUP BY C.CourseName;
```
|    | CourseName                  |   EnrolledStudents |
|---:|:----------------------------|-------------------:|
|  0 | AI Ethics                   |                  1 |
|  1 | Computer Vision             |                  1 |
|  2 | Deep Learning               |                  1 |
|  3 | Machine Learning            |                  1 |
|  4 | Natural Language Processing |                  1 |

### **Find Courses with More than 1 Student Enrolled**
```sql
SELECT CourseID, COUNT(StudentID) AS TotalEnrolled
FROM Enrollments
GROUP BY CourseID
HAVING COUNT(StudentID) > 1;
```
No courses with more than 1 student enrolled.

---

## **7. JOIN Operations**

### **INNER JOIN (Students with Courses)**
```sql
SELECT S.FirstName, S.LastName, C.CourseName
FROM Students S
INNER JOIN Enrollments E ON S.StudentID = E.StudentID
INNER JOIN Courses C ON E.CourseID = C.CourseID;
```
|    | FirstName   | LastName   | CourseName                  |
|---:|:------------|:-----------|:----------------------------|
|  0 | Alice       | Johnson    | Machine Learning            |
|  1 | Bob         | Smith      | Deep Learning               |
|  2 | Charlie     | Brown      | AI Ethics                   |
|  3 | David       | White      | Computer Vision             |
|  4 | Emma        | Davis      | Natural Language Processing |

### **LEFT JOIN (All Students Including Unenrolled)**
```sql
SELECT S.FirstName, S.LastName, C.CourseName
FROM Students S
LEFT JOIN Enrollments E ON S.StudentID = E.StudentID
LEFT JOIN Courses C ON E.CourseID = C.CourseID;
```
|    | FirstName   | LastName   | CourseName                  |
|---:|:------------|:-----------|:----------------------------|
|  0 | Alice       | Johnson    | Machine Learning            |
|  1 | Bob         | Smith      | Deep Learning               |
|  2 | Charlie     | Brown      | AI Ethics                   |
|  3 | David       | White      | Computer Vision             |
|  4 | Emma        | Davis      | Natural Language Processing |

### **RIGHT JOIN (All Courses Including Unenrolled)**
(Simulated using LEFT JOIN in SQL Server)
```sql
SELECT C.CourseName, COUNT(E.StudentID) AS EnrolledStudents
FROM Courses C
LEFT JOIN Enrollments E ON C.CourseID = E.CourseID
GROUP BY C.CourseName;
```
|    | CourseName                  |   EnrolledStudents |
|---:|:----------------------------|-------------------:|
|  0 | AI Ethics                   |                  1 |
|  1 | Computer Vision             |                  1 |
|  2 | Deep Learning               |                  1 |
|  3 | Machine Learning            |                  1 |
|  4 | Natural Language Processing |                  1 |

### **FULL JOIN (All Students & Courses)**
(Simulated using UNION of LEFT and RIGHT JOIN results)
|    | FirstName   | LastName   | CourseName                  |
|---:|:------------|:-----------|:----------------------------|
|  0 | Alice       | Johnson    | Machine Learning            |
|  1 | Bob         | Smith      | Deep Learning               |
|  2 | Charlie     | Brown      | AI Ethics                   |
|  3 | David       | White      | Computer Vision             |
|  4 | Emma        | Davis      | Natural Language Processing |
|  5 | None        | None       | AI Ethics                   |
|  6 | None        | None       | Computer Vision             |
|  7 | None        | None       | Deep Learning               |
|  8 | None        | None       | Machine Learning            |
|  9 | None        | None       | Natural Language Processing |

---

## **8. Modifying Data (UPDATE, INSERT, DELETE)**

#### **Update a Student's Email**
```sql
UPDATE Students SET Email = 'emma.davis.new@example.com' WHERE StudentID = 5;
```
✅ **Email updated for StudentID = 5**

#### **Insert a New Student**
```sql
INSERT INTO Students (FirstName, LastName, Email, EnrollmentDate) VALUES ('Sophia', 'Anderson', 'sophia.anderson@example.com', '2024-06-10');
```
✅ **New student added**

#### **Delete a Student**
```sql
DELETE FROM Students WHERE StudentID = 5;
```
✅ **Student removed**

---
