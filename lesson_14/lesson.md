# 📖 Lesson 14 — Aggregate funksiyalar va GROUP BY

## 🎯 Maqsad
PostgreSQLʼda maʼlumotlarni guruhlash, hisoblash va statistik maʼlumotlarni olish uchun aggregate funksiyalar va GROUP BY operatorini oʼrganish.

---

## 📖 Nazariya

Aggregate funksiyalar maʼlumotlar ustida hisob-kitoblar amalga oshirish uchun ishlatiladi:

- **COUNT()** — yozuvlar sonini hisoblash
- **SUM()** — qiymatlar yigʼindisini hisoblash
- **AVG()** — oʼrtacha qiymatni hisoblash
- **MAX()** — eng katta qiymatni topish
- **MIN()** — eng kichik qiymatni topish

**GROUP BY** — maʼlumotlarni guruhlarga ajratish uchun ishlatiladi.

---

## 🔷 COUNT() funksiyasi

### 📋 Asosiy sintaksis
```sql
SELECT COUNT(*) FROM jadval;
SELECT COUNT(ustun_nomi) FROM jadval;
SELECT COUNT(DISTINCT ustun_nomi) FROM jadval;
```

### 📋 Misollar
```sql
-- Barcha oʼquvchilar soni
SELECT COUNT(*) FROM students;

-- Telefon raqami bor oʼquvchilar soni
SELECT COUNT(phone) FROM students;

-- Har xil shaharlar soni
SELECT COUNT(DISTINCT city) FROM students;

-- A balli oʼquvchilar soni
SELECT COUNT(*) FROM students WHERE grade = 'A';
```

---

## 🔷 SUM() funksiyasi

### 📋 Asosiy sintaksis
```sql
SELECT SUM(ustun_nomi) FROM jadval;
SELECT SUM(ustun_nomi) FROM jadval WHERE shart;
```

### 📋 Misollar
```sql
-- Barcha mahsulotlar narxi yigʼindisi
SELECT SUM(price) FROM products;

-- Apple brendidagi mahsulotlar narxi yigʼindisi
SELECT SUM(price) FROM products WHERE brand = 'Apple';

-- 1000000 dan yuqori mahsulotlar narxi yigʼindisi
SELECT SUM(price) FROM products WHERE price > 1000000;
```

---

## 🔷 AVG() funksiyasi

### 📋 Asosiy sintaksis
```sql
SELECT AVG(ustun_nomi) FROM jadval;
SELECT ROUND(AVG(ustun_nomi), 2) FROM jadval; -- 2 xona aniqlikda
```

### 📋 Misollar
```sql
-- Oʼrtacha yosh
SELECT AVG(age) FROM students;

-- Oʼrtacha yosh (2 xona aniqlikda)
SELECT ROUND(AVG(age), 2) FROM students;

-- Oʼrtacha narx
SELECT ROUND(AVG(price), 2) FROM products;

-- A balli oʼquvchilarning oʼrtacha yoshi
SELECT ROUND(AVG(age), 2) FROM students WHERE grade = 'A';
```

---

## 🔷 MAX() va MIN() funksiyalari

### 📋 Asosiy sintaksis
```sql
SELECT MAX(ustun_nomi) FROM jadval;
SELECT MIN(ustun_nomi) FROM jadval;
```

### 📋 Misollar
```sql
-- Eng katta yosh
SELECT MAX(age) FROM students;

-- Eng kichik yosh
SELECT MIN(age) FROM students;

-- Eng qimmat mahsulot narxi
SELECT MAX(price) FROM products;

-- Eng arzon mahsulot narxi
SELECT MIN(price) FROM products;

-- Eng qimmat va eng arzon mahsulotlar
SELECT MAX(price) as eng_qimmat, MIN(price) as eng_arzon FROM products;
```

---

## 🔷 GROUP BY operatori

### 📋 Asosiy sintaksis
```sql
SELECT ustun1, aggregate_funksiya(ustun2) 
FROM jadval 
GROUP BY ustun1;
```

### 📋 Misollar
```sql
-- Har shahardagi oʼquvchilar soni
SELECT city, COUNT(*) as oquvchilar_soni 
FROM students 
GROUP BY city;

-- Har ball boʼyicha oʼquvchilar soni
SELECT grade, COUNT(*) as soni 
FROM students 
GROUP BY grade;

-- Har brenddagi mahsulotlar soni va oʼrtacha narx
SELECT brand, 
       COUNT(*) as mahsulotlar_soni,
       ROUND(AVG(price), 2) as o_rtacha_narx
FROM products 
GROUP BY brand;
```

---

## 🔷 HAVING operatori

### 📋 Asosiy sintaksis
```sql
SELECT ustun1, aggregate_funksiya(ustun2) 
FROM jadval 
GROUP BY ustun1 
HAVING aggregate_funksiya(ustun2) shart;
```

