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

4. SELECT students.surname, students.name, departments.name AS name_department, degrees.name AS name_degree
   FROM students
   JOIN degrees ON students.degree_id = degrees.id
   JOIN departments ON degrees.department_id = departments.id
   ORDER BY students.surname, students.name

5. SELECT degrees.name AS name_degree, courses.name AS name_course, teachers.name AS name_teacher, teachers.surname AS surname_teacher
   FROM degrees
   JOIN courses ON courses.degree_id = degrees.id
   JOIN course_teacher ON course_teacher.course_id = courses.id
   JOIN teachers ON course_teacher.teacher_id = teachers.id
   ORDER BY name_degree, name_course

6. SELECT teachers.name, teachers.surname
   FROM teachers
   JOIN course_teacher ON course_teacher.teacher_id = teachers.id
   JOIN courses ON course_teacher.course_id = courses.id
   JOIN degrees ON courses.degree_id = degrees.id
   JOIN departments ON degrees.department_id = departments.id
   WHERE departments.name = 'Dipartimento di Matematica'

7. SELECT students.id, students.surname, students.name, courses.name AS exam_name, COUNT(exam_student.exam_id) AS attempt_count, MAX(exam_student.vote) AS max_vote
   FROM exam_student
   JOIN students ON exam_student.student_id = students.id
   JOIN exams ON exam_student.exam_id = exams.id
   JOIN courses ON exams.course_id = courses.id
   WHERE exam_student.vote >= 18
   GROUP BY students.id, students.name, students.surname, courses.name
   ORDER BY students.surname, students.name;
