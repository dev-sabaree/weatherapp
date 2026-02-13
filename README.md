exp1

/* ===============================
   SECTION A – TABLE CREATION
================================ */

CREATE TABLE Book (
    book_id INT PRIMARY KEY,
    title VARCHAR(100),
    author VARCHAR(100),
    publisher VARCHAR(100),
    published_date DATE,
    price DECIMAL(10,2)
);

CREATE TABLE Member (
    member_id INT PRIMARY KEY,
    member_name VARCHAR(100),
    date_of_birth DATE,
    email VARCHAR(100),
    phone_no VARCHAR(15),
    address VARCHAR(150)
);

CREATE TABLE Issue (
    issue_id INT PRIMARY KEY,
    issue_date DATE,
    return_date DATE,
    book_id INT,
    member_id INT,
    FOREIGN KEY (book_id) REFERENCES Book(book_id),
    FOREIGN KEY (member_id) REFERENCES Member(member_id)
);

/* ===============================
   DATA INSERTION
================================ */

INSERT INTO Book VALUES
(1,'Database Systems','Navathe','Pearson','2019-05-10',950),
(2,'Operating Systems','Silberschatz','McGrawHill','2017-03-15',1100),
(3,'Computer Networks','Tanenbaum','Pearson','2020-07-21',1200),
(4,'Python Programming','Lutz','OReilly','2021-01-10',800),
(5,'Data Structures','Weiss','Pearson','2016-11-05',700),
(6,'Web Development','Duckett','Wiley','2019-09-12',900),
(7,'Artificial Intelligence','Russell','McGrawHill','2022-02-18',1300),
(8,'Machine Learning','Murphy','Pearson','2023-06-25',1500);

INSERT INTO Member VALUES
(1,'Sabareesh','2005-04-12','sabareesh@gmail.com','9876543210','Kochi'),
(2,'Arya','2005-09-23','arya@gmail.com','9876501234','Kochi'),
(3,'Hiba','2004-01-10','hiba@gmail.com','9123456780','Calicut'),
(4,'Vishnu','2003-07-18','vishnu@gmail.com','9988776655','Trivandrum'),
(5,'Arun','2004-12-02','arun@gmail.com','9090909090','Calicut');

INSERT INTO Issue VALUES
(1,'2023-02-10','2023-02-20',1,1),
(2,'2024-05-05',NULL,3,2),
(3,'2025-01-15','2025-01-25',4,3),
(4,'2023-08-12',NULL,2,4),
(5,'2024-11-20','2024-11-30',5,5),
(6,'2025-02-01',NULL,6,1);

/* ===============================
   ADD AGE COLUMN
================================ */

ALTER TABLE Member ADD age INT;

UPDATE Member
SET age = TIMESTAMPDIFF(YEAR, date_of_birth, CURDATE());

/* ===============================
   SECTION B – DATE FUNCTIONS
================================ */

SELECT MONTHNAME(issue_date) AS month_name FROM Issue;

SELECT YEAR(issue_date) AS year, COUNT(*) AS issue_count
FROM Issue
GROUP BY YEAR(issue_date);

SELECT * FROM Book
WHERE YEAR(published_date) > 2018;

SELECT * FROM Issue
WHERE issue_date >= CURDATE() - INTERVAL 90 DAY;

SELECT issue_id,
       DATEDIFF(return_date, issue_date) AS days_issued
FROM Issue
WHERE return_date IS NOT NULL;

SELECT COUNT(*) AS currently_issued
FROM Issue
WHERE return_date IS NULL;

SELECT MAX(DATEDIFF(return_date, issue_date)) AS max_duration
FROM Issue
WHERE return_date IS NOT NULL;

SELECT AVG(DATEDIFF(return_date, issue_date)) AS avg_duration
FROM Issue
WHERE return_date IS NOT NULL;

/* ===============================
   SECTION C – STRING FUNCTIONS
================================ */

SELECT UPPER(title) AS upper_title,
       LOWER(title) AS lower_title,
       member_name
FROM Book, Member;

SELECT LEFT(title,5) AS first_5_chars FROM Book;

SELECT title, LENGTH(title) AS title_length FROM Book;

SELECT member_name,
       SUBSTRING_INDEX(email,'@',-1) AS domain
FROM Member;

SELECT REPLACE(title,' ','_') AS modified_title
FROM Book;

/* ===============================
   SECTION D – NUMERIC FUNCTIONS
================================ */

SELECT title, price, price*1.10 AS increased_price
FROM Book;

SELECT MAX(price) AS max_price,
       MIN(price) AS min_price,
       AVG(price) AS avg_price
FROM Book;

SELECT publisher,
       COUNT(*) AS total_books,
       SUM(price) AS total_price
FROM Book
GROUP BY publisher;

SELECT *
FROM Book
WHERE price > (SELECT AVG(price) FROM Book);

SELECT *
FROM Book
ORDER BY YEAR(published_date) DESC;

SELECT *
FROM Book
WHERE price BETWEEN 800 AND 1200;

SELECT COUNT(*) AS returned_books
FROM Issue
WHERE return_date IS NOT NULL;


exp2

