# MySQL JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
```
SELECT `students`.* 
FROM `degrees`
INNER JOIN `students` ON `degrees`.`id` = `students`.`degree_id` 
WHERE `degrees`.`name` = 'Corso di Laurea in Economia'
```
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze
```
SELECT * 
FROM `departments`
INNER JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'
AND `degrees`.`level` = 'magistrale'
```
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
```
SELECT * 
FROM `teachers`
INNER JOIN `course_teacher` ON  `teachers`.`id` = `course_teacher`.`teacher_id`
INNER JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
WHERE `teachers`.`id` = 44
```
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome
```
SELECT * 
FROM `departments`
INNER JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id`
INNER JOIN `students` ON `degrees`.`id` = `students`.`degree_id`
ORDER BY `students`.`name`,`students`.`surname`
```
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
```
SELECT * 
FROM `degrees`
INNER JOIN `courses` ON `courses`.`degree_id` = `degrees`.`id`
INNER JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
```
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)
```
SELECT `teachers`.*
FROM `teachers`
INNER JOIN `course_teacher` ON  `teachers`.`id` = `course_teacher`.`teacher_id`
INNER JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = 'Dipartimento di Matematica'
GROUP BY `teachers`.`id`
```
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.
```
SELECT COUNT(`exam_student`.`student_id`) AS 'tentativi_sostenuti',MAX(`exam_student`.`vote`) AS 'voto_massimo',`students`.`name`,`students`.`surname`
FROM `students`
INNER JOIN `exam_student` ON `students`.`id` = `exam_student`.`student_id`
GROUP BY `students`.`id`

```