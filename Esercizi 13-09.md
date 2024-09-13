GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno
2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
3. Calcolare la media dei voti di ogni appello d'esame
4. Contare quanti corsi di laurea ci sono per ogni dipartimento

risposte:

1. SELECT COUNT() AS number_students_for_year, YEAR(enrolment_date) AS entolment_year
   FROM students
   GROUP BY YEAR(enrolment_date)

2. SELECT COUNT() AS teachers_quantity, office_address
   FROM teachers
   GROUP BY office_address

3. SELECT AVG(vote) AS voto_medio, exam_id
   FROM exam_student
   GROUP BY exam_id

4. SELECT COUNT(\*) AS degrees_number, department_id
   FROM degrees
   GROUP BY department_id
