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

<------------------------------------------------------------->
JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
   Neuroscienze
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
   sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
   nome
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
   Matematica (54)
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
   per ogni esame, stampando anche il voto massimo. Successivamente,
   filtrare i tentativi con voto minimo 18.

risposte:

1. SELECT students.name, students.surname, students.registration_number
   FROM students
   JOIN degrees ON students.degree_id = degrees.id
   WHERE degrees.name = 'Corso di Laurea in Economia';

2. SELECT degrees.name AS nome_corso, departments.name AS nome_dipartimento
   FROM degrees
   JOIN departments ON degrees.department_id = departments.id
   WHERE departments.name = 'Dipartimento di Neuroscienze'
   AND degrees.level = 'magistrale';

3. SELECT courses.name AS corsi_di_Fuvio_Amato
   FROM courses
   JOIN course_teacher ON courses.id = course_teacher.course_id
   JOIN teachers ON teachers.id = course_teacher.teacher_id
   WHERE teachers.id = 44
