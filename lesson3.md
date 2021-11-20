#Работаем с базой данных teachers.db. В качестве отчёта необходимо сдать команды, которые выполнялись (в текстовом файле), а также файл базы данных.

##1. Переименовать таблицу streams в training_groups.
##2. В таблице training_groups переименовать столбец даты начала обучения в started_at.
##3. В таблице training_groups добавить столбец даты завершения обучения в finished_at.
##4. Привести данные в полное соответствие с таблицами 1-4 практического задания в методичке

```
.open teachers.db
.schema
.header on
.mode column
ALTER TABLE streams RENAME COLUMN start_date TO started_at;
ALTER TABLE streams ADD COLUMN finished_at TEXT;

INSERT INTO teachers (id, name, surname, email)  
VALUES (1, ‘Николай’, ‘Савельев’, ‘saveliev.n@mai.ru’), (2, ‘Наталья’, ‘Петрова’, ‘petrova.n@yandex.ru’), (3, ‘Елена’, ‘Малышева’, ‘malisheva.e@google.com’);

INSERT INTO courses (id, name) VALUES (1, ‘Базы данных’), (2, ‘Основы Python’), (3, ‘Linux. Рабочая станция’);

INSERT INTO streams (id, number, course_id, started_at, students_amount) VALUES (1, 165, 3, ‘18.08.2020’, 34), (2, 178, 2, ‘02.10.2020’, 37), (3, 203, 1, ‘12.11.2020’, 35), (4, 210, 1, ‘03.12.2020’, 41);

INSERT INTO progress (teacher_id, stream_id, grade) VALUES (3, 1, 4.7), (2, 2, 4.9);
INSERT INTO progress (teacher_id, stream_id, grade) VALUES (1, 3, 4.8), (1, 4, 4.9);

ALTER TABLE progress RENAME TO tmp;
CREATE TABLE progress(
  teacher_id INTEGER NOT NULL,
  stream_id INTEGER NOT NULL,
  grade REAL NOT NULL,
  PRIMARY KEY(teacher_id, stream_id),
  FOREIGN KEY (teacher_id) REFERENCES teachers(id),
  FOREIGN KEY (stream_id) REFERENCES streams(id)
);
INSERT INTO progress (teacher_id,  stream_id, grade) SELECTteacher_id,  stream_id, grade FROM tmp;
DROP TABLE tmp;

ALTER TABLE streams RENAME TO training_groups;
```