### 📋 Misollar
```sql
-- 2 tadan koʼp oʼquvchisi bor shaharlar
SELECT city, COUNT(*) as oquvchilar_soni 
FROM students 
GROUP BY city 
HAVING COUNT(*) > 2;

-- Oʼrtacha narxi 1000000 dan yuqori brendlar
SELECT brand, ROUND(AVG(price), 2) as o_rtacha_narx
FROM products 
GROUP BY brand 
HAVING AVG(price) > 1000000;

-- 3 tadan koʼp mahsuloti bor kategoriyalar
SELECT category, COUNT(*) as mahsulotlar_soni
FROM products 
GROUP BY category 
HAVING COUNT(*) > 3;
```

---

## 🔷 Murakkab misollar

### 📋 Har shahardagi statistika
```sql
SELECT city,
       COUNT(*) as oquvchilar_soni,
       ROUND(AVG(age), 2) as o_rtacha_yosh,
       MAX(age) as eng_katta_yosh,
       MIN(age) as eng_kichik_yosh
FROM students 
GROUP BY city;
```

### 📋 Har brenddagi mahsulotlar statistikasi
```sql
SELECT brand,
       COUNT(*) as mahsulotlar_soni,
       ROUND(AVG(price), 2) as o_rtacha_narx,
       MAX(price) as eng_qimmat,
       MIN(price) as eng_arzon,
       SUM(price) as umumiy_narx
FROM products 
GROUP BY brand;
```

### 📋 Har ball boʼyicha statistika
```sql
SELECT grade,
       COUNT(*) as oquvchilar_soni,
       ROUND(AVG(age), 2) as o_rtacha_yosh,
       COUNT(CASE WHEN phone IS NOT NULL THEN 1 END) as telefon_bor
FROM students 
GROUP BY grade;
```

---

## 🔷 WHERE vs HAVING farqi

### 📋 WHERE — guruhlashdan oldin filtrlash
```sql
-- Faqat Tashkentlik oʼquvchilarni guruhlash
SELECT city, COUNT(*) as soni
FROM students 
WHERE city = 'Tashkent'
GROUP BY city;
```

### 📋 HAVING — guruhlashdan keyin filtrlash
```sql
-- 2 tadan koʼp oʼquvchisi bor shaharlar
SELECT city, COUNT(*) as soni
FROM students 
GROUP BY city 
HAVING COUNT(*) > 2;
```

### 📋 WHERE va HAVING birgalikda
```sql
-- Tashkentlik oʼquvchilarni guruhlash, 2 tadan koʼp boʼlsa
SELECT city, COUNT(*) as soni
FROM students 
WHERE city = 'Tashkent'
GROUP BY city 
HAVING COUNT(*) > 2;
```

---

## 🔷 DISTINCT bilan aggregate funksiyalar

### 📋 Misollar
```sql
-- Har xil yoshlar soni
SELECT COUNT(DISTINCT age) FROM students;

-- Har xil narxlar soni
SELECT COUNT(DISTINCT price) FROM products;

-- Har xil brendlar soni
SELECT COUNT(DISTINCT brand) FROM products;
```

---

## 🔷 Amaliy maslahatlar

### 📋 Aggregate funksiyalar qoidalari:
- **COUNT(*)** — barcha yozuvlarni hisoblaydi (NULL ham)
- **COUNT(ustun)** — NULL boʼlmagan qiymatlarni hisoblaydi
- **COUNT(DISTINCT ustun)** — noyob qiymatlarni hisoblaydi
- Aggregate funksiyalar WHERE dan keyin, GROUP BY dan oldin ishlatiladi

### 📋 GROUP BY qoidalari:
- SELECT da aggregate funksiya boʼlmagan ustunlar GROUP BY da boʼlishi kerak
- HAVING faqat aggregate funksiyalar bilan ishlatiladi
- WHERE guruhlashdan oldin, HAVING guruhlashdan keyin ishlatiladi

### 📋 Samaradorlik:
- Katta maʼlumotlar uchun indekslar yaratish
- Keraksiz ustunlarni tanlamaslik
- WHERE bilan oldindan filtrlash

---

## 📌 Eng koʼp ishlatiladigan funksiyalar
✅ `COUNT()` — yozuvlar sonini hisoblash  
✅ `SUM()` — qiymatlar yigʼindisini hisoblash  
✅ `AVG()` — oʼrtacha qiymatni hisoblash  
✅ `MAX()` — eng katta qiymatni topish  
✅ `MIN()` — eng kichik qiymatni topish  
✅ `GROUP BY` — maʼlumotlarni guruhlash  
✅ `HAVING` — guruhlar boʼyicha filtrlash  

---

## 📌 Keyingi dars:
[Lesson 15 — JOIN operatorlari (INNER, LEFT, RIGHT, FULL)](../lesson_15/lesson.md) 