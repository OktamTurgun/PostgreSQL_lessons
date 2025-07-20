# 🎯 Lesson 14 — Amaliy mashgʼulotlar

## 📋 Dars mazmuni
- COUNT(), SUM(), AVG(), MAX(), MIN() funksiyalari bilan ishlash
- GROUP BY operatori bilan maʼlumotlarni guruhlash
- HAVING operatori bilan guruhlar boʼyicha filtrlash
- Murakkab aggregate soʼrovlar

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
('Maftuna', 'Hasanova', 20, 'A', 'Samarkand', NULL, 'maftuna@email.com', 500000),
('Shahzod', 'Umarov', 21, 'B', 'Tashkent', '+998901234574', 'shahzod@email.com', 300000),
('Gulnora', 'Saidova', 19, 'A', 'Samarkand', '+998901234575', 'gulnora@email.com', 500000),
('Farrukh', 'Khalilov', 22, 'C', 'Bukhara', NULL, 'farrukh@email.com', 200000),
('Durdona', 'Muminova', 18, 'A', 'Tashkent', '+998901234576', 'durdona@email.com', 500000),
('Izzatillo', 'Rasulov', 20, 'B', 'Samarkand', '+998901234577', 'izzatillo@email.com', 300000);

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
('Samsung Galaxy Watch', 350000, 'Smartwatch', 'Samsung', 'Android smartwatch', '2023-04-18', 45),
('iPhone 14', 1500000, 'Phone', 'Apple', 'Latest iPhone model', '2023-07-20', 30),
('Google Pixel 7', 1100000, 'Phone', 'Google', 'Android flagship', '2023-08-15', 20),
('Lenovo ThinkPad', 2200000, 'Laptop', 'Lenovo', 'Business laptop', '2023-09-05', 10),
('HP Pavilion', 1200000, 'Laptop', 'HP', 'Home laptop', '2023-10-12', 25),
('iPad Pro', 1200000, 'Tablet', 'Apple', 'Professional tablet', '2023-11-08', 15);

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
(9, 11, 1, '2023-12-09', 1500000),
(10, 12, 1, '2023-12-10', 1100000),
(1, 6, 1, '2023-12-11', 600000),
(2, 13, 1, '2023-12-12', 2200000),
(3, 14, 1, '2023-12-13', 1200000),
(4, 15, 1, '2023-12-14', 1200000),
(5, 1, 1, '2023-12-15', 1200000);
```

---

## 🎯 Mashgʼulot 1: COUNT() funksiyasi

### Vazifa 1.1
**Savol:** Barcha oʼquvchilar soni qancha?

```sql
-- Yechim:
SELECT COUNT(*) FROM students;
```

### Vazifa 1.2
**Savol:** Telefon raqami bor oʼquvchilar soni qancha?

```sql
-- Yechim:
SELECT COUNT(phone) FROM students;
```

### Vazifa 1.3
**Savol:** Har xil shaharlar soni qancha?

```sql
-- Yechim:
SELECT COUNT(DISTINCT city) FROM students;
```

### Vazifa 1.4
**Savol:** A balli oʼquvchilar soni qancha?

```sql
-- Yechim:
SELECT COUNT(*) FROM students WHERE grade = 'A';
```

### Vazifa 1.5
**Savol:** Email manzili yoʼq oʼquvchilar soni qancha?

```sql
-- Yechim:
SELECT COUNT(*) FROM students WHERE email IS NULL;
```

---

## 🎯 Mashgʼulot 2: SUM() funksiyasi

### Vazifa 2.1
**Savol:** Barcha mahsulotlar narxi yigʼindisi qancha?

```sql
-- Yechim:
SELECT SUM(price) FROM products;
```

### Vazifa 2.2
**Savol:** Apple brendidagi mahsulotlar narxi yigʼindisi qancha?

```sql
-- Yechim:
SELECT SUM(price) FROM products WHERE brand = 'Apple';
```

### Vazifa 2.3
**Savol:** 1000000 dan yuqori mahsulotlar narxi yigʼindisi qancha?

```sql
-- Yechim:
SELECT SUM(price) FROM products WHERE price > 1000000;
```

### Vazifa 2.4
**Savol:** Barcha oʼquvchilarning stipendiya yigʼindisi qancha?

```sql
-- Yechim:
SELECT SUM(scholarship) FROM students;
```

---

## 🎯 Mashgʼulot 3: AVG() funksiyasi

### Vazifa 3.1
**Savol:** Oʼquvchilarning oʼrtacha yoshi qancha?

```sql
-- Yechim:
SELECT ROUND(AVG(age), 2) FROM students;
```

### Vazifa 3.2
**Savol:** Mahsulotlarning oʼrtacha narxi qancha?

```sql
-- Yechim:
SELECT ROUND(AVG(price), 2) FROM products;
```

### Vazifa 3.3
**Savol:** A balli oʼquvchilarning oʼrtacha yoshi qancha?

```sql
-- Yechim:
SELECT ROUND(AVG(age), 2) FROM students WHERE grade = 'A';
```

### Vazifa 3.4
**Savol:** Tashkentlik oʼquvchilarning oʼrtacha stipendiyasi qancha?

```sql
-- Yechim:
SELECT ROUND(AVG(scholarship), 2) FROM students WHERE city = 'Tashkent';
```

---

## 🎯 Mashgʼulot 4: MAX() va MIN() funksiyalari

### Vazifa 4.1
**Savol:** Eng katta va eng kichik yosh qancha?

```sql
-- Yechim:
SELECT MAX(age) as eng_katta_yosh, MIN(age) as eng_kichik_yosh FROM students;
```

### Vazifa 4.2
**Savol:** Eng qimmat va eng arzon mahsulot narxi qancha?

```sql
-- Yechim:
SELECT MAX(price) as eng_qimmat, MIN(price) as eng_arzon FROM products;
```

### Vazifa 4.3
**Savol:** Eng yuqori va eng past stipendiya qancha?

```sql
-- Yechim:
SELECT MAX(scholarship) as eng_yuqori_stipendiya, 
       MIN(scholarship) as eng_past_stipendiya 
