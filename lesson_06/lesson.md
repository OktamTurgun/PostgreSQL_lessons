# 📖 Lesson 06 — Foydali buyruqlar

## 🎯 Maqsad
PostgreSQLʼda eng koʼp ishlatiladigan foydali buyruqlar bilan tanishish va ularni amalda qoʼllashni oʼrganish.

---

## 📖 Nazariya

PostgreSQLʼda maʼlumotlar bazasi bilan ishlashda koʼp foydali buyruqlar mavjud.  
Bu buyruqlar maʼlumotlar bazasi tuzilmasi, maʼlumotlar va soʼrovlar bilan ishlashda yordam beradi.

---

## 🔷 Asosiy foydali buyruqlar

### 📋 Maʼlumotlar bazasi bilan ishlash

#### `\l` — Bazalar roʼyxatini koʼrish
```sql
\l
```
**Natija:** Barcha maʼlumotlar bazalari roʼyxati

#### `\c database_name` — Bazaga ulanish
```sql
\c my_database
```
**Natija:** Belgilangan bazaga ulanish

#### `\dt` — Jadvallar roʼyxatini koʼrish
```sql
\dt
```
**Natija:** Hozirgi bazadagi barcha jadvallar

#### `\d table_name` — Jadval tuzilmasini koʼrish
```sql
\d users
```
**Natija:** Jadval ustunlari, turlari va qoʼshimcha maʼlumotlar

---

### 📋 Soʼrovlar bilan ishlash

#### `SELECT` — Maʼlumotlarni olish
```sql
-- Barcha maʼlumotlarni olish
SELECT * FROM users;

-- Belgilangan ustunlarni olish
SELECT name, age FROM users;

-- Shartli soʼrov
SELECT * FROM users WHERE age > 25;
```

#### `INSERT` — Yangi maʼlumot qoʼshish
```sql
-- Bitta yozuv qoʼshish
INSERT INTO users (name, age) VALUES ('Ali', 25);

-- Bir nechta yozuv qoʼshish
INSERT INTO users (name, age) VALUES 
('Vali', 30),
('Gulbahor', 28);
```

#### `UPDATE` — Maʼlumotni yangilash
```sql
-- Barcha yozuvlarni yangilash
UPDATE users SET age = age + 1;

-- Shartli yangilash
UPDATE users SET age = 26 WHERE name = 'Ali';
```

#### `DELETE` — Maʼlumotni oʼchirish
```sql
-- Barcha yozuvlarni oʼchirish
DELETE FROM users;

-- Shartli oʼchirish
DELETE FROM users WHERE age < 18;
```

---

### 📋 Jadval bilan ishlash

#### `CREATE TABLE` — Jadval yaratish
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    age INTEGER,
    email VARCHAR(255)
);
```

#### `ALTER TABLE` — Jadvalni oʼzgartirish
```sql
-- Ustun qoʼshish
ALTER TABLE users ADD COLUMN phone VARCHAR(20);

-- Ustun nomini oʼzgartirish
ALTER TABLE users RENAME COLUMN name TO full_name;

-- Ustunni oʼchirish
ALTER TABLE users DROP COLUMN phone;
```

#### `DROP TABLE` — Jadvalni oʼchirish
```sql
DROP TABLE users;
```

---

### 📋 Maʼlumotlar bazasi bilan ishlash

#### `CREATE DATABASE` — Baza yaratish
```sql
CREATE DATABASE my_database;
```

#### `DROP DATABASE` — Bazani oʼchirish
```sql
DROP DATABASE my_database;
```

---

### 📋 Foydali psql buyruqlari

#### `\?` — Yordam
```sql
\?
```
**Natija:** Barcha mavjud buyruqlar roʼyxati

#### `\h` — SQL buyruqlari yordami
```sql
\h SELECT
```
**Natija:** SELECT buyrugʼi haqida batafsil maʼlumot

#### `\q` — Chiqish
```sql
\q
```
**Natija:** psqlʼdan chiqish

#### `\timing` — Vaqtni koʼrsatish
```sql
\timing
```
**Natija:** Soʼrovlar bajarilish vaqtini koʼrsatadi

---

### 📋 Maʼlumotlarni koʼrish buyruqlari

#### `\du` — Foydalanuvchilar roʼyxati
```sql
\du
```
**Natija:** Barcha foydalanuvchilar va ularning huquqlari

#### `\df` — Funksiyalar roʼyxati
```sql
\df
```
**Natija:** Maʼlumotlar bazasidagi funksiyalar

#### `\dv` — Koʼrinishlar (views) roʼyxati
```sql
\dv
```
**Natija:** Maʼlumotlar bazasidagi koʼrinishlar

---

### 📋 Natijalarni formatlash

#### `\x` — Kengaytirilgan koʼrinish
```sql
\x
SELECT * FROM users LIMIT 1;
```
**Natija:** Har bir ustun alohida qator koʼrinishida

#### `\pset` — Natija formatini oʼzgartirish
```sql
\pset border 2
\pset format expanded
```

---

## 📌 Eng koʼp ishlatiladigan buyruqlar
✅ **Maʼlumotlarni koʼrish** — `SELECT`, `\dt`, `\d`  
✅ **Maʼlumot qoʼshish** — `INSERT`  
✅ **Maʼlumot yangilash** — `UPDATE`  
✅ **Maʼlumot oʼchirish** — `DELETE`  
✅ **Jadval yaratish** — `CREATE TABLE`  
✅ **Bazaga ulanish** — `\c`  
✅ **Yordam olish** — `\?`, `\h`

---

## 📌 Keyingi dars:
[Lesson 07 — WHERE va FILTERING](../lesson_07/lesson.md) 