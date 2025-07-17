# 📐 Amaliy mashqlar — Lesson 06

## 🎯 Maqsad:
PostgreSQLʼda foydali buyruqlarni amalda qoʼllash va ularning natijalarini koʼrishni oʼrganish.

---

## 🔷 Vazifalar:
1⃣ PostgreSQLʼga ulaning va mavjud bazalarni koʼring  
2⃣ Yangi test bazasi yarating va unga ulaning  
3⃣ `students` jadvalini yarating va maʼlumotlar qoʼshing  
4⃣ Jadval tuzilmasini va maʼlumotlarni koʼring  
5⃣ Maʼlumotlarni yangilang va oʼchiring  
6⃣ Foydali psql buyruqlarini sinab koʼring

---

## 💻 Buyruqlar:

### 1. Bazalar bilan ishlash:
```sql
-- Mavjud bazalarni koʼrish
\l

-- Yangi baza yaratish
CREATE DATABASE test_db;

-- Bazaga ulanish
\c test_db

-- Hozirgi bazani koʼrish
SELECT current_database();
```

### 2. Jadval yaratish va maʼlumot qoʼshish:
```sql
-- Students jadvalini yaratish
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    age INTEGER,
    grade VARCHAR(10),
    email VARCHAR(255)
);

-- Maʼlumotlar qoʼshish
INSERT INTO students (name, age, grade, email) VALUES
('Ali Valiyev', 20, 'A', 'ali@example.com'),
('Gulbahor Karimova', 19, 'B', 'gulbahor@example.com'),
('Aziz Toshmatov', 21, 'A', 'aziz@example.com'),
('Malika Yusupova', 18, 'C', 'malika@example.com');
```

### 3. Maʼlumotlarni koʼrish:
```sql
-- Jadvallar roʼyxatini koʼrish
\dt

-- Jadval tuzilmasini koʼrish
\d students

-- Barcha maʼlumotlarni koʼrish
SELECT * FROM students;

-- Belgilangan ustunlarni koʼrish
SELECT name, age, grade FROM students;
```

### 4. Maʼlumotlarni yangilash:
```sql
-- Bitta yozuvni yangilash
UPDATE students SET grade = 'A+' WHERE name = 'Ali Valiyev';

-- Bir nechta yozuvni yangilash
UPDATE students SET age = age + 1 WHERE grade = 'A';

-- Yangilangan maʼlumotlarni koʼrish
SELECT * FROM students;
```

### 5. Maʼlumotlarni oʼchirish:
```sql
-- Shartli oʼchirish
DELETE FROM students WHERE grade = 'C';

-- Oʼchirilgan maʼlumotlarni koʼrish
SELECT * FROM students;
```

### 6. Foydali psql buyruqlari:
```sql
-- Yordam olish
\?

-- SQL buyrugʼi haqida maʼlumot
\h SELECT

-- Vaqtni koʼrsatish
\timing

-- Kengaytirilgan koʼrinish
\x
SELECT * FROM students LIMIT 1;

-- Oddiy koʼrinishga qaytish
\x
```

---

## 📋 Kutilgan natija:

### Bazalar roʼyxati:
```
Name      | Owner | Encoding | Collate | Ctype | Access privileges
----------|-------|----------|---------|-------|------------------
postgres  | postgres | UTF8 | en_US.UTF-8 | en_US.UTF-8 |
test_db   | postgres | UTF8 | en_US.UTF-8 | en_US.UTF-8 |
```

### Students jadvali:
| id | name | age | grade | email |
|----|------|-----|-------|-------|
| 1  | Ali Valiyev | 21 | A+ | ali@example.com |
| 2  | Gulbahor Karimova | 20 | B | gulbahor@example.com |
| 3  | Aziz Toshmatov | 22 | A | aziz@example.com |

---

## 🔍 Qoʼshimcha topshiriqlar:
- `\du` buyrugʼi bilan foydalanuvchilar roʼyxatini koʼring
- `\df` buyrugʼi bilan funksiyalar roʼyxatini koʼring
- `\dv` buyrugʼi bilan koʼrinishlar roʼyxatini koʼring
- `\pset` buyrugʼi bilan natija formatini oʼzgartiring
- Yangi jadval yarating va `ALTER TABLE` buyruqlarini sinab koʼring
- `\h` buyrugʼi bilan boshqa SQL buyruqlari haqida maʼlumot oling 