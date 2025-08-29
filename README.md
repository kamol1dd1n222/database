-- Databazani ko'rish
SHOW DATABASES;

-- Databaza yaratish
CREATE DATABASE mydatabase;
SHOW DATABASES;
-- Qayerda turganini ko'rish
SELECT DATABASE()

-- Databazdan foydalanish yani ichiga kirib malumotlar yozish
USE mydatabase;

-- Databazani o'chirish.
DROP DATABASE mydatabase;
SHOW DATABASES;

-- "\! cls" ekranni tozalash

-- Jadvallarni ko'rish
SHOW TABLES;

-- Jadval yaratish 1- usuli
CREATE TABLE student(
    first_name VARCHAR(50)
    second_name VARCHAR(50)
    age integer
    gender VARCHAR(10)
);
SHOW TABLES;

-- Jadvallarni qayta nomlash
RENAME TABLE Talaba TO student;
SHOW TABLES;

-- Jadvalni o'chirish
DROP TABLE student;
SHOW TABLES;


-- Jadval yaratish 2-usuli 
CREATE TABLE IF NOT EXISTS Talaba(
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    second_name VARCHAR(50) NOT NULL,
    age INT NOT NULL,
    gender TEXT,
    phone_number VARCHAR(14)
);

-- Jadvaldagi fieldlarni tiplarini ko'rish
DESCRIBE talaba;
DESC talaba;
SHOW COLUMNS FROM a.talaba;
SHOW COLUMNS FROM talaba IN a;

-- Jadvalni to'liq ko'rish
SELECT * FROM talaba;

-- Jadvalni to'ldirish birinchi usuli 1 qatorli to'ldirish
INSERT INTO talaba(first_name,second_name,age,gender,phone_number) VALUES
    ('Kamoliddin','Baxtiyorov',19,'Male','+998945121565');

INSERT INTO talaba VALUES(2,'Abbos','Xolbekov',23,'Male','+998956542738');



INSERT INTO talaba VALUES(3,'Bekmurod','Bozorov',31,'Male','+998901657841');
-- Jadval malumotlarini o'chirish
DELETE FROM talaba WHERE id = 4;

-- Jadvalga ko'p qatorli malumot qo'shish,2-usul
INSERT INTO talaba (first_name, second_name, age, gender, phone_number) VALUES
('Dilnoza', 'Karimova', 20, 'FEMALE', '+998901234502'),
('Javohir', 'Qodirov', 21, 'MALE', '+998901234503'),
('Madina', 'Rasulova', 22, 'FEMALE', '+998901234504'),
('Sherzod', 'Olimov', 20, 'MALE', '+998901234505'),
('Nilufar', 'Abdurahmonova', 21, 'FEMALE', '+998901234506'),
('Sardor', 'Valiyev', 19, 'MALE', '+998901234507'),
('Sitora', 'Solieva', 20, 'FEMALE', '+998901234508'),
('Bekzod', 'Tursunov', 23, 'MALE', '+998901234509'),
('Gulnoza', 'Matmurodova', 18, 'FEMALE', '+998901234510'),
('Diyor', 'Hamidov', 22, 'MALE', '+998901234511'),
('Malika', 'Yusupova', 19, 'FEMALE', '+998901234512'),
('Botir', 'Eshonov', 21, 'MALE', '+998901234513'),
('Rayhona', 'Mahkamova', 20, 'FEMALE', '+998901234514'),
('Anvar', 'Qo‘chqorov', 23, 'MALE', '+998901234515'),
('Dilafruz', 'Sobirova', 19, 'FEMALE', '+998901234516'),
('Shavkat', 'Asadov', 22, 'MALE', '+998901234517'),
('Zilola', 'Tojiboyeva', 18, 'FEMALE', '+998901234518'),
('Rustam', 'Saidov', 21, 'MALE', '+998901234519'),
('Munisa', 'Ortiqova', 20, 'FEMALE', '+998901234520'),
('Doston', 'Shokirov', 23, 'MALE', '+998901234521'),
('Mohira', 'Nabieva', 19, 'FEMALE', '+998901234522'),
('Oybek', 'Islomov', 22, 'MALE', '+998901234523'),
('Zarnigor', 'Xolmatova', 20, 'FEMALE', '+998901234524'),
('Elyor', 'Boboyev', 21, 'MALE', '+998901234525');

-- Faqat kerakli malumotlarni chiqarish jadval ichidan
SELECT id,first_name FROM  talaba;

-- USTUN nomini o'zgartirish(AS) va chiqarish
SELECT first_name AS ism, second_name AS familiya From talaba;


-- WHERE- qayerda || IF ga o'xshaydi shart tekshiradi.(>=,<=,<,>,!=,=) yoki (IS,OR,AND)

SELECT *From talaba WHERE gender = 'MALE';
SELECT *From talaba WHERE first_name != 'Malika';
SELECT *From talaba WHERE age >= 21;
SELECT *From talaba WHERE phone_number = NULL;
SELECT *From talaba WHERE phone_number IS  NULL;

-- OR AND

