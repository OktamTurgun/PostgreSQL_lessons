# 🎯 Lesson 16 — Amaliy mashgʼulotlar: DELETE operatori

## 📋 Dars mazmuni
- DELETE operatori bilan yozuvlarni o‘chirish
- WHERE sharti bilan aniq o‘chirish
- LIMIT va RETURNING bilan ishlash
- Tranzaksiya va xavfsiz o‘chirish

---

## 🗄️ Namuna maʼlumotlar bazasi

```sql
-- O‘quvchilar jadvali
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50),
    surname VARCHAR(50),
    age INTEGER,
    grade CHAR(1),
    city VARCHAR(30),
    phone VARCHAR(15),
    email VARCHAR(100)
);

INSERT INTO students (name, surname, age, grade, city, phone, email) VALUES
('Aziz', 'Karimov', 20, 'A', 'Tashkent', '+998901234567', 'aziz@email.com'),
('Malika', 'Rahimova', 19, 'B', 'Samarkand', '+998901234568', 'malika@email.com'),
('Jasur', 'Toshmatov', 22, 'A', 'Tashkent', NULL, 'jasur@email.com'),
('Dilfuza', 'Nazarova', 18, 'C', 'Bukhara', '+998901234569', NULL),
('Akmal', 'Sobirov', 21, 'B', 'Tashkent', '+998901234570', 'akmal@email.com'),
('Zarina', 'Mirzaeva', 20, 'A', 'Samarkand', NULL, 'zarina@email.com'),
('Bekzod', 'Alimov', 19, 'C', 'Tashkent', '+998901234571', 'bekzod@email.com'),
('Nilufar', 'Kadirova', 23, 'A', 'Bukhara', '+998901234572', 'nilufar@email.com'),
('Rustam', 'Yuldashev', 18, 'B', 'Tashkent', '+998901234573', 'rustam@email.com'),
('Maftuna', 'Hasanova', 20, 'A', 'Samarkand', NULL, 'maftuna@email.com');
```

---

## 🎯 Mashgʼulot 1: Oddiy o‘chirish

### Vazifa 1.1
**Savol:** ID si 3 bo‘lgan o‘quvchini o‘chiring.

```sql
-- Yechim:
DELETE FROM students WHERE id = 3;
```

### Vazifa 1.2
**Savol:** Familiyasi 'Nazarova' bo‘lgan o‘quvchini o‘chiring.

```sql
-- Yechim:
DELETE FROM students WHERE surname = 'Nazarova';
```

---

## 🎯 Mashgʼulot 2: Bir nechta yozuvlarni o‘chirish

### Vazifa 2.1
**Savol:** Tashkent shahridagi barcha o‘quvchilarni o‘chiring.

```sql
-- Yechim:
DELETE FROM students WHERE city = 'Tashkent';
```

### Vazifa 2.2
**Savol:** B balli o‘quvchilarni o‘chiring.

```sql
-- Yechim:
DELETE FROM students WHERE grade = 'B';
```

---

## 🎯 Mashgʼulot 3: LIMIT va RETURNING bilan ishlash

### Vazifa 3.1
**Savol:** Samarkand shahridan faqat 2 ta o‘quvchini o‘chiring va ularning ismini qaytaring. (PostgreSQL 13+)

```sql
-- Yechim:
DELETE FROM students WHERE city = 'Samarkand' RETURNING name LIMIT 2;
```

### Vazifa 3.2
**Savol:** C balli o‘quvchilarni o‘chiring va ularning ism va familiyasini qaytaring.

```sql
-- Yechim:
DELETE FROM students WHERE grade = 'C' RETURNING name, surname;
```

---

## 🎯 Mashgʼulot 4: Barcha yozuvlarni o‘chirish (EHTIYOT BO‘LING!)

### Vazifa 4.1
**Savol:** Jadvaldagi barcha o‘quvchilarni o‘chiring.

```sql
-- Yechim:
DELETE FROM students;
```

---

## 🎯 Mashgʼulot 5: Tranzaksiya bilan xavfsiz o‘chirish

### Vazifa 5.1
**Savol:** Buxorolik o‘quvchilarni tranzaksiya yordamida o‘chiring va natijani tekshirib, bekor qiling (ROLLBACK).

```sql
-- Yechim:
BEGIN;
DELETE FROM students WHERE city = 'Bukhara';
-- SELECT * FROM students WHERE city = 'Bukhara';
ROLLBACK;
```

---

## 📌 Natijalarni tekshirish

- O‘chirilgan yozuvlar to‘g‘ri tanlanganmi?
- WHERE sharti to‘g‘ri ishlatilganmi?
- RETURNING natijasi to‘g‘ri qaytdimi?
- Tranzaksiya yordamida o‘chirish xavfsiz amalga oshdimi?

---

## 📌 Keyingi darsga tayyorgarlik

Keyingi darsda quyidagilarni o‘rganamiz:
- UPDATE operatori bilan maʼlumotlarni yangilash
- SET va WHERE shartlari
- Tranzaksiya va xavfsiz yangilash
- Amaliy mashg‘ulotlar 