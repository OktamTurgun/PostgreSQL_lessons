# 🎯 Lesson 12 — Amaliy mashgʼulotlar

## 📋 Dars mazmuni
- LIKE, ILIKE operatorlari bilan ishlash
- BETWEEN operatori yordamida oralik qidirish
- IN operatori bilan roʼyxatdagi qiymatlarni qidirish
- IS NULL operatori bilan boʼsh qiymatlarni topish

---

## 🗄️ Namuna maʼlumotlar bazasi

```sql
-- Oʼquvchilar jadvali
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

-- Maʼlumotlarni kiritish
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

-- Mahsulotlar jadvali
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    price DECIMAL(10,2),
    category VARCHAR(30),
    brand VARCHAR(50),
    description TEXT
);

INSERT INTO products (name, price, category, brand, description) VALUES
('iPhone 13', 1200000, 'Phone', 'Apple', 'Smartphone with advanced features'),
('Samsung Galaxy S21', 900000, 'Phone', 'Samsung', 'Android smartphone'),
('MacBook Pro', 2500000, 'Laptop', 'Apple', 'Professional laptop'),
('Dell XPS 13', 1800000, 'Laptop', 'Dell', 'Ultrabook laptop'),
('iPad Air', 800000, 'Tablet', 'Apple', 'Lightweight tablet'),
('Samsung Tab S7', 600000, 'Tablet', 'Samsung', 'Android tablet'),
('AirPods Pro', 300000, 'Headphones', 'Apple', 'Wireless earbuds'),
('Sony WH-1000XM4', 400000, 'Headphones', 'Sony', 'Noise cancelling headphones'),
('Apple Watch', 500000, 'Smartwatch', 'Apple', 'Fitness tracking watch'),
('Samsung Galaxy Watch', 350000, 'Smartwatch', 'Samsung', 'Android smartwatch');
```

---

## 🎯 Mashgʼulot 1: LIKE va ILIKE operatorlari

### Vazifa 1.1
**Savol:** "A" harfi bilan boshlanadigan ismlar qaysilar?

```sql
-- Yechim:
SELECT name, surname FROM students WHERE name LIKE 'A%';
```

### Vazifa 1.2
**Savol:** "ov" bilan tugaydigan familiyalar qaysilar?

```sql
-- Yechim:
SELECT name, surname FROM students WHERE surname LIKE '%ov';
```

### Vazifa 1.3
**Savol:** "a" harfini oʼz ichiga olgan ismlar (katta-kichik harflarni hisobga olmagan holda)?

```sql
-- Yechim:
SELECT name, surname FROM students WHERE name ILIKE '%a%';
```

### Vazifa 1.4
**Savol:** "phone" soʼzini oʼz ichiga olgan mahsulotlar?

```sql
-- Yechim:
SELECT name, price FROM products WHERE name ILIKE '%phone%';
```

---

## 🎯 Mashgʼulot 2: BETWEEN operatori

### Vazifa 2.1
**Savol:** 19-21 yosh oraligʼidagi oʼquvchilar?

```sql
-- Yechim:
SELECT name, surname, age FROM students WHERE age BETWEEN 19 AND 21;
```

### Vazifa 2.2
**Savol:** Narxi 500000-1500000 oraligʼidagi mahsulotlar?

```sql
-- Yechim:
SELECT name, price FROM products WHERE price BETWEEN 500000 AND 1500000;
```

### Vazifa 2.3
**Savol:** Apple brendidagi mahsulotlar va narxi 1000000 dan yuqori boʼlganlar?

```sql
-- Yechim:
SELECT name, brand, price FROM products 
WHERE brand = 'Apple' AND price > 1000000;
```

---

## 🎯 Mashgʼulot 3: IN operatori

### Vazifa 3.1
**Savol:** A yoki B balli oʼquvchilar?

```sql
-- Yechim:
SELECT name, surname, grade FROM students WHERE grade IN ('A', 'B');
```

