# sql_select

________________________________________________________________________________
Easy Challenge

mysql> select * from student;
+------------+------------+-----------+---------------------+------------+
| student_id | first_name | last_name | years_of_experience | start_date |
+------------+------------+-----------+---------------------+------------+
|          1 | Eric       | Ephram    |                   2 | 2016-03-31 |
|          2 | Greg       | Gould     |                   6 | 2016-09-30 |
|          3 | Adam       | Ant       |                   5 | 2016-06-02 |
|          4 | Howard     | Hess      |                   1 | 2016-02-28 |
|          5 | Charles    | Caldwell  |                   7 | 2016-05-07 |
|          6 | James      | Joyce     |                   9 | 2016-08-27 |
|          7 | Doug       | Dumas     |                  13 | 2016-07-04 |
|          8 | Kevin      | Kraft     |                   3 | 2016-04-15 |
|          9 | Frank      | Fountain  |                   8 | 2016-01-31 |
|         10 | Brian      | Biggs     |                   4 | 2015-12-25 |
+------------+------------+-----------+---------------------+------------+
10 rows in set (0.00 sec)

1. Create a list of students showing first and last names only.

mysql> select first_name, last_name from student;
+------------+-----------+
| first_name | last_name |
+------------+-----------+
| Eric       | Ephram    |
| Greg       | Gould     |
| Adam       | Ant       |
| Howard     | Hess      |
| Charles    | Caldwell  |
| James      | Joyce     |
| Doug       | Dumas     |
| Kevin      | Kraft     |
| Frank      | Fountain  |
| Brian      | Biggs     |
+------------+-----------+
10 rows in set (0.00 sec)

2. Create a list of students with all the columns but only if the student has less than 8 years experience

mysql> select * from student
    ->    where years_of_experience < 8;
+------------+------------+-----------+---------------------+------------+
| student_id | first_name | last_name | years_of_experience | start_date |
+------------+------------+-----------+---------------------+------------+
|          1 | Eric       | Ephram    |                   2 | 2016-03-31 |
|          2 | Greg       | Gould     |                   6 | 2016-09-30 |
|          3 | Adam       | Ant       |                   5 | 2016-06-02 |
|          4 | Howard     | Hess      |                   1 | 2016-02-28 |
|          5 | Charles    | Caldwell  |                   7 | 2016-05-07 |
|          8 | Kevin      | Kraft     |                   3 | 2016-04-15 |
|         10 | Brian      | Biggs     |                   4 | 2015-12-25 |
+------------+------------+-----------+---------------------+------------+
7 rows in set (0.00 sec)

3. Create a list of students showing the lastname, startdate, and id columns only and sorted by last_name in ascending sequence

mysql> select last_name, start_date, student_id from student order by last_name asc;
+-----------+------------+------------+
| last_name | start_date | student_id |
+-----------+------------+------------+
| Ant       | 2016-06-02 |          3 |
| Biggs     | 2015-12-25 |         10 |
| Caldwell  | 2016-05-07 |          5 |
| Dumas     | 2016-07-04 |          7 |
| Ephram    | 2016-03-31 |          1 |
| Fountain  | 2016-01-31 |          9 |
| Gould     | 2016-09-30 |          2 |
| Hess      | 2016-02-28 |          4 |
| Joyce     | 2016-08-27 |          6 |
| Kraft     | 2016-04-15 |          8 |
+-----------+------------+------------+
10 rows in set (0.00 sec)

4. Create a list of students showing all columns but only if the student first name is Adam, James, or Frank and sort them in last_name descending sequence.

mysql> select * from student
    ->    where first_name in ('Adam', 'James', 'Frank')
    ->    order by last_name desc;
+------------+------------+-----------+---------------------+------------+
| student_id | first_name | last_name | years_of_experience | start_date |
+------------+------------+-----------+---------------------+------------+
|          6 | James      | Joyce     |                   9 | 2016-08-27 |
|          9 | Frank      | Fountain  |                   8 | 2016-01-31 |
|          3 | Adam       | Ant       |                   5 | 2016-06-02 |
+------------+------------+-----------+---------------------+------------+
3 rows in set (0.00 sec)

5. Create a list of students showing firstname, lastname and startdate where the startdate is between Jan 1, 2016 and June 30, 2016 and order the list by descending start_date sequence.

mysql> select first_name, last_name, start_date from student
    ->    where start_date between '2016-01-01' and '2016-06-30'
    ->    order by start_date desc;
+------------+-----------+------------+
| first_name | last_name | start_date |
+------------+-----------+------------+
| Adam       | Ant       | 2016-06-02 |
| Charles    | Caldwell  | 2016-05-07 |
| Kevin      | Kraft     | 2016-04-15 |
| Eric       | Ephram    | 2016-03-31 |
| Howard     | Hess      | 2016-02-28 |
| Frank      | Fountain  | 2016-01-31 |
+------------+-----------+------------+
6 rows in set (0.00 sec)


