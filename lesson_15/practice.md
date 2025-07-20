# 🎯 Lesson 15 — Amaliy mashgʼulotlar

## 📋 Dars mazmuni
- INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL JOIN operatorlari bilan ishlash
- CROSS JOIN bilan kombinatsiyalar yaratish
- Murakkab JOIN soʼrovlar
- Bir nechta jadval bilan ishlash

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
    email VARCHAR(100),
    scholarship DECIMAL(10,2)
);

-- Maʼlumotlarni kiritish
INSERT INTO students (name, surname, age, grade, city, phone, email, scholarship) VALUES
('Aziz', 'Karimov', 20, 'A', 'Tashkent', '+998901234567', 'aziz@email.com', 500000),
('Malika', 'Rahimova', 19, 'B', 'Samarkand', '+998901234568', 'malika@email.com', 300000),
('Jasur', 'Toshmatov', 22, 'A', 'Tashkent', NULL, 'jasur@email.com', 500000),
('Dilfuza', 'Nazarova', 18, 'C', 'Bukhara', '+998901234569', NULL, 200000),
('Akmal', 'Sobirov', 21, 'B', 'Tashkent', '+998901234570', 'akmal@email.com', 300000),
('Zarina', 'Mirzaeva', 20, 'A', 'Samarkand', NULL, 'zarina@email.com', 500000),
('Bekzod', 'Alimov', 19, 'C', 'Tashkent', '+998901234571', 'bekzod@email.com', 200000),
('Nilufar', 'Kadirova', 23, 'A', 'Bukhara', '+998901234572', 'nilufar@email.com', 500000),
('Rustam', 'Yuldashev', 18, 'B', 'Tashkent', '+998901234573', 'rustam@email.com', 300000),
('Maftuna', 'Hasanova', 20, 'A', 'Samarkand', NULL, 'maftuna@email.com', 500000);

-- Mahsulotlar jadvali
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    price DECIMAL(10,2),
    category VARCHAR(30),
    brand VARCHAR(50),
    description TEXT,
    created_date DATE,
    stock_quantity INTEGER
);

INSERT INTO products (name, price, category, brand, description, created_date, stock_quantity) VALUES
('iPhone 13', 1200000, 'Phone', 'Apple', 'Smartphone with advanced features', '2023-01-15', 50),
('Samsung Galaxy S21', 900000, 'Phone', 'Samsung', 'Android smartphone', '2023-02-20', 30),
('MacBook Pro', 2500000, 'Laptop', 'Apple', 'Professional laptop', '2023-03-10', 20),
('Dell XPS 13', 1800000, 'Laptop', 'Dell', 'Ultrabook laptop', '2023-01-25', 15),
('iPad Air', 800000, 'Tablet', 'Apple', 'Lightweight tablet', '2023-04-05', 40),
('Samsung Tab S7', 600000, 'Tablet', 'Samsung', 'Android tablet', '2023-02-15', 25),
('AirPods Pro', 300000, 'Headphones', 'Apple', 'Wireless earbuds', '2023-05-12', 100),
('Sony WH-1000XM4', 400000, 'Headphones', 'Sony', 'Noise cancelling headphones', '2023-03-28', 60),
('Apple Watch', 500000, 'Smartwatch', 'Apple', 'Fitness tracking watch', '2023-06-01', 35),
('Samsung Galaxy Watch', 350000, 'Smartwatch', 'Samsung', 'Android smartwatch', '2023-04-18', 45);

-- Buyurtmalar jadvali
CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    student_id INTEGER REFERENCES students(id),
    product_id INTEGER REFERENCES products(id),
    quantity INTEGER,
    order_date DATE,
    total_amount DECIMAL(10,2)
);

INSERT INTO orders (student_id, product_id, quantity, order_date, total_amount) VALUES
(1, 1, 1, '2023-12-01', 1200000),
(2, 5, 1, '2023-12-02', 800000),
(3, 7, 2, '2023-12-03', 600000),
(4, 2, 1, '2023-12-04', 900000),
(5, 3, 1, '2023-12-05', 2500000),
(6, 8, 1, '2023-12-06', 400000),
(7, 9, 1, '2023-12-07', 500000),
(8, 10, 1, '2023-12-08', 350000),
(1, 6, 1, '2023-12-09', 600000),
(2, 4, 1, '2023-12-10', 1800000);

