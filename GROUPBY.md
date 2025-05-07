# MySQL GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno
```
SELECT COUNT(YEAR(`enrolment_date`)), YEAR(`enrolment_date`)
FROM `students`
GROUP BY YEAR(`enrolment_date`)
```
2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
```
SELECT COUNT(`office_address`) AS 'insegnati', `office_address`
FROM teachers
GROUP BY `office_address`
```
3. Calcolare la media dei voti di ogni appello d'esame
```
SELECT CAST(AVG(`vote`) AS DECIMAL(5,2)) AS 'voto_medio',`exam_id`
FROM exam_student
GROUP BY `exam_id`

```
4. Contare quanti corsi di laurea ci sono per ogni dipartimento
```
SELECT COUNT(`degrees`.`name`) AS 'corsi_di_lauera',`departments`.`name`
FROM `departments`
INNER JOIN `degrees` ON `degrees`.`department_id` = `departments`.`id` 
GROUP BY `departments`.`name`
```