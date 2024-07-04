# tes
 study case database *

Berikut adalah contoh structure database dan data menggunakan SQL untuk studi kasus baru:
CREATE TABLE teachers ( id INT AUTO_INCREMENT, name VARCHAR(100), subject VARCHAR(50), PRIMARY KEY(id) ); INSERT INTO teachers (name, subject) VALUES ('Pak Anton', 'Matematika'); INSERT INTO teachers (name, subject) VALUES ('Bu Dina', 'Bahasa Indonesia'); INSERT INTO teachers (name, subject) VALUES ('Pak Eko', 'Biologi'); CREATE TABLE classes ( id INT AUTO_INCREMENT, name VARCHAR(50), teacher_id INT, PRIMARY KEY(id), FOREIGN KEY (teacher_id) REFERENCES teachers(id) ); INSERT INTO classes (name, teacher_id) VALUES ('Kelas 10A', 1); INSERT INTO classes (name, teacher_id) VALUES ('Kelas 11B', 2); INSERT INTO classes (name, teacher_id) VALUES ('Kelas 12C', 3); CREATE TABLE students ( id INT AUTO_INCREMENT, name VARCHAR(100), age INT, class_id INT, PRIMARY KEY(id), FOREIGN KEY (class_id) REFERENCES classes(id) ); INSERT INTO students (name, age, class_id) VALUES ('Budi', 16, 1); INSERT INTO students (name, age, class_id) VALUES ('Ani', 17, 2); INSERT INTO students (name, age, class_id) VALUES ('Candra', 18, 3); 
1. Tampilkan daftar siswa beserta kelas dan guru yang mengajar kelas tersebut.
2. Tampilkan daftar kelas yang diajar oleh guru yang sama.
3. buat query view untuk siswa, kelas, dan guru yang mengajar
4. buat query yang sama tapi menggunakan store_procedure
5. buat query input, yang akan memberikan warning error jika ada data yang sama pernah masuk
## Jawaban
1. select * from students INNER JOIN classes ON students.class_id = classes.id INNER JOIN teachers ON classes.teacher_id = teachers.id;
2. s
3. create view siswa AS select * from students; create view kelas AS select * from classes; create view guru AS select * from teachers;
4. mysql> delimiter //
   mysql> create procedure selectAllStudents()
       -> BEGIN
       -> select * from students;
       -> END;
       -> //
   mysql> delimiter ;
   mysql> call selectAllStudents();

   mysql> delimiter //
   mysql> create procedure selectAllClasses()
       -> BEGIN
       -> select * from classes;
       -> END;
       -> //
   mysql> delimiter ;
   mysql> call selectAllClassses();

   mysql> delimiter //
   mysql> create procedure selectAllTeachers()
       -> BEGIN
       -> select * from teachers;
       -> END;
       -> //
   mysql> delimiter ;
   mysql> call selectAllTeachers();
5. 
