# Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT students.id, students.name, students.surname,students.date_of_birth, students.fiscal_code, students.email, degrees.name
FROM students
JOIN degrees ON students.degree_id = degrees.id
WHERE degrees.name = "Corso di Laurea in Economia";

# Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

SELECT degrees.id,degrees.department_id, degrees.name, degrees.level, departments.name
FROM degrees
JOIN departments ON degrees.department_id = departments.id
WHERE departments.name = "Dipartimento di Neuroscienze" AND degrees.level="magistrale";

# Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT courses.id AS courses_id, courses.name AS courses, teachers.name AS teacher_name, teachers.surname AS teacher_surname
FROM courses
JOIN course_teacher ON courses.id = course_teacher.course_id
JOIN teachers ON course_teacher.teacher_id = teachers.id
WHERE teachers.id=44;

# Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
SELECT students.id AS student_id, students.name, students.surname, students.fiscal_code, students.registration_number, degrees.name AS degrees, departments.name AS department
FROM students
JOIN degrees ON students.degree_id = degrees.id
JOIN departments ON departments.id = degrees.department_id
ORDER BY students.surname ASC, students.name ASC;

# Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
SELECT degrees.name AS degrees, courses.name AS courses, teachers.name AS teacher_name, teachers.surname AS teacher_surname
FROM degrees
JOIN courses ON courses.degree_id = degrees.id
JOIN course_teacher ON course_teacher.course_id = courses.id
JOIN teachers ON teachers.id = course_teacher.teacher_id

# Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
SELECT DISTINCT teachers.name, teachers.surname, departments.name AS departments
FROM teachers
JOIN course_teacher ON course_teacher.teacher_id = teachers.id
JOIN courses ON courses.id = course_teacher.course_id
JOIN degrees ON degrees.id = courses.degree_id
JOIN departments ON departments.id = degrees.department_id
WHERE departments.name= "Dipartimento di Matematica";

## BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.
SELECT students.name, students.surname, COUNT(id) AS tentativi, MAX(exam_student.vote)
FROM students
JOIN exam_student ON exam_student.student_id = students.id
WHERE exam_student.vote>=18
GROUP BY students.id;