+ Найти потоки, количество учеников в которых больше или равно 40. В отчёт вывести номер потока, название курса и количество учеников.
+ Найти два потока с самыми низкими оценками за успеваемость. В отчёт вывести номер потока, название курса, фамилию и имя преподавателя (одним столбцом), оценку успеваемости.
+ Найти среднюю успеваемость всех потоков преподавателя Николая Савельева. В отчёт вывести идентификатор преподавателя и среднюю оценку по потокам.
+ Найти потоки преподавателя Натальи Петровой а также потоки, по которым успеваемость ниже 4.8. В отчёт вывести идентификатор потока, фамилию и имя преподавателя.

```
.open teachers.db
.header on
.mode column

SELECT number, 
	(SELECT name FROM courses WHERE courses.id = training_groups.course_id)
		AS course_name, students_amount 
		FROM training_groups
			WHERE students_amount >= 40;

SELECT	
	(SELECT number FROM training_groups WHERE training_groups.id = progress.stream_id)
		AS stream_number,
	(SELECT name FROM courses WHERE courses.id = (SELECT course_id FROM training_groups WHERE id = progress.stream_id))
		AS course_name, 
	(SELECT name || ' ' || surname FROM teachers WHERE teachers.id = progress.teacher_id) AS teacher,
grade
	FROM progress
		ORDER BY grade
	LIMIT 2;
  
SELECT teacher_id, AVG(grade)
	FROM progress
		WHERE teacher_id = (SELECT id FROM teachers WHERE surname = 'Савельев' AND name = 'Николай');

SELECT stream_id,
 (SELECT name FROM teachers WHERE teachers.id = progress.teacher_id)
     AS teacher_name,
   (SELECT surname FROM teachers WHERE teachers.id = progress.teacher_id)
     AS teacher_surname
 FROM progress WHERE teacher_id = (SELECT id FROM teachers WHERE name = 'Наталья' AND surname = 'Петрова')
UNION
SELECT stream_id,
 (SELECT name FROM teachers WHERE teachers.id = progress.teacher_id)
     AS teacher_name,
   (SELECT surname FROM teachers WHERE teachers.id = progress.teacher_id)
     AS teacher_surname
 FROM progress WHERE grade < 4.8;
.quit
```