-- Kategoriyalar jadvali
CREATE TABLE categories (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50),
    description TEXT,
    created_date DATE
);

INSERT INTO categories (name, description, created_date) VALUES
('Phone', 'Mobile phones and smartphones', '2023-01-01'),
('Laptop', 'Portable computers and notebooks', '2023-01-01'),
('Tablet', 'Tablet computers and iPads', '2023-01-01'),
('Headphones', 'Audio devices and earphones', '2023-01-01'),
('Smartwatch', 'Wearable technology devices', '2023-01-01');
```

---

## 🎯 Mashgʼulot 1: INNER JOIN

### Vazifa 1.1
**Savol:** Oʼquvchilar va ularning buyurtmalari maʼlumotlarini koʼrsating.

```sql
-- Yechim:
SELECT s.name, s.surname, o.order_date, o.total_amount
FROM students s
INNER JOIN orders o ON s.id = o.student_id;
```

### Vazifa 1.2
**Savol:** Mahsulotlar va ularning buyurtmalari maʼlumotlarini koʼrsating.

```sql
-- Yechim:
SELECT p.name, p.brand, o.quantity, o.total_amount
FROM products p
INNER JOIN orders o ON p.id = o.product_id;
```

### Vazifa 1.3
**Savol:** Oʼquvchilar, mahsulotlar va buyurtmalar maʼlumotlarini koʼrsating.

```sql
-- Yechim:
SELECT s.name, s.surname, p.name as mahsulot, o.total_amount
FROM students s
INNER JOIN orders o ON s.id = o.student_id
INNER JOIN products p ON o.product_id = p.id;
```

### Vazifa 1.4
**Savol:** A balli oʼquvchilar va ularning buyurtmalari.

```sql
-- Yechim:
SELECT s.name, s.surname, o.order_date, o.total_amount
FROM students s
INNER JOIN orders o ON s.id = o.student_id
WHERE s.grade = 'A';
```

---

## 🎯 Mashgʼulot 2: LEFT JOIN

### Vazifa 2.1
**Savol:** Barcha oʼquvchilar va ularning buyurtmalari (buyurtmasi yoʼq boʼlsa ham).

```sql
-- Yechim:
SELECT s.name, s.surname, o.order_date, o.total_amount
FROM students s
LEFT JOIN orders o ON s.id = o.student_id;
```

### Vazifa 2.2
**Savol:** Barcha mahsulotlar va ularning sotilish maʼlumotlari.

```sql
-- Yechim:
SELECT p.name, p.brand, COUNT(o.id) as sotilgan_soni
FROM products p
LEFT JOIN orders o ON p.id = o.product_id
GROUP BY p.id, p.name, p.brand;
```

### Vazifa 2.3
**Savol:** Oʼquvchilar va ularning buyurtmalari (NULL boʼlsa ham koʼrsating).

```sql
-- Yechim:
SELECT s.name, s.surname, 
       CASE WHEN o.id IS NULL THEN 'Buyurtma yoʼq' 
            ELSE 'Buyurtma bor' END as holat
