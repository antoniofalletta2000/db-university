# Contare quanti iscritti ci sono stati ogni anno
SELECT YEAR(enrolment_date) AS anno, COUNT(*) AS "numero di iscritti"
FROM students
GROUP BY anno 
ORDER BY anno ASC;

# Contare gli insegnanti che hanno l'ufficio nello stesso edificio
SELECT office_address AS ufficio, COUNT(*) AS personale
FROM teachers
GROUP BY teachers.office_address;

#  Calcolare la media dei voti di ogni appello d'esame
SELECT exam_id AS "appello d'esame", CEIL(AVG(vote)) AS "media voti"
FROM exam_student
GROUP BY exam_id;

# Contare quanti corsi di laurea ci sono per ogni dipartimento
SELECT departments.name AS department, COUNT(*) AS "quantità di corsi"
FROM degrees
JOIN departments ON departments.id = degrees.department_id
GROUP BY departments.id;
