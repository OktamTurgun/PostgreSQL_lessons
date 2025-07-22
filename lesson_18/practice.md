# 📝 Amaliyot — Jadvallarni to'g'ri dizayn qilish (chuqur)

Quyidagi topshiriqlar orqali darsda o'rgangan barcha asosiy mavzularni mustahkamlab oling. Har bir topshiriq uchun CREATE TABLE yoki ALTER TABLE so'rovini yozing, qisqacha izoh va natijasini ko'rsating.

---

## 1. To'g'ri dizayn qilish

### 1.1. Oddiy jadval yarating
**Vazifa:** "students" jadvalini yarating. Ustunlar: id (PRIMARY KEY), name (NOT NULL), age (0 dan katta), email (UNIQUE), city (DEFAULT 'Toshkent').

```sql
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    age INT CHECK (age > 0),
    email VARCHAR(100) UNIQUE,
    city VARCHAR(50) DEFAULT 'Toshkent'
);
```
**Izoh:** Har bir ustun uchun cheklovlar qo‘llanilgan.

---

## 2. ALTER TABLE buyrug'i

### 2.1. Ustun qo'shish
**Vazifa:** "students" jadvaliga "phone" ustunini qo‘shing.

```sql
ALTER TABLE students ADD COLUMN phone VARCHAR(20);
```
**Natija:** Jadvalga yangi ustun qo‘shildi.

### 2.2. Ustun nomini o‘zgartirish
**Vazifa:** "phone" ustunini "phone_number" deb o‘zgartiring.

```sql
ALTER TABLE students RENAME COLUMN phone TO phone_number;
```
**Natija:** Ustun nomi o‘zgardi.

### 2.3. Cheklov qo‘shish
**Vazifa:** "age" ustuniga musbat qiymat cheklovi qo‘shing.

```sql
ALTER TABLE students ADD CONSTRAINT age_positive CHECK (age > 0);
```
**Natija:** Faqat musbat yosh kiritiladi.

---

## 3. Alohida jadvalga olib chiqish

### 3.1. Yomon va to‘g‘ri dizaynni solishtiring
**Vazifa:** "orders" jadvalini yomon va to‘g‘ri dizayn bilan yarating.

**Yomon dizayn:**
```sql
CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    customer_name VARCHAR(50),
    product_name VARCHAR(50),
    quantity INT
);
```
**To‘g‘ri dizayn:**
```sql
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
**Izoh:** Takrorlanuvchi ma’lumotlar alohida jadvallarga ajratildi.

---

## 4. Jadvallar orasidagi munosabat turlari

### 4.1. 1:1 munosabat
**Vazifa:** Har bir student uchun bitta passport bo‘lsin.
```sql
CREATE TABLE passports (
    id SERIAL PRIMARY KEY,
    student_id INT UNIQUE REFERENCES students(id)
);
```
**Izoh:** Har bir studentga faqat bitta passport bog‘lanadi.

### 4.2. 1:N munosabat
**Vazifa:** Har bir groupda bir nechta student bo‘lsin.
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
**Izoh:** Bir groupda ko‘plab student bo‘lishi mumkin.

### 4.3. N:M munosabat
**Vazifa:** Studentlar ko‘plab kurslarga yozilishi mumkin.
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
**Izoh:** Oraliq jadval orqali ko‘pdan-ko‘p bog‘lanish amalga oshiriladi.

### 4.4. ON DELETE CASCADE
**Vazifa:** Ota o‘chirilsa, bolalar ham o‘chsin.
```sql
CREATE TABLE parent (
    id SERIAL PRIMARY KEY
);
CREATE TABLE child (
    id SERIAL PRIMARY KEY,
    parent_id INT REFERENCES parent(id) ON DELETE CASCADE
);
```
**Izoh:** Ota yozuvi o‘chirilsa, unga bog‘liq barcha child yozuvlar ham o‘chadi.

---

## 5. Boshqa muhim mavzular

### 5.1. ER-diagram haqida qisqacha
**Vazifa:** Jadval va ularning bog‘lanishini grafik ko‘rinishda chizing (qog‘ozda yoki onlayn vositalarda).

**Izoh:** ER-diagram loyihani vizual ko‘rishga yordam beradi.

### 5.2. Best practices
- Jadval va ustun nomlarini aniq va tushunarli tanlang
- O‘zgartirishdan oldin har doim backup qiling
- Cheklovlardan foydalaning

---

Har bir topshiriqni bajaring, natijani tahlil qiling va savollaringiz bo‘lsa, yozib qoldiring. 