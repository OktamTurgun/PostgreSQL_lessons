# 📖 Lesson 15 — JOIN operatorlari va jadvallarni birlashtirish

## 🎯 Maqsad
PostgreSQLʼda turli jadvallardan maʼlumotlarni birlashtirish va olish uchun JOIN operatorlarini oʼrganish.

---

## 📖 Nazariya

JOIN operatorlari bir nechta jadvallardan maʼlumotlarni birlashtirish uchun ishlatiladi:

- **INNER JOIN** — faqat mos keladigan yozuvlarni qaytaradi
- **LEFT JOIN** — chap jadvaldagi barcha yozuvlarni qaytaradi
- **RIGHT JOIN** — oʼng jadvaldagi barcha yozuvlarni qaytaradi
- **FULL JOIN** — ikkala jadvaldagi barcha yozuvlarni qaytaradi

---

## 🔷 INNER JOIN

### 📋 Asosiy sintaksis
```sql
SELECT ustunlar 
FROM jadval1 
INNER JOIN jadval2 ON jadval1.ustun = jadval2.ustun;
```

### 📋 Misollar
```sql
-- Oʼquvchilar va ularning buyurtmalari
SELECT s.name, s.surname, o.order_date, o.total_amount
FROM students s
INNER JOIN orders o ON s.id = o.student_id;

-- Mahsulotlar va ularning buyurtmalari
SELECT p.name, p.brand, o.quantity, o.total_amount
FROM products p
INNER JOIN orders o ON p.id = o.product_id;

-- Oʼquvchilar, mahsulotlar va buyurtmalar
SELECT s.name, p.name as mahsulot, o.total_amount
FROM students s
INNER JOIN orders o ON s.id = o.student_id
INNER JOIN products p ON o.product_id = p.id;
```

---

## 🔷 LEFT JOIN

### 📋 Asosiy sintaksis
```sql
SELECT ustunlar 
FROM jadval1 
LEFT JOIN jadval2 ON jadval1.ustun = jadval2.ustun;
```

### 📋 Misollar
```sql
-- Barcha oʼquvchilar va ularning buyurtmalari (buyurtmasi yoʼq boʼlsa ham)
SELECT s.name, s.surname, o.order_date, o.total_amount
FROM students s
LEFT JOIN orders o ON s.id = o.student_id;

-- Barcha mahsulotlar va ularning sotilish maʼlumotlari
SELECT p.name, p.brand, COUNT(o.id) as sotilgan_soni
FROM products p
LEFT JOIN orders o ON p.id = o.product_id
GROUP BY p.id, p.name, p.brand;

-- Oʼquvchilar va ularning buyurtmalari (NULL boʼlsa ham)
SELECT s.name, s.surname, 
       CASE WHEN o.id IS NULL THEN 'Buyurtma yoʼq' 
            ELSE 'Buyurtma bor' END as holat
FROM students s
LEFT JOIN orders o ON s.id = o.student_id;
```

---

## 🔷 RIGHT JOIN

### 📋 Asosiy sintaksis
```sql
SELECT ustunlar 
FROM jadval1 
RIGHT JOIN jadval2 ON jadval1.ustun = jadval2.ustun;
```

### 📋 Misollar
```sql
-- Barcha buyurtmalar va ularning oʼquvchilari
SELECT o.order_date, o.total_amount, s.name, s.surname
FROM students s
RIGHT JOIN orders o ON s.id = o.student_id;

-- Barcha buyurtmalar va mahsulotlar
SELECT o.order_date, p.name, p.brand, o.quantity
FROM products p
RIGHT JOIN orders o ON p.id = o.product_id;
```

---

## 🔷 FULL JOIN

### 📋 Asosiy sintaksis
```sql
SELECT ustunlar 
FROM jadval1 
FULL JOIN jadval2 ON jadval1.ustun = jadval2.ustun;
```

### 📋 Misollar
```sql
-- Barcha oʼquvchilar va barcha buyurtmalar
SELECT s.name, s.surname, o.order_date, o.total_amount
FROM students s
FULL JOIN orders o ON s.id = o.student_id;

-- Barcha mahsulotlar va barcha buyurtmalar
SELECT p.name, p.brand, o.order_date, o.quantity
FROM products p
FULL JOIN orders o ON p.id = o.product_id;
```

---

## 🔷 CROSS JOIN

