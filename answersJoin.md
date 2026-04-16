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