/* TABLE CREATION */

CREATE TABLE Book (
    book_id INT PRIMARY KEY,
    title VARCHAR(100),
    author VARCHAR(100),
    publisher VARCHAR(100),
    published_date DATE,
    price DECIMAL(10,2)
);

CREATE TABLE Member (
    member_id INT PRIMARY KEY,
    member_name VARCHAR(100),
    date_of_birth DATE,
    email VARCHAR(100),
    phone_no VARCHAR(15),
    address VARCHAR(150)
);

CREATE TABLE Issue (
    issue_id INT PRIMARY KEY,
    issue_date DATE,
    return_date DATE,
    book_id INT,
    member_id INT,
    FOREIGN KEY (book_id) REFERENCES Book(book_id),
    FOREIGN KEY (member_id) REFERENCES Member(member_id)
);

/* DATA INSERTION */

INSERT INTO Book VALUES
(1,'Database Systems','Navathe','Pearson','2019-05-10',950),
(2,'Operating Systems','Silberschatz','McGrawHill','2017-03-15',1100),
(3,'Computer Networks','Tanenbaum','Pearson','Pearson','2020-07-21',1200),
(4,'Python Programming','Lutz','OReilly','2021-01-10',800),
(5,'Data Structures','Weiss','Pearson','2016-11-05',700),
(6,'Web Development','Duckett','Wiley','2019-09-12',900),
(7,'Artificial Intelligence','Russell','McGrawHill','2022-02-18',1300),
(8,'Machine Learning','Murphy','Pearson','2023-06-25',1500);

INSERT INTO Member VALUES
(1,'Sabareesh','2005-04-12','sabareesh@gmail.com','9876543210','Kochi'),
(2,'Arya','2005-09-23','arya@gmail.com','9876501234','Kochi'),
(3,'Hiba','2004-01-10','hiba@gmail.com','9123456780','Calicut'),
(4,'Vishnu','2003-07-18','vishnu@gmail.com','9988776655','Trivandrum'),
(5,'Arun','2004-12-02','arun@gmail.com','9090909090','Calicut');

INSERT INTO Issue VALUES
(1,'2023-02-10','2023-02-20',1,1),
(2,'2024-05-05',NULL,3,2),
(3,'2025-01-15','2025-01-25',4,3),
(4,'2023-08-12',NULL,2,4),
(5,'2024-11-20','2024-11-30',5,5),
(6,'2025-02-01',NULL,6,1);

/* ADD AGE COLUMN */

ALTER TABLE Member ADD age INT;

UPDATE Member
SET age = TIMESTAMPDIFF(YEAR, date_of_birth, CURDATE());

/* DATE FUNCTIONS */

SELECT MONTHNAME(issue_date) FROM Issue;

SELECT YEAR(issue_date), COUNT(*)
FROM Issue
GROUP BY YEAR(issue_date);

SELECT * FROM Book
WHERE YEAR(published_date) > 2018;

SELECT * FROM Issue
WHERE issue_date >= CURDATE() - INTERVAL 90 DAY;

SELECT issue_id,
DATEDIFF(return_date, issue_date)
FROM Issue
WHERE return_date IS NOT NULL;

SELECT COUNT(*) FROM Issue
WHERE return_date IS NULL;

SELECT MAX(DATEDIFF(return_date, issue_date))
FROM Issue
WHERE return_date IS NOT NULL;

SELECT AVG(DATEDIFF(return_date, issue_date))
FROM Issue
WHERE return_date IS NOT NULL;

/* STRING FUNCTIONS */

SELECT UPPER(title), LOWER(title), member_name
FROM Book, Member;

SELECT LEFT(title,5) FROM Book;

SELECT title, LENGTH(title) FROM Book;

SELECT member_name,
SUBSTRING_INDEX(email,'@',-1)
FROM Member;

SELECT REPLACE(title,' ','_') FROM Book;

/* NUMERIC FUNCTIONS */

SELECT title, price, price*1.10 FROM Book;

SELECT MAX(price), MIN(price), AVG(price)
FROM Book;

SELECT publisher, COUNT(*), SUM(price)
FROM Book
GROUP BY publisher;

SELECT *
FROM Book
WHERE price > (SELECT AVG(price) FROM Book);

SELECT *
FROM Book
ORDER BY YEAR(published_date) DESC;

SELECT *
FROM Book
WHERE price BETWEEN 800 AND 1200;

SELECT COUNT(*)
FROM Issue
WHERE return_date IS NOT NULL;

/* ORDER BY */

SELECT * FROM Book
ORDER BY title, price;

SELECT * FROM Member
ORDER BY member_name DESC;

/* GROUP BY */

SELECT publisher, SUM(price)
FROM Book
GROUP BY publisher;

SELECT YEAR(issue_date), COUNT(*)
FROM Issue
GROUP BY YEAR(issue_date);

/* HAVING */

SELECT publisher, COUNT(*)
FROM Book
GROUP BY publisher
HAVING COUNT(*) >= 2;

SELECT YEAR(issue_date), COUNT(*)
FROM Issue
GROUP BY YEAR(issue_date)
HAVING COUNT(*) > 1;