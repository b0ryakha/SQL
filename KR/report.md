## Задания на «3»
### 1)
```sql
SELECT * FROM students;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/7643776d-adcd-4d13-b420-f5747f5b1205)

### 2)
```sql
SELECT firstname, lastname FROM students WHERE age > 21;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/c4f7835b-990b-46a6-9709-c97e62369e60)

### 3)
```sql
SELECT coursename FROM courses;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/7de466e4-606a-4399-95dd-f2e4c874fc4e)

### 4)
```sql
SELECT firstname, lastname FROM students
WHERE studentid IN (SELECT studentid FROM studentcourses WHERE courseid = (SELECT courseid FROM courses WHERE coursename = 'Математика'));
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/e36d056c-ed30-45a7-a373-d3142044ec42)

### 5)
```sql
SELECT firstname, lastname FROM students
WHERE age = 20 AND studentid IN (SELECT studentid FROM studentcourses WHERE courseid = (SELECT courseid FROM courses WHERE coursename = 'История'));
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/41d6a101-98d9-4b8c-bd1a-9e41cb83d0b4)

### 6)
```sql
SELECT courses.coursename, COUNT(studentcourses.studentid) FROM courses
JOIN studentcourses ON studentcourses.courseid = courses.courseid GROUP BY courses.courseid
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/765d3b31-0abc-48b2-9e49-63d9829c0567)

### 7)
```sql
SELECT AVG(age) FROM students;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/420080fe-b908-4b4e-9ed4-f6bd0dc8b502)

### 8)
```sql
SELECT firstname, lastname FROM students
WHERE studentid NOT IN (SELECT studentid FROM studentcourses)
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/f9dff843-d1aa-437a-848b-d2e845c6fadc)

### 9)
```sql
SELECT courses.coursename, COUNT(studentcourses.studentid) FROM courses
JOIN studentcourses ON studentcourses.courseid = courses.courseid GROUP BY courses.courseid
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/ce527a84-d3be-4653-b0dd-c07d36d9961f)

### 10)
```sql
SELECT firstname, lastname FROM students
WHERE age <= 22 AND studentid IN (SELECT studentid FROM studentcourses WHERE courseid = (SELECT courseid FROM courses WHERE coursename = 'Биология'));
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/a166bb0f-6832-4cf6-a080-a03d1fc37cae)



---



## Задания на «5»
### 1)
```sql
SELECT courses.coursename, COUNT(studentcourses.studentid) FROM courses
JOIN studentcourses ON studentcourses.courseid = courses.courseid GROUP BY courses.courseid
HAVING COUNT(studentcourses.studentid) >= 2
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/af33d268-4ecc-4854-9b17-e5ae454c3f30)

### 2)
```sql
SELECT courses.courseid, COUNT(studentcourses.studentid) INTO limit_courses FROM courses
JOIN studentcourses ON studentcourses.courseid = courses.courseid GROUP BY courses.courseid
HAVING COUNT(studentcourses.studentid) = 1;

SELECT firstname, lastname FROM students
WHERE studentid IN (SELECT studentcourses.studentid FROM studentcourses WHERE studentcourses.courseid IN (SELECT limit_courses.courseid FROM limit_courses));

DROP TABLE limit_courses;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/a2cfbe75-6872-4e0d-952f-3d721a17cc78)

### 3)
```sql
SELECT firstname, lastname FROM students
WHERE (SELECT COUNT(studentid) FROM studentcourses) = (SELECT COUNT(courseid) FROM courses)
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/70f0a6df-a18d-45b4-8adb-ab6a6cd52790)

### 4)
```sql
SELECT firstname, lastname FROM students
WHERE
	studentid NOT IN (SELECT studentid FROM studentcourses WHERE courseid = (SELECT courseid FROM courses WHERE coursename = 'Информатика'))
AND
	studentid IN (SELECT studentid FROM studentcourses)
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/1d0f93ef-e136-4422-8225-9853026b07fd)

### 5)
```sql
SELECT courses.coursename, COUNT(studentcourses.studentid) INTO tmp_table FROM courses
JOIN studentcourses ON studentcourses.courseid = courses.courseid GROUP BY courses.courseid
HAVING COUNT(studentcourses.studentid) = 0;

SELECT coursename FROM tmp_table;
DROP TABLE tmp_table;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/379670a3-502a-4366-a0d6-81371183b915)

### 6)
```sql
SELECT firstname, lastname FROM students
WHERE age = (SELECT MAX(age) FROM students);
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/106c08e4-2de4-4acd-8f99-ae3448e2a0cb)

### 7)
```sql
SELECT firstname, lastname FROM students
WHERE
	studentid IN (SELECT studentid FROM studentcourses WHERE courseid IN
		(SELECT courseid FROM courses WHERE courseid IN (SELECT courseid FROM studentcourses WHERE studentid = (SELECT studentid FROM students WHERE firstname = 'Иван'))))
AND
	NOT (firstname = 'Иван')
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/b0e0906c-94eb-4b67-bad4-6ca2284aebe6)

### 8)
```sql
SELECT firstname, lastname, age INTO biology_course FROM students
WHERE studentid IN (SELECT studentid FROM studentcourses WHERE courseid = (SELECT courseid FROM courses WHERE coursename = 'Биология'));

SELECT AVG(age) FROM biology_course;
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/7173364b-3917-4fe3-822f-aedb708c8cdd)

### 9)
```sql
SELECT firstname, lastname FROM students
WHERE
	studentid NOT IN (SELECT studentid FROM studentcourses)
AND
	age > 18
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/b1114cfd-98b9-426b-b90a-577c4fd05a46)

### 10)
```sql
SELECT firstname, lastname FROM students
WHERE (SELECT COUNT(studentid) FROM studentcourses) >= 2
```
![image](https://github.com/b0ryakha/SQL/assets/47691726/5659eb79-c15a-4203-b4fb-b251d4260676)