________________________________________________________________________________
Medium Challenge: Changing the GRADE field in Assignment



        CREATE TABLE `assignment` (
          `assignment_id` int(11) unsigned NOT NULL AUTO_INCREMENT,
          `student_id` int(11) NOT NULL,
          `assignment_nbr` int(11) NOT NULL,
          `class_id` int(11) DEFAULT NULL,
          `grade_id` int(11), DEFAULT NULL,             <== changed this with ALTER below
          PRIMARY KEY (`assignment_id`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8;


        CREATE TABLE `grade` (
          `grade_id` int(11) unsigned NOT NULL AUTO_INCREMENT,
          `grade` varchar(30) DEFAULT NULL,
          PRIMARY KEY (`grade_id`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8;

        mysql> alter table assignment drop column grade;
        Query OK, 0 rows affected (0.02 sec)
        Records: 0  Duplicates: 0  Warnings: 0

        mysql> alter table assignment add column grade_id int unsigned not null
        Query OK, 0 rows affected (0.02 sec)
        Records: 0  Duplicates: 0  Warnings: 0

        grade_id  grade
            1     Incomplete
            2     Complete and unsatisfactory
            3     Complete and satisfactory
            4     Exceeds expectations
            5     Not graded


===> Index & Create the Foreign Key In assignment

        NOTE: BOTH assignment AND grade CONTAINED NO DATA PRIOR TO THESE OPERATIONS

        mysql> CREATE INDEX idx_grade_id ON assignment (grade_id);
        Query OK, 0 rows affected (0.02 sec)
        Records: 0  Duplicates: 0  Warnings: 0

        mysql> ALTER TABLE assignment ADD CONSTRAINT idx_grade_id FOREIGN KEY (grade_id) REFERENCES grade(grade_id);
        Query OK, 0 rows affected (0.02 sec)
        Records: 0  Duplicates: 0  Warnings: 0

===> Build assignment Values:

        mysql> describe assignment;
        +----------------+------------------+------+-----+---------+----------------+
        | Field          | Type             | Null | Key | Default | Extra          |
        +----------------+------------------+------+-----+---------+----------------+
        | assignment_id  | int(11) unsigned | NO   | PRI | NULL    | auto_increment |
        | student_id     | int(11)          | NO   |     | NULL    |                |
        | assignment_nbr | int(11)          | NO   |     | NULL    |                |
        | class_id       | int(11)          | YES  |     | NULL    |                |
        | grade_id       | int(11) unsigned | NO   | MUL | NULL    |                |
        +----------------+------------------+------+-----+---------+----------------+
        5 rows in set (0.00 sec)

        NOTE: AUTO-INCREMENT CREATED VALUES 1-5 IN THE grades table

        insert into assignment (student_id, assignment_nbr, class_id, grade_id) values
        (1, 1, 1, 1),
        (2, 2, 2, 2),
        (3, 3, 3, 3),
        (4, 4, 4, 4),
        (5, 5, 5, 5);

        mysql>         insert into assignment (student_id, assignment_nbr, class_id, grade_id) values
            ->         (1, 1, 1, 1),
            ->         (2, 2, 2, 2),
            ->         (3, 3, 3, 3),
            ->         (4, 4, 4, 4),
            ->         (5, 5, 5, 5);
        Query OK, 5 rows affected (0.00 sec)
        Records: 5  Duplicates: 0  Warnings: 0

===> Built corresponding Grade Values:

        mysql> describe grade;
        +----------+------------------+------+-----+---------+----------------+
        | Field    | Type             | Null | Key | Default | Extra          |
        +----------+------------------+------+-----+---------+----------------+
        | grade_id | int(11) unsigned | NO   | PRI | NULL    | auto_increment |
        | grade    | varchar(30)      | YES  |     | NULL    |                |
        +----------+------------------+------+-----+---------+----------------+
        2 rows in set (0.00 sec)

        insert into grade (grade) values
         ('Incomplete'),
         ('Complete and unsatisfactory'),
         ('Complete and satisfactory'),
         ('Exceeds expectations'),
         ('Not graded');

        mysql>         insert into grade (grade) values
            ->          ('Incomplete'),
            ->          ('Complete and unsatisfactory'),
            ->          ('Complete and satisfactory'),
            ->          ('Exceeds expectations'),
            ->          ('Not graded');
        Query OK, 5 rows affected (0.00 sec)
        Records: 5  Duplicates: 0  Warnings: 0


        mysql> Explain assignment;
        +----------------+------------------+------+-----+---------+----------------+
        | Field          | Type             | Null | Key | Default | Extra          |
        +----------------+------------------+------+-----+---------+----------------+
        | assignment_id  | int(11) unsigned | NO   | PRI | NULL    | auto_increment |
        | student_id     | int(11)          | NO   |     | NULL    |                |
        | assignment_nbr | int(11)          | NO   |     | NULL    |                |
        | class_id       | int(11)          | YES  |     | NULL    |                |
        | grade_id       | int(11) unsigned | NO   | MUL | NULL    |                |
        +----------------+------------------+------+-----+---------+----------------+
        5 rows in set (0.00 sec)

        mysql> select * from assignment;
        +---------------+------------+----------------+----------+----------+
        | assignment_id | student_id | assignment_nbr | class_id | grade_id |
        +---------------+------------+----------------+----------+----------+
        |             6 |          1 |              1 |        1 |        1 |
        |             7 |          2 |              2 |        2 |        2 |
        |             8 |          3 |              3 |        3 |        3 |
        |             9 |          4 |              4 |        4 |        4 |
        |            10 |          5 |              5 |        5 |        5 |
        +---------------+------------+----------------+----------+----------+
        5 rows in set (0.00 sec)

        mysql> explain grade;
        +----------+------------------+------+-----+---------+----------------+
        | Field    | Type             | Null | Key | Default | Extra          |
        +----------+------------------+------+-----+---------+----------------+
        | grade_id | int(11) unsigned | NO   | PRI | NULL    | auto_increment |
        | grade    | varchar(30)      | YES  |     | NULL    |                |
        +----------+------------------+------+-----+---------+----------------+
        2 rows in set (0.00 sec)

        mysql> select * from grade;
        +----------+-----------------------------+
        | grade_id | grade                       |
        +----------+-----------------------------+
        |        1 | Incomplete                  |
        |        2 | Complete and unsatisfactory |
        |        3 | Complete and satisfactory   |
        |        4 | Exceeds expectations        |
        |        5 | Not graded                  |
        +----------+-----------------------------+
        5 rows in set (0.00 sec)


________________________________________________________________________________
Hard Challenge:

Add the constraint to the assignment table that prohibits creating an assignment without an associated student row;

    Since the data between these fields is consistent but the definition is NOT the same, ensuring student_id in both assignment and student have the same field definition(s) - in this case "unsigned" and "int" - allows us to index the student_id in assignment followed by adding a foreign key to assignment referencing the student student_id.

Commands:

    CREATE INDEX idx_student_id ON assignment (student_id);
    ALTER TABLE assignment ADD CONSTRAINT idx_student_id FOREIGN KEY (student_id) REFERENCES student(student_id);

        mysql> CREATE INDEX idx_student_id ON assignment (student_id);
        Query OK, 0 rows affected (0.03 sec)
        Records: 0  Duplicates: 0  Warnings: 0

        mysql> ALTER TABLE assignment ADD CONSTRAINT idx_student_id FOREIGN KEY (student_id) REFERENCES student(student_id);
        Query OK, 5 rows affected (0.02 sec)
        Records: 5  Duplicates: 0  Warnings: 0

        ===> These are the final table info states at the end of this assignment

        assignment:

            CREATE TABLE `assignment` (
              `assignment_id` int(11) unsigned NOT NULL AUTO_INCREMENT,
              `student_id` int(11) unsigned NOT NULL,
              `assignment_nbr` int(11) NOT NULL,
              `class_id` int(11) DEFAULT NULL,
              `grade_id` int(11) unsigned NOT NULL,
              PRIMARY KEY (`assignment_id`),
              KEY `idx_grade_id` (`grade_id`),
              KEY `idx_student_id` (`student_id`),
              CONSTRAINT `idx_grade_id` FOREIGN KEY (`grade_id`) REFERENCES `grade` (`grade_id`),
              CONSTRAINT `idx_student_id` FOREIGN KEY (`student_id`) REFERENCES `student` (`student_id`)
            ) ENGINE=InnoDB AUTO_INCREMENT=11 DEFAULT CHARSET=utf8;

        grade:

            CREATE TABLE `grade` (
              `grade_id` int(11) unsigned NOT NULL AUTO_INCREMENT,
              `grade` varchar(30) DEFAULT NULL,
              PRIMARY KEY (`grade_id`)
            ) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8;

        student:

            CREATE TABLE `student` (
              `student_id` int(11) unsigned NOT NULL AUTO_INCREMENT,
              `first_name` varchar(30) DEFAULT NULL,
              `last_name` varchar(30) DEFAULT NULL,
              `years_of_experience` tinyint(3) DEFAULT NULL,
              `start_date` date DEFAULT NULL,
              PRIMARY KEY (`student_id`)
            ) ENGINE=InnoDB AUTO_INCREMENT=11 DEFAULT CHARSET=utf8;


HERE ENDTH THE LESSON