SELECT * FROM talaba WHERE age >= 21 AND gender = 'MALE';
SELECT * FROM talaba WHERE age >= 21 OR gender = 'MALE';

-- BETWEEN  - orasida
SELECT * FROM talaba WHERE age BETWEEN 15 AND 21;
SELECT * FROM talaba WHERE id BETWEEN 15 AND 21;

-- ORDER BY  - sortlash.(ASC - o'sish tartibida, DESC - kamayish tartibida)
SELECT * FROM talaba ORDER BY age;
SELECT * From talaba WHERE gender = 'MALE' ORDER BY age ASC;
SELECT * From talaba WHERE gender = 'MALE' ORDER BY age DESC;


-- LIMIT - CHEGARA  || offset, count
SELECT * FROM talaba LIMIT 5;
SELECT * FROM talaba LIMIT 5,11;
SELECT * FROM talaba ORDER BY first_name LIMIT 5; -- ham sortlayabdi va 5 tasini chiqarib beryapti


-- LIKE  - o'xshash
SELECT * FROM talaba WHERE first_name LIKE 'Bekmurod';SELECT * FROM talaba WHERE first_name LIKE 'Bekmurod'; -- agar shunga teng bo'lsa chiqaradi
SELECT * FROM talaba WHERE first_name LIKE 'Bek%'; -- Ismining boshi Bek bilan boshlanganlarin i chiqaradi
SELECT * FROM talaba WHERE first_name LIKE '%Bek%'; -- Ismning ichida Bek bo'lganlarini chiqaradi
SELECT * FROM talaba WHERE first_name LIKE '%Bek';  -- Ismining oxiri bek bn tugaganlarini chiqaradi
SELECT * FROM talaba WHERE first_name LIKE 'a%';
SELECT * FROM talaba WHERE first_name LIKE '____r'; -- nechta paschiziq bo'lsa shuncha harf boshida bo'lishi kerak va oxiri r harfi bilan tugashi kerak
SELECT * FROM talaba WHERE first_name LIKE 'K________n'; -- boshi k bn boshlanib oxiri n bilan tugasi kerak va pastchiziqlar nechta bo'lsa shuncha harf bo'lishi kerak orasida
SELECT * FROM talaba WHERE first_name LIKE '__m%'; -- 3-yoki 2- harfi m bo'lishi kerak
SELECT * FROM talaba WHERE phone_number LIKE '+99894%'; -- raqamining boshi 94 lik bo'lgan barcha raqamlarni tekshiradi

-- IN - ichida || ichida bo'lsa ko'rsatadi
SELECT * From talaba WHERE first_name IN ('Kamoliddin','Abbos','Malika','Islom'); -- Ichida shu ismlar bo'lsa chiqaradi

-- FUNCTION SUM, AVG, MIN, MAX, COUNT
SELECT SUM(age) From talaba; -- talaba yoshlarini yig'indisini chiqaradi
SELECT SUM(age) From talaba WHERE age >= 21; -- talaba yoshlarini yig'indisini chiqaradi yoshi 21 dan kattalarini
SELECT AVG(age) AS ortacha_yosh From talaba; -- yoshlaring o'rtachasini chiqaradi(yani o'rtacha qiymatini) 
SELECT MIN(age) FRom talaba;
SELECT MAX(age) FRom talaba;
SELECT MAX(first_name) FRom talaba;
SELECT COUNT(*) FROM talaba WHERE age = 21;
SELECT COUNT(DISTINCT age) FROM talaba; -- DISTINCT takrorlanmaydigan qiymatlarni sanaydi

-- UPDATE - yangilash
UPDATE talaba SET age = 0 WHERE age >= 21;


-- DELETE - o'chirish
DELETE From talaba WHERE age = 0;

DELETE FROM talaba id;
TRUNCATE TABLE talaba;

-- Yangi ustun qo'shish
ALTER TABLE talaba ADD viloyat VARCHAR(40);

-- Qo'shilgan yoki bor ustunlarni o'chirish 
ALTER TABLE talaba DROP COLUMN viloyat;

-- Uzunligini aniqlayfigan funksiya: LENGTH
SELECT LENGTH(ism) FROM talaba; -- talabalarining ismining uzunligini chiqaradi

-- Vaqt funksiyalari
CREATE TABLE sn3 (
    id INT PRIMARY KEY AUTO_INCREMENT,
    ism VARCHAR(50),
    yil TIMESTAMP);

INSERT INTO sn3 (ism, yil) VALUES
('Sardor', '2000-05-14 00:00:00'),
('Jasur', '2003-09-22 00:00:00'),
('Javlon', '1999-12-01 00:00:00'),
('Javlon', '2004-03-30 00:00:00'),
('Dilmurod', '2002-07-17 00:00:00');

SELECT *,YEAR(yil) as yilning_ozi From sn3;

-- Ustunlarni birlashtirsh yoki malumot qo'shish uchun: CONCAT
SELECT id,CONCAT(ism,' ',familiya) as toliq FROM talaba;
SELECT *, CONCAT(ism,' ',familiya) as toliq FROM talaba;
