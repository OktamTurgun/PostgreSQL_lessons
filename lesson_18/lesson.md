# 📖 Lesson 18 — Jadvallarni to'g'ri dizayn qilish (mukammal)

## 🎯 Maqsad
PostgreSQL'da jadvallarni to'g'ri loyihalash, bog'lash va o'zgartirish bo'yicha barcha muhim bilimlarni bosqichma-bosqich, misollar va izohlar bilan chuqur o'rganish.

---

## 1. Jadval dizayni asoslari

### Nazariya
- **Ustun turlari:** INT, VARCHAR, DATE, BOOLEAN va boshqalar.
- **Cheklovlar:** NOT NULL, UNIQUE, DEFAULT, CHECK — ma'lumotlar sifatini nazorat qiladi.
- **Birlamchi kalit (PRIMARY KEY):** har bir yozuvni noyob aniqlovchi ustun.
- **Tashqi kalit (FOREIGN KEY):** boshqa jadvalga bog'lovchi ustun, yaxlitlikni ta'minlaydi.
- **Normalizatsiya:** 1NF, 2NF, 3NF — ma'lumotlarni takrorlanmas va tartibli saqlash.

### Misol
```sql
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    age INT CHECK (age > 0),
    email VARCHAR(100) UNIQUE,
    city VARCHAR(50) DEFAULT 'Toshkent'
);
```
**Natija:** Jadvalda har bir ustun uchun cheklovlar va kalitlar mavjud.

---

## 2. One to One (1:1) munosabat

### Nazariya
- Har bir yozuv faqat bitta bog'liq yozuvga ega.

### Misol
```sql
CREATE TABLE passports (
    id SERIAL PRIMARY KEY,
    student_id INT UNIQUE REFERENCES students(id)
);
```
**Natija:** Har bir studentga faqat bitta passport bog'lanadi.

**Izoh:** UNIQUE cheklovi 1:1 munosabatni ta'minlaydi.

---

## 3. One to Many (1:N) munosabat

### Nazariya
- Bitta yozuv ko'plab bog'liq yozuvlarga ega.

### Misol
```sql
CREATE TABLE groups (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50)
);
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50),
    group_id INT REFERENCES groups(id)
);
```
**Natija:** Bir groupda ko'plab student bo'lishi mumkin.

**Izoh:** Tashqi kalit orqali 1:N munosabat yaratiladi.

---

## 4. Many to Many (N:M) munosabat

### Nazariya
- Ko'pdan-ko'p bog'lanish, oraliq jadval orqali amalga oshiriladi.

### Misol
```sql
CREATE TABLE courses (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50)
);
CREATE TABLE student_courses (
    student_id INT REFERENCES students(id),
    course_id INT REFERENCES courses(id),
    PRIMARY KEY (student_id, course_id)
);
```
**Natija:** Har bir student bir nechta kursga yozilishi, har bir kursda bir nechta student bo'lishi mumkin.

**Izoh:** Oraliq jadval (student_courses) N:M munosabatni ta'minlaydi.

---

## 5. Alohida jadvalga olib chiqish va denormalizatsiya

### Nazariya
- Takrorlanuvchi yoki bog'liq ma'lumotlarni alohida jadvalga ajratish (denormalizatsiya).

### Misol
```sql
-- Yomon dizayn:
CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    customer_name VARCHAR(50),
    product_name VARCHAR(50),
    quantity INT
);

-- To'g'ri dizayn:
CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50)
);
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50)
);
CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    customer_id INT REFERENCES customers(id),
    product_id INT REFERENCES products(id),
    quantity INT
);
```
**Natija:** Takrorlanuvchi ma'lumotlar alohida jadvallarga ajratildi.

**Izoh:** Bu yondashuv ma'lumotlar yaxlitligi va soddaligini ta'minlaydi.

---

## 6. ALTER TABLE buyrug'i

### Nazariya
- Jadval tuzilmasini o'zgartirish uchun ishlatiladi: ustun qo'shish, o'chirish, o'zgartirish, cheklovlar qo'shish yoki olib tashlash.

### Misol
```sql
-- Ustun qo'shish
ALTER TABLE students ADD COLUMN phone VARCHAR(20);

-- Ustun nomini o'zgartirish
ALTER TABLE students RENAME COLUMN phone TO phone_number;

-- Ustunni o'chirish
ALTER TABLE students DROP COLUMN phone_number;

-- Cheklov qo'shish
ALTER TABLE students ADD CONSTRAINT age_positive CHECK (age > 0);
```
**Natija:** Jadval tuzilmasi o'zgartirildi.

**Izoh:** O'zgartirishdan oldin ma'lumotlarni zaxiralash tavsiya etiladi.

---

## 7. ON DELETE/UPDATE CASCADE va referential integrity

### Nazariya
- ON DELETE/UPDATE CASCADE — bog'liq yozuvlar o'chirilganda/yangilanganda avtomatik o'zgarish.
- Referential integrity — ma'lumotlar bog'liqligini saqlash.

### Misol
```sql
CREATE TABLE parent (
    id SERIAL PRIMARY KEY
);
CREATE TABLE child (
    id SERIAL PRIMARY KEY,
    parent_id INT REFERENCES parent(id) ON DELETE CASCADE
);
```
**Natija:** Ota yozuvi o'chirilsa, unga bog'liq barcha child yozuvlar ham o'chadi.

**Izoh:** CASCADE opsiyasi ma'lumotlar yaxlitligini avtomatik ta'minlaydi.

---

## 8. ER-diagram va best practices

### Nazariya
- ER-diagram — jadvallar va ularning bog'lanishini grafik ko'rinishda chizish.
- Best practices — nomlash, cheklovlar, zaxiralash, soddalik.

### Tavsiyalar
- Jadval va ustun nomlarini aniq va tushunarli tanlang.
- Katta loyihalarda ER-diagram chizing.
- O'zgartirishdan oldin har doim backup qiling.
- Cheklovlardan foydalaning.

---

## 9. Xulosa va amaliy maslahatlar
- Jadval dizayni — ma'lumotlar bazasining eng muhim qismi.
- Har bir jadvalda PRIMARY KEY va kerakli cheklovlar bo'lishi shart.
- Munosabatlarni to'g'ri loyihalang: 1:1, 1:N, N:M.
- Takrorlanuvchi ma'lumotlarni alohida jadvallarga ajrating.
- Jadval tuzilmasini o'zgartirishda ehtiyot bo'ling.
- Ma'lumotlar yaxlitligini har doim nazorat qiling.

---

## 📌 Keyingi dars:
[Lesson 19 — Transactionlar va xavfsiz o‘zgartirishlar](../lesson_19/lesson.md) 