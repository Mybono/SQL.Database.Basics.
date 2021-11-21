+ Показать информацию по потокам. В отчет вывести номер потока, название курса и дату начала занятий.
+ Найти общее количество учеников для каждого курса. В отчет вывести название курса и количество учеников по всем потокам курса.
+ Найти среднюю оценку по всем потокам для всех учителей. В отчет вывести идентификатор, фамилию и имя учителя, 
  среднюю оценку по всем проведенным потокам. Учителя, у которых не было потоков, также должны попасть в выборку.


```
.open teachers.db
.header on
.mode column
.schema
.tables

SELECT number, name, started_at
	FROM courses
	JOIN training_groups
		ON courses.id = training_groups.course_id;

SELECT name as course_name, SUM(students_amount) as students_amount
	FROM training_groups
	JOIN courses
		ON courses.id = training_groups.course_id
GROUP BY name;

SELECT id, surname, name, AVG(progress.grade) as avg_grade
	FROM teachers 
	LEFT JOIN progress 
		ON teachers.id = progress.teacher_id
GROUP BY teacher_id;

SELECT teachers.name, surname, MIN(progress.grade) as min_grade, courses.name
FROM teachers 
	LEFT JOIN progress
	ON teachers.id = progress.stream_id
	LEFT JOIN courses
	ON courses.id = progress.stream_id
GROUP BY surname;

.quit

```