### Vazifa 3.2
**Savol:** Tashkent yoki Samarkand shaharlaridagi oʼquvchilar?

```sql
-- Yechim:
SELECT name, surname, city FROM students WHERE city IN ('Tashkent', 'Samarkand');
```

### Vazifa 3.3
**Savol:** Phone yoki Laptop kategoriyalaridagi mahsulotlar?

```sql
-- Yechim:
SELECT name, category, price FROM products WHERE category IN ('Phone', 'Laptop');
```

---

## 🎯 Mashgʼulot 4: IS NULL operatori

### Vazifa 4.1
**Savol:** Telefon raqami yoʼq oʼquvchilar?

```sql
-- Yechim:
SELECT name, surname, phone FROM students WHERE phone IS NULL;
```

### Vazifa 4.2
**Savol:** Email manzili yoʼq oʼquvchilar?

```sql
-- Yechim:
SELECT name, surname, email FROM students WHERE email IS NULL;
```

### Vazifa 4.3
**Savol:** Telefon raqami yoki email manzili yoʼq oʼquvchilar?

```sql
-- Yechim:
SELECT name, surname, phone, email FROM students 
WHERE phone IS NULL OR email IS NULL;
```

---

## 🎯 Mashgʼulot 5: Murakkab soʼrovlar

### Vazifa 5.1
**Savol:** Tashkentlik, A balli va telefon raqami yoʼq oʼquvchilar?

```sql
-- Yechim:
SELECT name, surname, city, grade, phone FROM students 
WHERE city = 'Tashkent' AND grade = 'A' AND phone IS NULL;
```

### Vazifa 5.2
**Savol:** "a" harfi bilan boshlanadigan, 19-22 yosh oraligʼida va A yoki B balli oʼquvchilar?

```sql
-- Yechim:
SELECT name, surname, age, grade FROM students 
WHERE name ILIKE 'a%' AND age BETWEEN 19 AND 22 AND grade IN ('A', 'B');
```

### Vazifa 5.3
**Savol:** Apple brendidagi, narxi 500000-2000000 oraligʼida va "phone" soʼzini oʼz ichiga olgan mahsulotlar?

```sql
-- Yechim:
SELECT name, brand, price FROM products 
WHERE brand = 'Apple' AND price BETWEEN 500000 AND 2000000 AND name ILIKE '%phone%';
```

---

## 🎯 Qoʼshimcha mashgʼulotlar

### Vazifa 6.1
**Savol:** Har bir shahardagi oʼquvchilar soni va ularning oʼrtacha yoshi?

```sql
-- Yechim:
SELECT city, COUNT(*) as student_count, AVG(age) as avg_age 
FROM students 
GROUP BY city;
```

### Vazifa 6.2
**Savol:** Har bir ball boʼyicha oʼquvchilar soni va telefon raqami yoʼq oʼquvchilar soni?

```sql
-- Yechim:
SELECT grade, COUNT(*) as total_students, 
       COUNT(CASE WHEN phone IS NULL THEN 1 END) as no_phone_count
FROM students 
GROUP BY grade;
```

### Vazifa 6.3
**Savol:** Har bir brend boʼyicha mahsulotlar soni va ularning oʼrtacha narxi?

```sql
-- Yechim:
SELECT brand, COUNT(*) as product_count, AVG(price) as avg_price 
FROM products 
GROUP BY brand;
```

---

## ✅ Natijalar tekshirish

Har bir vazifani bajarib, natijalarni tekshiring:

1. **LIKE/ILIKE** — toʼgʼri pattern matching
2. **BETWEEN** — chegaralar toʼgʼri kiritilgan
3. **IN** — roʼyxatdagi qiymatlar toʼgʼri
4. **IS NULL** — boʼsh qiymatlar toʼgʼri topilgan
5. **Murakkab soʼrovlar** — barcha shartlar bajarilgan

---

## 📚 Keyingi darsga tayyorgarlik
Keyingi darsda ORDER BY, LIMIT va OFFSET operatorlari bilan tanishingiz! 