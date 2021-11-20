#### Работаем с базой данных учителей teachers.db. Для каждого из заданий необходимо создать запрос, сдать нужно только код запросов в текстовом файле.

##### + Преобразовать дату начала потока к виду год-месяц-день.
##### + Получить идентификатор и номер потока, который запланирован на самую позднюю дату.
##### + Показать уникальные значения года дат начала потоков обучения
##### + Найти количество преподавателей в базе данных. Вывести искомое значение в столбец с именем total_teachers.
##### + Показать даты начала двух последних по времени потоков.
##### + Найти среднюю успеваемости учеников по потоку преподавателя с идентификатором равным 1.

```
.open teachers.db
.header on
.mode column
.schema training_groups
SELECT SUBSTR(started_at, 7, 4) || '-' || SUBSTR(started_at, 4, 2) || '-' || SUBSTR(started_at, 1, 2) FROM training_groups;
UPDATE training_groups SET started_at = SUBSTR(started_at, 7, 4) || '-' || SUBSTR(started_at, 4, 2) || '-' || SUBSTR(started_at, 1, 2);
SELECT * FROM training_groups;
SELECT id, number, MAX(started_at) FROM training_groups; 
SELECT DISTINCT SUBSTR(started_at, 1, 4) FROM training_groups; 
SELECT id, COUNT(*) AS 'total_teachers' FROM teachers;
SELECT started_at FROM training_groups ORDER BY started_at DESC LIMIT 2;
SELECT teacher_id, AVG(grade) FROM progress WHERE teacher_id = 1;
.quit
```