FROM students s
LEFT JOIN orders o ON s.id = o.student_id;
```

### Vazifa 2.4
**Savol:** Tashkentlik oʼquvchilar va ularning buyurtmalari.

```sql
-- Yechim:
SELECT s.name, s.surname, o.total_amount
FROM students s
LEFT JOIN orders o ON s.id = o.student_id
WHERE s.city = 'Tashkent';
```

---

## 🎯 Mashgʼulot 3: RIGHT JOIN

### Vazifa 3.1
**Savol:** Barcha buyurtmalar va ularning oʼquvchilari.

```sql
-- Yechim:
SELECT o.order_date, o.total_amount, s.name, s.surname
FROM students s
RIGHT JOIN orders o ON s.id = o.student_id;
```

### Vazifa 3.2
**Savol:** Barcha buyurtmalar va mahsulotlar maʼlumotlari.

```sql
-- Yechim:
SELECT o.order_date, p.name, p.brand, o.quantity
FROM products p
RIGHT JOIN orders o ON p.id = o.product_id;
```

### Vazifa 3.3
**Savol:** Buyurtmalar va ularning oʼquvchilari (sana boʼyicha tartiblangan).

```sql
-- Yechim:
SELECT o.order_date, s.name, s.surname, o.total_amount
FROM students s
RIGHT JOIN orders o ON s.id = o.student_id
ORDER BY o.order_date;
```

---

## 🎯 Mashgʼulot 4: FULL JOIN

### Vazifa 4.1
**Savol:** Barcha oʼquvchilar va barcha buyurtmalar.

```sql
-- Yechim:
SELECT s.name, s.surname, o.order_date, o.total_amount
FROM students s
FULL JOIN orders o ON s.id = o.student_id;
```

### Vazifa 4.2
**Savol:** Barcha mahsulotlar va barcha buyurtmalar.

```sql
-- Yechim:
SELECT p.name, p.brand, o.order_date, o.quantity
FROM products p
FULL JOIN orders o ON p.id = o.product_id;
```

### Vazifa 4.3
**Savol:** Oʼquvchilar va buyurtmalar (NULL qiymatlarni koʼrsating).

```sql
-- Yechim:
SELECT s.name, s.surname, o.order_date, o.total_amount
FROM students s
FULL JOIN orders o ON s.id = o.student_id
WHERE s.name IS NULL OR o.order_date IS NULL;
```

---

## 🎯 Mashgʼulot 5: CROSS JOIN

### Vazifa 5.1
**Savol:** Barcha oʼquvchilar va barcha mahsulotlar kombinatsiyasi.

```sql
-- Yechim:
SELECT s.name, s.surname, p.name as mahsulot, p.price
FROM students s
CROSS JOIN products p;
```

### Vazifa 5.2
**Savol:** Har bir oʼquvchi uchun har bir kategoriya.

```sql
-- Yechim:
SELECT s.name, c.name as kategoriya
FROM students s
CROSS JOIN categories c;
```

### Vazifa 5.3
**Savol:** Oʼquvchilar va mahsulotlar (faqat 5 ta natija).

```sql
-- Yechim:
SELECT s.name, p.name as mahsulot
FROM students s
CROSS JOIN products p
LIMIT 5;
```

---

## 🎯 Mashgʼulot 6: Murakkab JOIN soʼrovlar

### Vazifa 6.1
**Savol:** Oʼquvchilar, ularning buyurtmalari va mahsulotlar toʼliq maʼlumoti.

```sql
-- Yechim:
SELECT s.name, s.surname, p.name as mahsulot, 
       o.quantity, o.total_amount, o.order_date
FROM students s
INNER JOIN orders o ON s.id = o.student_id
INNER JOIN products p ON o.product_id = p.id
ORDER BY s.name, o.order_date;
```

### Vazifa 6.2
**Savol:** Har oʼquvchining buyurtmalari soni va umumiy summa.

```sql
-- Yechim:
SELECT s.name, s.surname, 
       COUNT(o.id) as buyurtmalar_soni,
       SUM(o.total_amount) as umumiy_summa
FROM students s
LEFT JOIN orders o ON s.id = o.student_id
GROUP BY s.id, s.name, s.surname
ORDER BY umumiy_summa DESC;
```

### Vazifa 6.3
**Savol:** Har mahsulotning nechta marta sotilgani va umumiy tushumi.

```sql
-- Yechim:
SELECT p.name, p.brand, 
       COUNT(o.id) as sotilgan_soni,
       SUM(o.total_amount) as umumiy_tushum
FROM products p
LEFT JOIN orders o ON p.id = o.product_id
GROUP BY p.id, p.name, p.brand
ORDER BY umumiy_tushum DESC;
```

### Vazifa 6.4
**Savol:** Har brenddagi mahsulotlar va ularning sotilish statistikasi.

```sql
-- Yechim:
SELECT p.brand,
       COUNT(DISTINCT p.id) as mahsulotlar_soni,
       COUNT(o.id) as sotilgan_soni,
       SUM(o.total_amount) as umumiy_tushum
FROM products p
LEFT JOIN orders o ON p.id = o.product_id
GROUP BY p.brand
ORDER BY umumiy_tushum DESC;
```

---

## 🎯 Mashgʼulot 7: JOIN turlari taqqoslash

### Vazifa 7.1
**Savol:** INNER JOIN vs LEFT JOIN taqqoslash - oʼquvchilar va buyurtmalar.

```sql
-- INNER JOIN: faqat buyurtmasi bor oʼquvchilar
SELECT s.name, COUNT(o.id) as buyurtmalar_soni
FROM students s
INNER JOIN orders o ON s.id = o.student_id
GROUP BY s.id, s.name;

