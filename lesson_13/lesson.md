# 📖 Lesson 13 — ORDER BY, LIMIT, OFFSET va natijalarni tartiblash

## 🎯 Maqsad
PostgreSQLʼda soʼrov natijalarini tartiblash, cheklash va sahifalash (pagination) usullarini oʼrganish.

---

## 📖 Nazariya

Bu operatorlar soʼrov natijalarini boshqarishda juda muhim hisoblanadi:

- **ORDER BY** — natijalarni tartiblash
- **LIMIT** — natijalar sonini cheklash
- **OFFSET** — natijalarni oʼtkazib yuborish (sahifalash uchun)

---

## 🔷 ORDER BY operatori

### 📋 Asosiy sintaksis
```sql
SELECT ustun1, ustun2 FROM jadval ORDER BY ustun1;
SELECT * FROM jadval ORDER BY ustun1 ASC;  -- oʼsish tartibida
SELECT * FROM jadval ORDER BY ustun1 DESC; -- kamayish tartibida
```

### 📋 Misollar
```sql
-- Oʼquvchilarni yosh boʼyicha tartiblash (kattadan kichikka)
SELECT name, surname, age FROM students ORDER BY age DESC;

-- Mahsulotlarni narx boʼyicha tartiblash (arzonidan qimmatga)
SELECT name, price FROM products ORDER BY price ASC;

-- Familiya boʼyicha alfavit tartibida
SELECT name, surname FROM students ORDER BY surname;
```

### 📋 Bir nechta ustun boʼyicha tartiblash
```sql
-- Avval familiya, keyin ism boʼyicha
SELECT name, surname, age FROM students 
ORDER BY surname ASC, name ASC;

-- Avval ball, keyin yosh boʼyicha (kamayish tartibida)
SELECT name, surname, grade, age FROM students 
ORDER BY grade DESC, age DESC;
```

---

## 🔷 LIMIT operatori

### 📋 Asosiy sintaksis
```sql
SELECT * FROM jadval LIMIT son;
SELECT * FROM jadval ORDER BY ustun LIMIT son;
```

### 📋 Misollar
```sql
-- Faqat 5 ta oʼquvchi
SELECT name, surname FROM students LIMIT 5;

-- Eng yuqori balli 3 ta oʼquvchi
SELECT name, surname, grade FROM students 
ORDER BY grade DESC LIMIT 3;

-- Eng qimmat 5 ta mahsulot
SELECT name, price FROM products 
ORDER BY price DESC LIMIT 5;
```

---

## 🔷 OFFSET operatori

### 📋 Asosiy sintaksis
```sql
SELECT * FROM jadval LIMIT son OFFSET oʼtkazib_yuborilgan_son;
```

### 📋 Misollar
```sql
-- 1-5 oʼquvchilar (birinchi sahifa)
SELECT name, surname FROM students ORDER BY name LIMIT 5 OFFSET 0;

-- 6-10 oʼquvchilar (ikkinchi sahifa)
SELECT name, surname FROM students ORDER BY name LIMIT 5 OFFSET 5;

-- 11-15 oʼquvchilar (uchinchi sahifa)
SELECT name, surname FROM students ORDER BY name LIMIT 5 OFFSET 10;
```

---

## 🔷 Sahifalash (Pagination) formulasi

```sql
-- Sahifa raqami = n, har sahifada = m ta yozuv
SELECT * FROM jadval 
ORDER BY ustun 
LIMIT m OFFSET (n-1) * m;
```

**Misol:** Har sahifada 10 ta yozuv, 3-sahifa uchun:
```sql
SELECT * FROM students 
ORDER BY name 
LIMIT 10 OFFSET 20;  -- (3-1) * 10 = 20
```

---

## 🔷 Murakkab misollar

### 📋 Eng yaxshi oʼquvchilar
```sql
-- Eng yuqori balli 5 ta oʼquvchi, yosh boʼyicha tartiblangan
SELECT name, surname, grade, age FROM students 
WHERE grade = 'A' 
ORDER BY age ASC 
LIMIT 5;
```

### 📋 Mahsulotlar sahifalash
```sql
-- Narxi 500000 dan yuqori mahsulotlar, 2-sahifa
SELECT name, price, brand FROM products 
WHERE price > 500000 
ORDER BY price DESC 
LIMIT 10 OFFSET 10;
```

### 📋 Shahar boʼyicha guruhlash va tartiblash
```sql
-- Har shahardan eng yaxshi oʼquvchi
SELECT DISTINCT ON (city) name, surname, city, grade 
FROM students 
ORDER BY city, grade DESC;
```

---

## 🔷 Amaliy maslahatlar

### 📋 Tartiblash qoidalari:
- **ASC** — oʼsish tartibida (default)
- **DESC** — kamayish tartibida
- Bir nechta ustun boʼyicha tartiblashda har bir ustun uchun tartib belgilash mumkin

### 📋 LIMIT va OFFSET:
- **LIMIT** har doim **ORDER BY** bilan ishlatilishi tavsiya etiladi
- **OFFSET** katta maʼlumotlar bazalarida sekin ishlashi mumkin
- Sahifalash uchun **OFFSET** oʼrniga **cursor-based pagination** ishlatish mumkin

### 📋 Samaradorlik:
- Tartiblash uchun indekslar yaratish
- Katta maʼlumotlar uchun cheklovlar qoʼyish
- Keraksiz ustunlarni tanlamaslik

---

## 📌 Eng koʼp ishlatiladigan operatorlar
✅ `ORDER BY` — natijalarni tartiblash  
✅ `LIMIT` — natijalar sonini cheklash  
✅ `OFFSET` — natijalarni oʼtkazib yuborish  
✅ `ASC/DESC` — tartiblash yoʼnalishi  
✅ `DISTINCT ON` — noyob qiymatlar  

---

## 📌 Keyingi dars:
[Lesson 14 — Aggregate funksiyalar (COUNT, SUM, AVG, MAX, MIN)](../lesson_14/lesson.md) 