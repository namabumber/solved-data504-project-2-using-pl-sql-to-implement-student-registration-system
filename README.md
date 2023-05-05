Download Link: https://assignmentchef.com/product/solved-data504-project-2-using-pl-sql-to-implement-student-registration-system
<br>
This project is to use Oracle’s PL/SQL to create an application to support typical student registration tasks in a university. Students are required to form teams of two members for this project.

Due to the time constraint, only a subset of the database tables and a subset of the needed functionalities will be implemented in this project.

<ol>

 <li><strong> Preparation </strong></li>

</ol>

The following tables from the Student Registration System will be used in this project:

<strong>Students(<u>B#</u>, first_name, last_name, status, gpa, email, bdate, deptname) </strong>

<strong>Courses(<u>prog_code, course#</u>, title) </strong>

<strong>            Classes(<u>classid</u>, prog_code, course#, sect#, year, semester, limit, class_size, room) </strong>         <strong>Enrollments(<u>B#, classid, </u>lgrade) </strong>




In addition, the following table is also required for this project: <strong>          </strong>

<strong> </strong>

<h1>                        Logs(<u>log#</u>, op_name, op_time, table_name, operation, key_value)</h1>




Each tuple in the logs table describes who (op_name – the login name of a database user) has performed what operation (insert, delete, update) on which table (table_name) and which tuple (as indicated by the value of the primary key, key_value, of the tuple) at what time (op_time). Attribute log# is the primary key of the table. op_name can be produced by system function “user” and op_time can be produced by system function “sysdate”.




The schemas and constraints of the first four tables are the same as those used in Project 1. Please use the following statements to create the Logs table (you can add them to the script file):




create table logs (log# number(4) primary key, op_name varchar2(10) not null, op_time date not null, table_name varchar2(12) not null, operation varchar2(6) not null, key_value varchar2(10));




<h1>2.  PL/SQL Implementation</h1>




You need to create a PL/SQL package for this application. All procedures and functions should be included in this package. <strong>Other Oracle objects such as sequences and triggers are to be created outside the package.</strong> The following requirements and functionalities need to be implemented.




<ol>

 <li>(4 points) Use a sequence to generate the values for log# automatically when new log records are inserted into the logs table. Start the sequence with 100 with an increment of 1.</li>

 <li>(8 points) Write procedures in your package to display the tuples in each of the five tables for this project. As an example, you can write a procedure, say <strong>show_students</strong>, to display all students in the students table.</li>

 <li>(30 points) Write a procedure in your package to enroll a student into a class (i.e., insert a tuple into the Enrollments table). The B# of the student and the classid of the class are provided as parameters (all new enrollments will have a null value for lgrade). In all the following cases, reject the enrollment request:

  <ol>

   <li>If the student is not in the Students table, report “The B# is invalid.”</li>

   <li>If the classid is not in the classes table, report “The classid is invalid.”</li>

   <li>If the class is not offered in Spring 2020 (treating it as the current semester), report</li>

  </ol></li>

</ol>

“Cannot enroll into a class from a previous semester.”

<ol>

 <li>If the class is already full before the enrollment request, report “The class is already full.”</li>

 <li>If the student is already in the class, report “The student is already in the class.”</li>

 <li>If the student is already enrolled in four other classes in the same semester and the same year, report “Students cannot enroll into more than four courses in the same semester.”</li>

</ol>

For all the other cases, the requested enrollment should be carried out successfully. You need to make sure that all data are consistent after each enrollment. For example, after you successfully enrolled a student into a class, the class size of the class should be increased by 1. Use trigger(s) to implement the updates of values caused by successfully enrolling a student into a class. (Once again, it is recommended that all triggers for this project be implemented outside of the package.)

<ol start="4">

 <li>(20 points) Write a procedure in your package to drop a student from a class (i.e., delete a</li>

</ol>

tuple from the Enrollments table). The B# of the student and the classid of the class are provided as parameters. In all the following cases, reject the drop request:

<ol>

 <li>If the student is not in the Students table, report “The B# is invalid.”</li>

 <li>If the classid is not in the Classes table, report “The classid is invalid.”</li>

 <li>If the student is not enrolled in the class, report “The student is not enrolled in the class.”</li>

 <li>If the class is not offered in Spring 2020, report “Only enrollment in the current semester can be dropped.”</li>

</ol>

In all the other cases, the student will be dropped from the class. If the class is the last class for the student, report “This student is not enrolled in any classes.”  If the student is the last student in the class, report “The class now has no students.” Again, you should make sure that all data are consistent after a successful enrollment drop and all updates caused by the drop need to be implemented using trigger(s).

<ol start="5">

 <li>(15 points) Write triggers to add tuples to the Logs table automatically whenever a student is successfully enrolled into or dropped from a class (i.e., when a tuple is inserted into or deleted from the Enrollments table). For a logs record for enrollments, the key value is the concatenation of the B# value, a comma, and the classid value.</li>

</ol>




<h1>3.  Documentation (15 points)</h1>




Documentation consists of the following aspects:




<ol>

 <li>Each procedure and function and every other object you create for your project needs to be explained clearly regarding its objective and usage.</li>

</ol>




<ol start="2">

 <li>Your code needs to be reasonably documented with in-line comments.</li>

</ol>




<ol start="3">

 <li><em>Team report</em>. This report should describe in reasonable detail how the team members collaborated for the project. More specifically, it needs to include the following information:

  <ol>

   <li>Your meetings (describe when each meeting occurred and what was discussed for the project at the meeting?)</li>

   <li>What was your plan (schedule) for completing your project? How was the plan followed during the course of completing the project?</li>

   <li>Which team member is primarily responsible for which part of the project? Did the other member contribute to the task primarily assigned to another member?</li>

  </ol></li>

</ol>