FROM students;
```

### Vazifa 4.4
**Savol:** Eng koʼp va eng kam zaxira soni qancha?

```sql
-- Yechim:
SELECT MAX(stock_quantity) as eng_ko_p_zaxira, 
       MIN(stock_quantity) as eng_kam_zaxira 
FROM products;
```

---

## 🎯 Mashgʼulot 5: GROUP BY operatori

### Vazifa 5.1
**Savol:** Har shahardagi oʼquvchilar soni qancha?

```sql
-- Yechim:
SELECT city, COUNT(*) as oquvchilar_soni 
FROM students 
GROUP BY city;
```

### Vazifa 5.2
**Savol:** Har ball boʼyicha oʼquvchilar soni qancha?

```sql
-- Yechim:
SELECT grade, COUNT(*) as oquvchilar_soni 
FROM students 
GROUP BY grade;
```

### Vazifa 5.3
**Savol:** Har brenddagi mahsulotlar soni va oʼrtacha narxi qancha?

```sql
-- Yechim:
SELECT brand, 
       COUNT(*) as mahsulotlar_soni,
       ROUND(AVG(price), 2) as o_rtacha_narx
FROM products 
GROUP BY brand;
```

### Vazifa 5.4
**Savol:** Har kategoriyadagi mahsulotlar soni va umumiy narxi qancha?

```sql
-- Yechim:
SELECT category, 
       COUNT(*) as mahsulotlar_soni,
       SUM(price) as umumiy_narx
FROM products 
GROUP BY category;
```

---

## 🎯 Mashgʼulot 6: HAVING operatori

### Vazifa 6.1
**Savol:** 2 tadan koʼp oʼquvchisi bor shaharlar qaysilar?

```sql
-- Yechim:
SELECT city, COUNT(*) as oquvchilar_soni 
FROM students 
GROUP BY city 
HAVING COUNT(*) > 2;
```

### Vazifa 6.2
**Savol:** Oʼrtacha narxi 1000000 dan yuqori brendlar qaysilar?

```sql
-- Yechim:
SELECT brand, ROUND(AVG(price), 2) as o_rtacha_narx
FROM products 
GROUP BY brand 
HAVING AVG(price) > 1000000;
```

### Vazifa 6.3
**Savol:** 3 tadan koʼp mahsuloti bor kategoriyalar qaysilar?

```sql
-- Yechim:
SELECT category, COUNT(*) as mahsulotlar_soni
FROM products 
GROUP BY category 
HAVING COUNT(*) > 3;
```

### Vazifa 6.4
**Savol:** Oʼrtacha stipendiyasi 400000 dan yuqori ballar qaysilar?

```sql
-- Yechim:
SELECT grade, ROUND(AVG(scholarship), 2) as o_rtacha_stipendiya
FROM students 
GROUP BY grade 
HAVING AVG(scholarship) > 400000;
```

---

## 🎯 Mashgʼulot 7: Murakkab soʼrovlar

### Vazifa 7.1
**Savol:** Har shahardagi toʼliq statistika (oʼquvchilar soni, oʼrtacha yosh, eng katta va eng kichik yosh).

```sql
-- Yechim:
SELECT city,
       COUNT(*) as oquvchilar_soni,
       ROUND(AVG(age), 2) as o_rtacha_yosh,
       MAX(age) as eng_katta_yosh,
       MIN(age) as eng_kichik_yosh
FROM students 
GROUP BY city;
```

### Vazifa 7.2
**Savol:** Har brenddagi mahsulotlar statistikasi (soni, oʼrtacha narx, eng qimmat, eng arzon, umumiy narx).

```sql
-- Yechim:
SELECT brand,
       COUNT(*) as mahsulotlar_soni,
       ROUND(AVG(price), 2) as o_rtacha_narx,
       MAX(price) as eng_qimmat,
       MIN(price) as eng_arzon,
       SUM(price) as umumiy_narx
