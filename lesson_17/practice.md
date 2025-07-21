# 🎯 Lesson 17 — Amaliy mashgʼulotlar: UPDATE operatori

## 📋 Dars mazmuni
- UPDATE operatori bilan yozuvlarni yangilash
- WHERE sharti bilan aniq yangilash
- RETURNING va tranzaksiya bilan ishlash
- Amaliy xavfsiz yangilash

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

## 🎯 Mashgʼulot 1: Oddiy yangilash

### Vazifa 1.1
**Savol:** ID si 2 bo‘lgan o‘quvchining yoshini 22 ga o‘zgartiring.

```sql
-- Yechim:
UPDATE students SET age = 22 WHERE id = 2;
```

### Vazifa 1.2
**Savol:** Familiyasi 'Nazarova' bo‘lgan o‘quvchining ballini 'B' ga o‘zgartiring.

```sql
-- Yechim:
UPDATE students SET grade = 'B' WHERE surname = 'Nazarova';
```

---

## 🎯 Mashgʼulot 2: Bir nechta ustunni yangilash

### Vazifa 2.1
**Savol:** ID si 4 bo‘lgan o‘quvchining yoshini 19 va ballini 'A' ga o‘zgartiring.

```sql
-- Yechim:
UPDATE students SET age = 19, grade = 'A' WHERE id = 4;
```

### Vazifa 2.2
**Savol:** Tashkent shahridagi barcha o‘quvchilarning ballini 'A' ga o‘zgartiring.

```sql
-- Yechim:
UPDATE students SET grade = 'A' WHERE city = 'Tashkent';
```

---

## 🎯 Mashgʼulot 3: Bir nechta yozuvlarni yangilash

### Vazifa 3.1
**Savol:** Barcha o‘quvchilarning ballini 'C' ga o‘zgartiring. (EHTIYOT BO‘LING!)

```sql
-- Yechim:
UPDATE students SET grade = 'C';
```

### Vazifa 3.2
**Savol:** 20 yoshdan katta o‘quvchilarning shahrini 'Bukhara' ga o‘zgartiring.

```sql
-- Yechim:
UPDATE students SET city = 'Bukhara' WHERE age > 20;
```

---

## 🎯 Mashgʼulot 4: RETURNING bilan ishlash

### Vazifa 4.1
**Savol:** Balli 'B' bo‘lgan o‘quvchilarning ballini 'A' ga o‘zgartirib, ism va familiyasini qaytaring.

```sql
-- Yechim:
UPDATE students SET grade = 'A' WHERE grade = 'B' RETURNING name, surname;
```

### Vazifa 4.2
**Savol:** Samarkand shahridagi o‘quvchilarning yoshini 21 ga o‘zgartirib, ism va yangi yoshini qaytaring.

```sql
-- Yechim:
UPDATE students SET age = 21 WHERE city = 'Samarkand' RETURNING name, age;
```

---

## 🎯 Mashgʼulot 5: Tranzaksiya bilan xavfsiz yangilash

### Vazifa 5.1
**Savol:** Buxorolik o‘quvchilarning ballini 'B' ga o‘zgartiring, natijani tekshirib, bekor qiling (ROLLBACK).

```sql
-- Yechim:
BEGIN;
UPDATE students SET grade = 'B' WHERE city = 'Bukhara';
-- SELECT * FROM students WHERE city = 'Bukhara';
ROLLBACK;
```

---

## 📌 Natijalarni tekshirish

- Yangilangan yozuvlar to‘g‘ri tanlanganmi?
- WHERE sharti to‘g‘ri ishlatilganmi?
- RETURNING natijasi to‘g‘ri qaytdimi?
- Tranzaksiya yordamida yangilash xavfsiz amalga oshdimi?

---

## 📌 Keyingi darsga tayyorgarlik

Keyingi darsda quyidagilarni o‘rganamiz:
- Jadvallar dizayni va indekslar
- Jadval yaratish va o‘zgartirish
- Indekslar va ularning samaradorligi
- Amaliy mashg‘ulotlar 