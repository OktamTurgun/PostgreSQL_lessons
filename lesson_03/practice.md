# 📐 Amaliy mashqlar — Lesson 03

## 🎯 Maqsad:
PostgreSQL’da jadval yaratish, maʼlumot qoʻshish, o‘qish, yangilash va o‘chirish bo‘yicha amaliy ko‘nikma hosil qilish.

---

## 🔷 Vazifalar:
1️⃣ PostgreSQL’da yangi maʼlumotlar bazasi yarating.  
2️⃣ Quyidagi ustunlarga ega bo‘lgan `users` jadvalini yarating:
   - `id` (integer, primary key)
   - `ism` (text)
   - `yosh` (integer)
   
   *Eslatma: Primary Key — har bir qator uchun unikal va takrorlanmas qiymat bo‘lishi kerak.*

3️⃣ `users` jadvaliga 3 ta yozuv qoʻshing.  
4️⃣ Yozuvlarni o‘qib chiqing (`SELECT`).  
5️⃣ Faqat yosh qiymati 25 dan katta bo‘lgan foydalanuvchilarni tanlang.  
6️⃣ Biror foydalanuvchining yoshini yangilang.  
7️⃣ Biror foydalanuvchini o‘chirib tashlang.

---

## 💻 Buyruqlar:
```sql
-- 1. Maʼlumotlar bazasini yarating
CREATE DATABASE my_database;

-- 2. Maʼlumotlar bazasiga ulaning
\c my_database

-- 3. Jadval yaratish
CREATE TABLE users (
    id SERIAL PRIMARY KEY, -- Primary Key: unikal identifikator
    ism TEXT,
    yosh INTEGER
);

-- 4. Maʼlumot qoʻshish
INSERT INTO users (ism, yosh) VALUES
('Ali', 25),
('Vali', 30),
('Gulbahor', 28);

-- 5. Barcha maʼlumotlarni ko‘rish
SELECT * FROM users;

-- 6. Faqat yosh > 25 bo‘lganlarni ko‘rish
SELECT * FROM users WHERE yosh > 25;

-- 7. Maʼlumotni yangilash (Ali'ning yoshini 26 ga o‘zgartirish)
UPDATE users SET yosh = 26 WHERE ism = 'Ali';

-- 8. Maʼlumotni o‘chirish (Vali'ni o‘chirish)
DELETE FROM users WHERE ism = 'Vali';
```

---

## 📝 Natija namunasi:

| id | ism      | yosh |
|----|----------|------|
| 1  | Ali      | 25   |
| 2  | Vali     | 30   |
| 3  | Gulbahor | 28   |

*SELECT so‘rovlaridan so‘ng natija shunga o‘xshash bo‘ladi.*
