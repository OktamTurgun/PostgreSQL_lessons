# 📐 Amaliy mashqlar — Lesson 11

## 🎯 Maqsad:
AND, OR, NOT operatorlari yordamida murakkab shartlar bilan soʼrovlar yozishni amalda oʼrganish.

---

## 🔷 Vazifalar:
1⃣ students jadvalini yarating va maʼlumotlar kiriting  
2⃣ AND, OR, NOT operatorlari bilan turli shartlarda soʼrovlar yozing  
3⃣ Qavslar yordamida murakkab shartlar tuzing

---

## 💻 Buyruqlar:

### 1. Jadval yaratish va maʼlumot kiritish:
```sql
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    age INTEGER,
    grade VARCHAR(2)
);

INSERT INTO students (name, age, grade) VALUES
('Ali Valiyev', 21, 'A'),
('Gulbahor Karimova', 19, 'B'),
('Aziz Toshmatov', 22, 'A'),
('Malika Yusupova', 18, 'C'),
('Jasur Turgunov', 20, 'B');
```

### 2. AND, OR, NOT operatorlari bilan soʼrovlar:
```sql
-- 20 yoshdan katta va 'A' baholi talabalar
SELECT * FROM students WHERE age > 20 AND grade = 'A';

-- 'A' yoki 'B' baholi talabalar
SELECT * FROM students WHERE grade = 'A' OR grade = 'B';

-- 'C' baholi boʼlmagan talabalar
SELECT * FROM students WHERE NOT (grade = 'C');

-- 20 yoshdan katta va 'A' yoki 'B' baholi talabalar
SELECT * FROM students WHERE (grade = 'A' OR grade = 'B') AND age > 20;

-- 19 yoshdan kichik yoki 'C' baholi boʼlmagan talabalar
SELECT * FROM students WHERE NOT (age < 19 OR grade = 'C');
```

---

## 📋 Kutilgan natija:

| id | name               | age | grade |
|----|--------------------|-----|-------|
| 1  | Ali Valiyev        | 21  | A     |
| 2  | Gulbahor Karimova  | 19  | B     |
| 3  | Aziz Toshmatov     | 22  | A     |
| 4  | Malika Yusupova    | 18  | C     |
| 5  | Jasur Turgunov     | 20  | B     |

---

## 🔍 Qoʼshimcha topshiriqlar:
- 20 yoshdan katta va 'B' baholi talabalarni koʼring
- 'A' yoki 'C' baholi va 19 yoshdan kichik boʼlganlarni toping
- NOT operatori bilan 'B' baholi boʼlmaganlarni koʼring
- AND va OR ni birga ishlatib murakkab shart yozing 