### 📋 Asosiy sintaksis
```sql
SELECT ustunlar 
FROM jadval1 
CROSS JOIN jadval2;
```

### 📋 Misollar
```sql
-- Barcha oʼquvchilar va barcha mahsulotlar kombinatsiyasi
SELECT s.name, s.surname, p.name as mahsulot, p.price
FROM students s
CROSS JOIN products p;

-- Har bir oʼquvchi uchun har bir kategoriya
SELECT s.name, p.category
FROM students s
CROSS JOIN (SELECT DISTINCT category FROM products) p;
```

---

## 🔷 Murakkab JOIN misollari

### 📋 Bir nechta jadval bilan JOIN
```sql
-- Oʼquvchilar, ularning buyurtmalari va mahsulotlar
SELECT s.name, s.surname, p.name as mahsulot, 
       o.quantity, o.total_amount, o.order_date
FROM students s
INNER JOIN orders o ON s.id = o.student_id
INNER JOIN products p ON o.product_id = p.id
ORDER BY s.name, o.order_date;
```

### 📋 WHERE bilan JOIN
```sql
-- Tashkentlik oʼquvchilar va ularning buyurtmalari
SELECT s.name, s.surname, o.total_amount
FROM students s
LEFT JOIN orders o ON s.id = o.student_id
WHERE s.city = 'Tashkent';
```

### 📋 Aggregate funksiyalar bilan JOIN
```sql
-- Har oʼquvchining buyurtmalari soni va umumiy summa
SELECT s.name, s.surname, 
       COUNT(o.id) as buyurtmalar_soni,
       SUM(o.total_amount) as umumiy_summa
FROM students s
LEFT JOIN orders o ON s.id = o.student_id
GROUP BY s.id, s.name, s.surname
ORDER BY umumiy_summa DESC;
```

---

## 🔷 JOIN turlari taqqoslash

### 📋 INNER JOIN vs LEFT JOIN
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

### 📋 LEFT JOIN vs RIGHT JOIN
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

## 🔷 JOIN shartlari

### 📋 Bir nechta shart bilan JOIN
```sql
-- Oʼquvchilar va ularning 2023-yilgi buyurtmalari
SELECT s.name, s.surname, o.order_date, o.total_amount
FROM students s
INNER JOIN orders o ON s.id = o.student_id 
    AND o.order_date >= '2023-01-01' 
    AND o.order_date <= '2023-12-31';
```

### 📋 Turli xil shartlar bilan JOIN
```sql
-- A balli oʼquvchilar va ularning qimmat buyurtmalari
SELECT s.name, s.surname, o.total_amount
FROM students s
INNER JOIN orders o ON s.id = o.student_id
WHERE s.grade = 'A' AND o.total_amount > 1000000;
```

---

## 🔷 Amaliy maslahatlar

### 📋 JOIN qoidalari:
- **INNER JOIN** — faqat mos keladigan yozuvlar kerak boʼlsa
- **LEFT JOIN** — chap jadvaldagi barcha yozuvlar kerak boʼlsa
- **RIGHT JOIN** — oʼng jadvaldagi barcha yozuvlar kerak boʼlsa
- **FULL JOIN** — ikkala jadvaldagi barcha yozuvlar kerak boʼlsa

### 📋 Samaradorlik:
- JOIN uchun indekslar yaratish
- Keraksiz ustunlarni tanlamaslik
- WHERE bilan oldindan filtrlash
- Katta jadvallar uchun INNER JOIN ishlatish

### 📋 Xatolarni oldini olish:
- JOIN shartlarini toʼgʼri yozish
- NULL qiymatlarni hisobga olish
- Duplikatlarni oldini olish

---

## 📌 Eng koʼp ishlatiladigan JOIN turlari
✅ `INNER JOIN` — mos keladigan yozuvlarni birlashtirish  
✅ `LEFT JOIN` — chap jadvaldagi barcha yozuvlarni qaytarish  
✅ `RIGHT JOIN` — oʼng jadvaldagi barcha yozuvlarni qaytarish  
✅ `FULL JOIN` — ikkala jadvaldagi barcha yozuvlarni qaytarish  
✅ `CROSS JOIN` — barcha kombinatsiyalarni qaytarish  

---

## 📌 Keyingi dars:
[Lesson 16 — Subquery va EXISTS operatori](../lesson_16/lesson.md) 