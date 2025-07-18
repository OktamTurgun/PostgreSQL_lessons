# 📐 Amaliy mashqlar — Lesson 10

## 🎯 Maqsad:
WHERE va filtratsiya operatorlari yordamida maʼlumotlarni aniq tanlashni amalda oʼrganish.

---

## 🔷 Vazifalar:
1⃣ students jadvalini yarating va maʼlumotlar kiriting  
2⃣ WHERE bilan turli shartlarda soʼrovlar yozing  
3⃣ LIKE, BETWEEN, IN, IS NULL, AND, OR operatorlarini amalda sinab koʼring

---

## 💻 Buyruqlar:

### 1. Jadval yaratish va maʼlumot kiritish:
```sql
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    age INTEGER,
    grade VARCHAR(2),
    email VARCHAR(100)
);

INSERT INTO students (name, age, grade, email) VALUES
('Ali Valiyev', 21, 'A', 'ali@example.com'),
('Gulbahor Karimova', 19, 'B', NULL),
('Aziz Toshmatov', 22, 'A', 'aziz@example.com'),
('Malika Yusupova', 18, 'C', 'malika@example.com'),
('Jasur Turgunov', 20, 'B', NULL);
```

### Solishtirish operatorlari bilan misollar:

### 2. WHERE bilan turli shartlarda soʼrovlar:
```sql
-- 21 yoshdan katta talabalar
SELECT * FROM students WHERE age > 21;

-- Faqat 'A' baholi talabalar
SELECT name FROM students WHERE grade = 'A';

-- 18-20 yosh oraligʼidagi talabalar
SELECT * FROM students WHERE age BETWEEN 18 AND 20;

-- Emaili yoʼq (NULL) talabalar
SELECT name FROM students WHERE email IS NULL;

-- Ismi 'A' harfi bilan boshlanadigan talabalar
SELECT * FROM students WHERE name LIKE 'A%';

-- 'B' yoki 'C' baholi talabalar
SELECT * FROM students WHERE grade IN ('B', 'C');

-- 'A' baholi va 20 yoshdan katta talabalar
SELECT * FROM students WHERE grade = 'A' AND age > 20;

-- 'B' baholi yoki emaili yoʼq talabalar
SELECT * FROM students WHERE grade = 'B' OR email IS NULL;
```

---

## 📋 Kutilgan natija:

| id | name               | age | grade | email              |
|----|--------------------|-----|-------|--------------------|
| 1  | Ali Valiyev        | 21  | A     | ali@example.com    |
| 2  | Gulbahor Karimova  | 19  | B     | NULL               |
| 3  | Aziz Toshmatov     | 22  | A     | aziz@example.com   |
| 4  | Malika Yusupova    | 18  | C     | malika@example.com |
| 5  | Jasur Turgunov     | 20  | B     | NULL               |

---

## 🔍 Qoʼshimcha topshiriqlar:
- NOT IN operatori bilan 'A' baholi boʼlmaganlarni koʼring
- ILIKE yordamida ismi 'ali' boʼlganlarni toping
- Bir nechta shartlarni AND/OR bilan birlashtirib soʼrov yozing
- IS NOT NULL operatori bilan emaili bor talabalarni koʼring 