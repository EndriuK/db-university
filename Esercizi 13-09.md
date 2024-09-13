GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno
2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
3. Calcolare la media dei voti di ogni appello d'esame
4. Contare quanti corsi di laurea ci sono per ogni dipartimento

5. SELECT COUNT() AS number_students_for_year, YEAR(enrolment_date) AS entolment_year
   FROM students
   GROUP BY YEAR(enrolment_date)
