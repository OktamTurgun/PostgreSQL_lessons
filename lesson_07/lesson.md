# 📖 Lesson 07 — Maʼlumotlarni kiritish

## 🎯 Maqsad
PostgreSQLʼda maʼlumotlarni jadvalga kiritishning turli usullarini oʼrganish va INSERT buyrugʼini samarali qoʼllashni oʼrganish.

---

## 📖 Nazariya

Maʼlumotlarni kiritish — bu maʼlumotlar bazasining asosiy amallaridan biri.  
PostgreSQLʼda maʼlumotlarni kiritish uchun `INSERT` buyrugʼi ishlatiladi.

**INSERT buyrugʼi nima uchun muhim?**
- Yangi maʼlumotlarni saqlash
- Maʼlumotlar bazasini boyitish
- Dastur maʼlumotlarini yuklash
- Test maʼlumotlarini yaratish

---

## 🔷 INSERT buyrugʼining tuzilishi

### 📋 Asosiy sintaksis
```sql
INSERT INTO table_name (column1, column2, ...) 
VALUES (value1, value2, ...);
```

**Qismlar:**
- `INSERT INTO` — buyruq boshlanishi
- `table_name` — jadval nomi
- `(column1, column2, ...)` — ustunlar roʼyxati
- `VALUES` — qiymatlar kaliti
- `(value1, value2, ...)` — kiritiladigan qiymatlar

---

## 🔷 INSERT buyrugʼining turli usullari

### 📋 1. Bitta yozuv kiritish
```sql
-- Barcha ustunlar uchun
INSERT INTO users (id, name, age, email) 
VALUES (1, 'Ali', 25, 'ali@example.com');

-- Faqat kerakli ustunlar uchun
INSERT INTO users (name, age) 
VALUES ('Vali', 30);
```

### 📋 2. Bir nechta yozuv kiritish
```sql
-- Bir qator ichida
INSERT INTO users (name, age, email) VALUES 
('Ali', 25, 'ali@example.com'),
('Vali', 30, 'vali@example.com'),
('Gulbahor', 28, 'gulbahor@example.com');
```

### 📋 3. Qiymatlarni alohida qatorlarda
```sql
INSERT INTO users (name, age, email) VALUES 
('Ali', 25, 'ali@example.com'),
('Vali', 30, 'vali@example.com'),
('Gulbahor', 28, 'gulbahor@example.com');
```

---

## 🔷 Maxsus holatlar

### 📋 SERIAL ustunlar bilan
```sql
-- SERIAL ustun avtomatik to'ldiriladi
INSERT INTO users (name, age) VALUES ('Ali', 25);

-- SERIAL ustunni qo'lda belgilash (kam ishlatiladi)
INSERT INTO users (id, name, age) VALUES (10, 'Vali', 30);
```

### 📋 NULL qiymatlar bilan
```sql
-- NULL qiymat kiritish
INSERT INTO users (name, age, email) VALUES ('Ali', 25, NULL);

-- Ustunni tashlab qoldirish (NULL bo'ladi)
INSERT INTO users (name, age) VALUES ('Vali', 30);
```

### 📋 DEFAULT qiymatlar bilan
```sql
-- DEFAULT qiymatdan foydalanish
INSERT INTO users (name) VALUES ('Ali');

-- DEFAULT kalit so'zi bilan
INSERT INTO users (name, age, email) VALUES ('Vali', DEFAULT, 'vali@example.com');
```

---

## 🔷 INSERT + SELECT (INSERT ... SELECT)

### 📋 Boshqa jadvaldan maʼlumot kiritish
```sql
-- Barcha maʼlumotlarni kiritish
INSERT INTO new_users (name, age)
SELECT name, age FROM old_users;

-- Shartli maʼlumot kiritish
INSERT INTO active_users (name, age)
SELECT name, age FROM users WHERE status = 'active';
```

### 📋 Natijani yangi jadvalga saqlash
```sql
-- CREATE TABLE ... AS SELECT
CREATE TABLE user_backup AS 
SELECT * FROM users WHERE created_date > '2024-01-01';
```

---

## 🔷 Xatolarni oldini olish

### 📋 NOT NULL cheklovlari
```sql
-- NOT NULL ustunni tashlab qoldirish xatolik beradi
INSERT INTO users (name, age) VALUES ('Ali'); -- XATO!

-- Toʼgʼri: barcha NOT NULL ustunlarni toʼldirish
INSERT INTO users (name, age, email) VALUES ('Ali', 25, 'ali@example.com');
```

### 📋 UNIQUE cheklovlari
```sql
-- Bir xil qiymatni qayta kiritish xatolik beradi
INSERT INTO users (email, name) VALUES ('ali@example.com', 'Ali');
INSERT INTO users (email, name) VALUES ('ali@example.com', 'Vali'); -- XATO!
```

### 📋 PRIMARY KEY cheklovlari
```sql
-- Bir xil ID ni qayta kiritish xatolik beradi
INSERT INTO users (id, name) VALUES (1, 'Ali');
INSERT INTO users (id, name) VALUES (1, 'Vali'); -- XATO!
```

---

## 🔷 INSERT natijasini koʼrish

### 📋 RETURNING kalit soʼzi
```sql
-- Kiritilgan yozuvni qaytarish
INSERT INTO users (name, age) VALUES ('Ali', 25)
RETURNING id, name, age;

-- Faqat ID ni qaytarish
INSERT INTO users (name, age) VALUES ('Vali', 30)
RETURNING id;
```

### 📋 Bir nechta yozuv kiritish natijasi
```sql
INSERT INTO users (name, age) VALUES 
('Ali', 25),
('Vali', 30),
('Gulbahor', 28)
RETURNING id, name;
```

---

## 🔷 Amaliy maslahatlar

### 📋 Tezlik uchun
✅ **Bir nechta yozuvni bir vaqtda kiritish** — koʼp INSERT oʼrniga bitta INSERT  
✅ **Kerakli ustunlarni koʼrsatish** — * oʼrniga aniq ustunlar  
✅ **BATCH INSERT** — katta hajmdagi maʼlumotlar uchun

### 📋 Xavfsizlik uchun
✅ **Maʼlumotlarni tekshirish** — kiritishdan oldin  
✅ **Xatolarni qayta ishlash** — try-catch bloklari  
✅ **Tranzaksiyalardan foydalanish** — katta oʼzgarishlar uchun

### 📋 Samaradorlik uchun
✅ **Indekslardan foydalanish** — tez qidiruv uchun  
✅ **Maʼlumotlar hajmini nazarda tutish** — xotira uchun  
✅ **Muntazam tozalash** — eski maʼlumotlarni oʼchirish

---

## 📌 Eng koʼp ishlatiladigan INSERT usullari
✅ **Bitta yozuv** — `INSERT INTO table (col1, col2) VALUES (val1, val2)`  
✅ **Bir nechta yozuv** — `INSERT INTO table (col1, col2) VALUES (val1, val2), (val3, val4)`  
✅ **Boshqa jadvaldan** — `INSERT INTO table1 SELECT * FROM table2`  
✅ **Natijani koʼrish** — `INSERT INTO table VALUES (...) RETURNING *`

---

## 📌 Keyingi dars:
[Lesson 08 — NULL va DEAFAULT qiymatlar](../lesson_08/lesson.md) 