-- LEFT JOIN: barcha oʼquvchilar (buyurtmasi yoʼq boʼlsa ham)
SELECT s.name, COUNT(o.id) as buyurtmalar_soni
FROM students s
LEFT JOIN orders o ON s.id = o.student_id
GROUP BY s.id, s.name;
```

### Vazifa 7.2
**Savol:** LEFT JOIN vs RIGHT JOIN taqqoslash.

```sql
-- LEFT JOIN: barcha oʼquvchilar
SELECT s.name, o.order_date
FROM students s
LEFT JOIN orders o ON s.id = o.student_id;

-- RIGHT JOIN: barcha buyurtmalar
SELECT s.name, o.order_date
FROM students s
RIGHT JOIN orders o ON s.id = o.student_id;
```

---

## 🎯 Mashgʼulot 8: JOIN shartlari

### Vazifa 8.1
**Savol:** Oʼquvchilar va ularning 2023-yilgi buyurtmalari.

```sql
-- Yechim:
SELECT s.name, s.surname, o.order_date, o.total_amount
FROM students s
INNER JOIN orders o ON s.id = o.student_id 
    AND o.order_date >= '2023-01-01' 
    AND o.order_date <= '2023-12-31';
```

### Vazifa 8.2
**Savol:** A balli oʼquvchilar va ularning qimmat buyurtmalari.

```sql
-- Yechim:
SELECT s.name, s.surname, o.total_amount
FROM students s
INNER JOIN orders o ON s.id = o.student_id
WHERE s.grade = 'A' AND o.total_amount > 1000000;
```

### Vazifa 8.3
**Savol:** Apple brendidagi mahsulotlar va ularning buyurtmalari.

```sql
-- Yechim:
SELECT p.name, o.quantity, o.total_amount
FROM products p
LEFT JOIN orders o ON p.id = o.product_id
WHERE p.brand = 'Apple';
```

---

## 🎯 Qoʼshimcha vazifalar

### Vazifa 9.1
**Savol:** Har oy qaysi mahsulotlar sotilgan va ularning umumiy miqdori.

```sql
-- Yechim:
SELECT 
    EXTRACT(MONTH FROM o.order_date) as oy,
    p.name,
    COUNT(o.id) as sotilgan_soni,
    SUM(o.total_amount) as umumiy_summa
FROM products p
INNER JOIN orders o ON p.id = o.product_id
GROUP BY EXTRACT(MONTH FROM o.order_date), p.name
ORDER BY oy, umumiy_summa DESC;
```

### Vazifa 9.2
**Savol:** Har shahardagi oʼquvchilar va ularning buyurtmalari statistikasi.

```sql
-- Yechim:
SELECT s.city,
       COUNT(DISTINCT s.id) as oquvchilar_soni,
       COUNT(o.id) as buyurtmalar_soni,
       SUM(o.total_amount) as umumiy_summa
FROM students s
LEFT JOIN orders o ON s.id = o.student_id
GROUP BY s.city
ORDER BY umumiy_summa DESC;
```

### Vazifa 9.3
**Savol:** Har kategoriyadagi mahsulotlar va ularning sotilish maʼlumotlari.

```sql
-- Yechim:
SELECT p.category,
       COUNT(DISTINCT p.id) as mahsulotlar_soni,
       COUNT(o.id) as sotilgan_soni,
       ROUND(AVG(p.price), 2) as o_rtacha_narx
FROM products p
LEFT JOIN orders o ON p.id = o.product_id
GROUP BY p.category
ORDER BY sotilgan_soni DESC;
```

---

## 📌 Natijalarni tekshirish

Har bir vazifani bajarganingizdan soʼng, natijalarni tekshiring:

1. **INNER JOIN** — faqat mos keladigan yozuvlar qaytarilganmi?
2. **LEFT JOIN** — chap jadvaldagi barcha yozuvlar qaytarilganmi?
3. **RIGHT JOIN** — oʼng jadvaldagi barcha yozuvlar qaytarilganmi?
4. **FULL JOIN** — ikkala jadvaldagi barcha yozuvlar qaytarilganmi?
5. **CROSS JOIN** — barcha kombinatsiyalar qaytarilganmi?

---

## 📌 Keyingi darsga tayyorgarlik

Keyingi darsda quyidagilarni oʼrganamiz:
- Subquery (ichki soʼrovlar)
- EXISTS operatori
- IN va NOT IN operatorlari
- Murakkab ichki soʼrovlar 