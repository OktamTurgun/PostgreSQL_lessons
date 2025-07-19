# 📖 Lesson 12 — LIKE, ILIKE, BETWEEN, IN, IS NULL operatorlari

## 🎯 Maqsad
PostgreSQLʼda qoʼshimcha operatorlar yordamida yanada aniq va samarali soʼrovlar tuzishni oʼrganish.

---

## 📖 Nazariya

Bu operatorlar maʼlumotlarni qidirish va filtrlashda juda foydali hisoblanadi:

- **LIKE** — matnlar bilan ishlashda pattern matching
- **ILIKE** — katta-kichik harflarni hisobga olmagan holda pattern matching
- **BETWEEN** — maʼlum oralikdagi qiymatlarni qidirish
- **IN** — roʼyxatdagi qiymatlardan birini topish
- **IS NULL** — boʼsh qiymatlarni qidirish

---

## 🔷 Sintaksis va asosiy misollar

### 📋 LIKE operatori
```sql
-- "john" bilan boshlanadigan ismlar
SELECT * FROM students WHERE name LIKE 'john%';

-- "son" bilan tugaydigan familiyalar
SELECT * FROM students WHERE surname LIKE '%son';

-- "an" harflarini oʼz ichiga olgan ismlar
SELECT * FROM students WHERE name LIKE '%an%';
```

**Izoh:** `%` har qanday belgilar sonini bildiradi, `_` esa bitta belgini.

### 📋 ILIKE operatori
```sql
-- Katta-kichik harflarni hisobga olmagan holda
SELECT * FROM students WHERE name ILIKE 'JOHN%';
SELECT * FROM students WHERE surname ILIKE '%SMITH';
```

### 📋 BETWEEN operatori
```sql
-- Yosh oraligʼi
SELECT * FROM students WHERE age BETWEEN 18 AND 25;

-- Narx oraligʼi
SELECT * FROM products WHERE price BETWEEN 100 AND 500;

-- Sana oraligʼi
SELECT * FROM orders WHERE order_date BETWEEN '2023-01-01' AND '2023-12-31';
```

### 📋 IN operatori
```sql
-- Maʼlum ballar
SELECT * FROM students WHERE grade IN ('A', 'B', 'C');

-- Maʼlum ID lar
SELECT * FROM products WHERE category_id IN (1, 3, 5);

-- Maʼlum shaharlar
SELECT * FROM customers WHERE city IN ('Tashkent', 'Samarkand', 'Bukhara');
```

### 📋 IS NULL operatori
```sql
-- Telefon raqami yoʼq mijozlar
SELECT * FROM customers WHERE phone IS NULL;

-- Email manzili yoʼq foydalanuvchilar
SELECT * FROM users WHERE email IS NULL;

-- Boʼsh qiymatli yozuvlar
SELECT * FROM orders WHERE delivery_date IS NULL;
```

---

## 🔷 Bir nechta operatorlarni birlashtirish

```sql
-- Maktab oʼquvchilari, 15-18 yosh oraligʼida, A yoki B balli
SELECT * FROM students 
WHERE age BETWEEN 15 AND 18 
AND grade IN ('A', 'B')
AND name LIKE 'A%';

-- Tashkentlik mijozlar, telefon raqami yoʼq
SELECT * FROM customers 
WHERE city = 'Tashkent' 
AND phone IS NULL;

-- Narxi 100-1000 oraligʼida, "phone" soʼzini oʼz ichiga olgan mahsulotlar
SELECT * FROM products 
WHERE price BETWEEN 100 AND 1000 
AND name ILIKE '%phone%';
```

---

## 🔷 Pattern matching uchun maxsus belgilar

| Belgilar | Maʼnosi | Misol |
|----------|---------|-------|
| `%` | Har qanday belgilar soni | `'john%'` - john bilan boshlanadi |
| `_` | Bitta belgi | `'j_n'` - j va n orasida bitta harf |
| `[abc]` | a, b yoki c harflaridan biri | `'j[aeiou]n'` - j va n orasida unli harf |

---

## 🔷 Amaliy maslahatlar
- LIKE va ILIKE da `%` va `_` belgilaridan foydalaning
- BETWEEN da chegaralar kiritilgan
- IN da roʼyxatdagi qiymatlar aniq koʼrsatilishi kerak
- IS NULL va IS NOT NULL ni toʼgʼri ishlatish
- Pattern matching da katta-kichik harflarni hisobga oling

---

## 📌 Eng koʼp ishlatiladigan operatorlar
✅ `LIKE` — matn pattern matching  
✅ `ILIKE` — katta-kichik harflarni hisobga olmagan pattern matching  
✅ `BETWEEN` — oralikdagi qiymatlarni qidirish  
✅ `IN` — roʼyxatdagi qiymatlardan birini topish  
✅ `IS NULL` — boʼsh qiymatlarni qidirish  

---

## 📌 Keyingi dars:
[Lesson 13 — ORDER BY, LIMIT, OFFSET](../lesson_13/lesson.md) 