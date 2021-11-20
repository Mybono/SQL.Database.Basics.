+ Найти потоки, количество учеников в которых больше или равно 40. В отчёт вывести номер потока, название курса и количество учеников.
+ Найти два потока с самыми низкими оценками за успеваемость. В отчёт вывести номер потока, название курса, фамилию и имя преподавателя (одним столбцом), оценку успеваемости.
+ Найти среднюю успеваемость всех потоков преподавателя Николая Савельева. В отчёт вывести идентификатор преподавателя и среднюю оценку по потокам.
+ Найти потоки преподавателя Натальи Петровой а также потоки, по которым успеваемость ниже 4.8. В отчёт вывести идентификатор потока, фамилию и имя преподавателя.

```
.open teachers.db
.header on
.mode column
SELECT number, (SELECT name FROM courses WHERE courses.id = training_groups.course_id) AS course_name, students_amount FROM training_groups WHERE students_amount >= 40;

SELECT MIN(grade),
	(SELECT name FROM courses WHERE id = stream_id) AS course_name, 
	(SELECT name || surname FROM teachers WHERE id = teacher_id) AS teacher_name FROM progress;
  
SELECT (SELECT id FROM teachers WHERE surname = 'Савельев' AND name = 'Николай') AS teacher_id, 
AVG(grade)
FROM progress WHERE (SELECT id FROM teachers WHERE surname = 'Савельев' AND name = 'Николай');

SELECT number FROM training_groups WHERE id = (SELECT stream_id FROM progress WHERE teacher_id = (SELECT id FROM teachers WHERE surname = 'Петрова' AND name = 'Наталья'))
UNION ALL
SELECT
(SELECT name || surname FROM teachers WHERE id = teacher_id) AS teacher_name FROM progress
WHERE grade < 4.8;
.quit
```
