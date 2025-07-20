# 🎯 Lesson 13 — Amaliy mashgʼulotlar

## 📋 Dars mazmuni
- ORDER BY operatori bilan natijalarni tartiblash
- LIMIT operatori bilan natijalar sonini cheklash
- OFFSET operatori bilan sahifalash
- Murakkab tartiblash va sahifalash misollari

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
('Maftuna', 'Hasanova', 20, 'A', 'Samarkand', NULL, 'maftuna@email.com'),
('Shahzod', 'Umarov', 21, 'B', 'Tashkent', '+998901234574', 'shahzod@email.com'),
('Gulnora', 'Saidova', 19, 'A', 'Samarkand', '+998901234575', 'gulnora@email.com'),
('Farrukh', 'Khalilov', 22, 'C', 'Bukhara', NULL, 'farrukh@email.com'),
('Durdona', 'Muminova', 18, 'A', 'Tashkent', '+998901234576', 'durdona@email.com'),
('Izzatillo', 'Rasulov', 20, 'B', 'Samarkand', '+998901234577', 'izzatillo@email.com');

-- Mahsulotlar jadvali
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    price DECIMAL(10,2),
    category VARCHAR(30),
    brand VARCHAR(50),
    description TEXT,
    created_date DATE
);

INSERT INTO products (name, price, category, brand, description, created_date) VALUES
('iPhone 13', 1200000, 'Phone', 'Apple', 'Smartphone with advanced features', '2023-01-15'),
('Samsung Galaxy S21', 900000, 'Phone', 'Samsung', 'Android smartphone', '2023-02-20'),
('MacBook Pro', 2500000, 'Laptop', 'Apple', 'Professional laptop', '2023-03-10'),
('Dell XPS 13', 1800000, 'Laptop', 'Dell', 'Ultrabook laptop', '2023-01-25'),
('iPad Air', 800000, 'Tablet', 'Apple', 'Lightweight tablet', '2023-04-05'),
('Samsung Tab S7', 600000, 'Tablet', 'Samsung', 'Android tablet', '2023-02-15'),
('AirPods Pro', 300000, 'Headphones', 'Apple', 'Wireless earbuds', '2023-05-12'),
('Sony WH-1000XM4', 400000, 'Headphones', 'Sony', 'Noise cancelling headphones', '2023-03-28'),
('Apple Watch', 500000, 'Smartwatch', 'Apple', 'Fitness tracking watch', '2023-06-01'),
('Samsung Galaxy Watch', 350000, 'Smartwatch', 'Samsung', 'Android smartwatch', '2023-04-18'),
('iPhone 14', 1500000, 'Phone', 'Apple', 'Latest iPhone model', '2023-07-20'),
('Google Pixel 7', 1100000, 'Phone', 'Google', 'Android flagship', '2023-08-15'),
('Lenovo ThinkPad', 2200000, 'Laptop', 'Lenovo', 'Business laptop', '2023-09-05'),
('HP Pavilion', 1200000, 'Laptop', 'HP', 'Home laptop', '2023-10-12'),
('iPad Pro', 1200000, 'Tablet', 'Apple', 'Professional tablet', '2023-11-08');
```

---

## 🎯 Mashgʼulot 1: ORDER BY operatori

### Vazifa 1.1
**Savol:** Oʼquvchilarni yosh boʼyicha kattadan kichikka tartiblang.

```sql
-- Yechim:
SELECT name, surname, age FROM students ORDER BY age DESC;
```

### Vazifa 1.2
**Savol:** Oʼquvchilarni familiya boʼyicha alfavit tartibida koʼrsating.

```sql
-- Yechim:
SELECT name, surname FROM students ORDER BY surname ASC;
```

### Vazifa 1.3
**Savol:** Mahsulotlarni narx boʼyicha arzonidan qimmatga tartiblang.

```sql
-- Yechim:
SELECT name, price FROM products ORDER BY price ASC;
```

### Vazifa 1.4
**Savol:** Oʼquvchilarni avval ball, keyin yosh boʼyicha tartiblang (ball kamayish tartibida).

```sql
-- Yechim:
SELECT name, surname, grade, age FROM students 
ORDER BY grade DESC, age ASC;
```

---

## 🎯 Mashgʼulot 2: LIMIT operatori

### Vazifa 2.1
**Savol:** Faqat 5 ta oʼquvchi koʼrsating.

```sql
-- Yechim:
SELECT name, surname FROM students LIMIT 5;
```

### Vazifa 2.2
**Savol:** Eng yuqori balli 3 ta oʼquvchi kimlar?

```sql
-- Yechim:
SELECT name, surname, grade FROM students 
ORDER BY grade DESC LIMIT 3;
```

### Vazifa 2.3
**Savol:** Eng qimmat 5 ta mahsulot qaysilar?

```sql
-- Yechim:
SELECT name, price, brand FROM products 
ORDER BY price DESC LIMIT 5;
```

### Vazifa 2.4
**Savol:** Eng arzon 3 ta mahsulot qaysilar?

```sql
-- Yechim:
SELECT name, price, category FROM products 
ORDER BY price ASC LIMIT 3;
```

---

## 🎯 Mashgʼulot 3: OFFSET operatori

### Vazifa 3.1
**Savol:** 1-5 oʼquvchilar (birinchi sahifa).

```sql
-- Yechim:
SELECT name, surname FROM students 
ORDER BY name LIMIT 5 OFFSET 0;
```

### Vazifa 3.2
**Savol:** 6-10 oʼquvchilar (ikkinchi sahifa).

```sql
-- Yechim:
SELECT name, surname FROM students 
ORDER BY name LIMIT 5 OFFSET 5;
```

### Vazifa 3.3
**Savol:** 11-15 oʼquvchilar (uchinchi sahifa).

```sql
-- Yechim:
SELECT name, surname FROM students 
ORDER BY name LIMIT 5 OFFSET 10;
```

### Vazifa 3.4
**Savol:** Mahsulotlarning 2-sahifasini koʼrsating (har sahifada 5 ta).

```sql
-- Yechim:
SELECT name, price, brand FROM products 
ORDER BY price DESC LIMIT 5 OFFSET 5;
```

---

## 🎯 Mashgʼulot 4: Murakkab soʼrovlar

### Vazifa 4.1
**Savol:** Tashkentlik oʼquvchilarni yosh boʼyicha tartiblang va faqat 3 tasini koʼrsating.

```sql
-- Yechim:
SELECT name, surname, age FROM students 
WHERE city = 'Tashkent' 
ORDER BY age ASC LIMIT 3;
```

### Vazifa 4.2
**Savol:** A balli oʼquvchilarni yosh boʼyicha tartiblang va eng kattasi 3 tasini koʼrsating.

```sql
-- Yechim:
SELECT name, surname, age, grade FROM students 
WHERE grade = 'A' 
ORDER BY age DESC LIMIT 3;
```

### Vazifa 4.3
**Savol:** Apple brendidagi mahsulotlarni narx boʼyicha tartiblang va eng qimmati 3 tasini koʼrsating.

```sql
-- Yechim:
SELECT name, price, brand FROM products 
WHERE brand = 'Apple' 
ORDER BY price DESC LIMIT 3;
```

### Vazifa 4.4
**Savol:** Phone kategoriyasidagi mahsulotlarni narx boʼyicha tartiblang va 2-sahifasini koʼrsating (har sahifada 3 ta).

```sql
-- Yechim:
SELECT name, price, brand FROM products 
WHERE category = 'Phone' 
ORDER BY price ASC LIMIT 3 OFFSET 3;
```

---

## 🎯 Mashgʼulot 5: Sahifalash formulasi

### Vazifa 5.1
**Savol:** Oʼquvchilarning 4-sahifasini koʼrsating (har sahifada 4 ta).

```sql
-- Yechim:
-- Formula: OFFSET = (sahifa_raqami - 1) * har_sahifadagi_son
-- OFFSET = (4 - 1) * 4 = 12
SELECT name, surname FROM students 
ORDER BY name LIMIT 4 OFFSET 12;
```

### Vazifa 5.2
**Savol:** Mahsulotlarning 3-sahifasini koʼrsating (har sahifada 5 ta).

```sql
-- Yechim:
-- OFFSET = (3 - 1) * 5 = 10
SELECT name, price, brand FROM products 
ORDER BY price DESC LIMIT 5 OFFSET 10;
```

### Vazifa 5.3
**Savol:** Oʼquvchilarning oxirgi sahifasini koʼrsating (har sahifada 3 ta).

```sql
-- Yechim:
-- Jami 15 ta oʼquvchi, har sahifada 3 ta = 5 sahifa
-- Oxirgi sahifa = 5-sahifa, OFFSET = (5-1) * 3 = 12
SELECT name, surname FROM students 
ORDER BY name LIMIT 3 OFFSET 12;
```

---

## 🎯 Mashgʼulot 6: DISTINCT ON

### Vazifa 6.1
**Savol:** Har shahardan eng yaxshi balli oʼquvchini koʼrsating.

```sql
-- Yechim:
SELECT DISTINCT ON (city) name, surname, city, grade 
FROM students 
ORDER BY city, grade DESC;
```

### Vazifa 6.2
**Savol:** Har brenddan eng qimmat mahsulotni koʼrsating.

```sql
-- Yechim:
SELECT DISTINCT ON (brand) name, brand, price 
FROM products 
ORDER BY brand, price DESC;
```

---

## 🎯 Qoʼshimcha vazifalar

### Vazifa 7.1
**Savol:** Oʼquvchilarni avval familiya, keyin ism boʼyicha tartiblang va faqat 10 tasini koʼrsating.

```sql
-- Yechim:
SELECT name, surname FROM students 
ORDER BY surname ASC, name ASC LIMIT 10;
```

### Vazifa 7.2
**Savol:** Mahsulotlarni avval kategoriya, keyin narx boʼyicha tartiblang va 2-sahifasini koʼrsating (har sahifada 4 ta).

```sql
-- Yechim:
SELECT name, category, price FROM products 
ORDER BY category ASC, price DESC LIMIT 4 OFFSET 4;
```

### Vazifa 7.3
**Savol:** Telefon raqami yoʼq oʼquvchilarni yosh boʼyicha tartiblang va eng kattasi 3 tasini koʼrsating.

```sql
-- Yechim:
SELECT name, surname, age FROM students 
WHERE phone IS NULL 
ORDER BY age DESC LIMIT 3;
```

---

## 📌 Natijalarni tekshirish

Har bir vazifani bajarganingizdan soʼng, natijalarni tekshiring:

1. **ORDER BY** — natijalar toʼgʼri tartiblanganmi?
2. **LIMIT** — kerakli son qaytarilganmi?
3. **OFFSET** — toʼgʼri sahifa koʼrsatilganmi?
4. **Murakkab soʼrovlar** — barcha shartlar bajarilganmi?

---

## 📌 Keyingi darsga tayyorgarlik

Keyingi darsda quyidagilarni oʼrganamiz:
- Aggregate funksiyalar (COUNT, SUM, AVG, MAX, MIN)
- GROUP BY operatori
- HAVING operatori
- Maʼlumotlarni guruhlash va hisoblash 