FROM products 
GROUP BY brand;
```

### Vazifa 7.3
**Savol:** Har ball boʼyicha statistika (oʼquvchilar soni, oʼrtacha yosh, telefon raqami bor oʼquvchilar soni).

```sql
-- Yechim:
SELECT grade,
       COUNT(*) as oquvchilar_soni,
       ROUND(AVG(age), 2) as o_rtacha_yosh,
       COUNT(CASE WHEN phone IS NOT NULL THEN 1 END) as telefon_bor
FROM students 
GROUP BY grade;
```

### Vazifa 7.4
**Savol:** Har kategoriyadagi mahsulotlar statistikasi (soni, oʼrtacha narx, umumiy zaxira, oʼrtacha zaxira).

```sql
-- Yechim:
SELECT category,
       COUNT(*) as mahsulotlar_soni,
       ROUND(AVG(price), 2) as o_rtacha_narx,
       SUM(stock_quantity) as umumiy_zaxira,
       ROUND(AVG(stock_quantity), 2) as o_rtacha_zaxira
FROM products 
GROUP BY category;
```

---

## 🎯 Mashgʼulot 8: WHERE va HAVING birgalikda

### Vazifa 8.1
**Savol:** Tashkentlik oʼquvchilarni guruhlash, 2 tadan koʼp boʼlsa.

```sql
-- Yechim:
SELECT city, COUNT(*) as oquvchilar_soni
FROM students 
WHERE city = 'Tashkent'
GROUP BY city 
HAVING COUNT(*) > 2;
```

### Vazifa 8.2
**Savol:** Apple brendidagi mahsulotlarni guruhlash, oʼrtacha narxi 1000000 dan yuqori boʼlsa.

```sql
-- Yechim:
SELECT brand, ROUND(AVG(price), 2) as o_rtacha_narx
FROM products 
WHERE brand = 'Apple'
GROUP BY brand 
HAVING AVG(price) > 1000000;
```

### Vazifa 8.3
**Savol:** A balli oʼquvchilarni shahar boʼyicha guruhlash, 2 tadan koʼp boʼlsa.

```sql
-- Yechim:
SELECT city, COUNT(*) as oquvchilar_soni
FROM students 
WHERE grade = 'A'
GROUP BY city 
HAVING COUNT(*) > 2;
```

---

## 🎯 Mashgʼulot 9: DISTINCT bilan aggregate funksiyalar

### Vazifa 9.1
**Savol:** Har xil yoshlar soni qancha?

```sql
-- Yechim:
SELECT COUNT(DISTINCT age) FROM students;
```

### Vazifa 9.2
**Savol:** Har xil narxlar soni qancha?

```sql
-- Yechim:
SELECT COUNT(DISTINCT price) FROM products;
```

### Vazifa 9.3
**Savol:** Har xil stipendiya miqdorlari soni qancha?

```sql
-- Yechim:
SELECT COUNT(DISTINCT scholarship) FROM students;
```

---

## 🎯 Qoʼshimcha vazifalar

### Vazifa 10.1
**Savol:** Har oy qaysi mahsulotlar sotilgan va ularning umumiy miqdori qancha?

```sql
-- Yechim:
SELECT 
    EXTRACT(MONTH FROM order_date) as oy,
    COUNT(*) as buyurtmalar_soni,
    SUM(total_amount) as umumiy_summa
FROM orders 
GROUP BY EXTRACT(MONTH FROM order_date)
ORDER BY oy;
```

### Vazifa 10.2
**Savol:** Har oʼquvchining nechta buyurtmasi bor va ularning umumiy summası qancha?

```sql
-- Yechim:
SELECT 
    s.name,
    s.surname,
    COUNT(o.id) as buyurtmalar_soni,
    SUM(o.total_amount) as umumiy_summa
FROM students s
LEFT JOIN orders o ON s.id = o.student_id
GROUP BY s.id, s.name, s.surname
ORDER BY umumiy_summa DESC;
```

### Vazifa 10.3
**Savol:** Har mahsulotning nechta marta sotilgani va umumiy tushumi qancha?

```sql
-- Yechim:
SELECT 
    p.name,
    p.brand,
    COUNT(o.id) as sotilgan_soni,
    SUM(o.total_amount) as umumiy_tushum
FROM products p
LEFT JOIN orders o ON p.id = o.product_id
GROUP BY p.id, p.name, p.brand
ORDER BY umumiy_tushum DESC;
```

---

## 📌 Natijalarni tekshirish

Har bir vazifani bajarganingizdan soʼng, natijalarni tekshiring:

1. **COUNT()** — toʼgʼri son qaytarilganmi?
2. **SUM()** — yigʼindi toʼgʼri hisoblanganmi?
3. **AVG()** — oʼrtacha toʼgʼri hisoblanganmi?
4. **GROUP BY** — guruhlar toʼgʼri ajratilganmi?
5. **HAVING** — shartlar toʼgʼri qoʼyilganmi?

---

## 📌 Keyingi darsga tayyorgarlik

Keyingi darsda quyidagilarni oʼrganamiz:
- JOIN operatorlari (INNER, LEFT, RIGHT, FULL)
- Jadvalarni birlashtirish
- Murakkab soʼrovlar
- Maʼlumotlarni turli jadvallardan olish 