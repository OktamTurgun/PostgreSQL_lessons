# 📝 Amaliyot — Index va samaradorlik optimizatsiyasi

Quyidagi amaliy mashqlarni bajaring. Har bir topshiriq uchun kod va natijani yozing.

---

### 1. Oddiy index yaratish va tekshirish

**Vazifa:**
students jadvalida name ustuni uchun index yaratish va so'rov samaradorligini tekshirish.

**Kod:**
```sql
-- Jadval yaratish
CREATE TABLE students (
    id serial PRIMARY KEY,
    name varchar(100),
    grade char(1),
    age integer
);

-- Ma'lumotlar qo'shish
INSERT INTO students (name, grade, age) VALUES 
('Ali', 'A', 20),
('Vali', 'B', 21),
('Hasan', 'A', 19),
('Zafar', 'C', 22);

-- Index yaratish
CREATE INDEX idx_students_name ON students (name);

-- Samaradorlikni tekshirish
EXPLAIN ANALYZE SELECT * FROM students WHERE name = 'Ali';
```

**Natija:**
```sql
-- Index yaratilgandan keyin so'rov tezroq ishlaydi
-- EXPLAIN ANALYZE natijasida "Index Scan" ko'rinadi
```

---

### 2. Ko'p ustunli index yaratish

**Vazifa:**
name va grade ustunlari uchun birgalikda index yaratish va turli so'rovlarni sinab ko'rish.

**Kod:**
```sql
-- Ko'p ustunli index yaratish
CREATE INDEX idx_students_name_grade ON students (name, grade);

-- Birinchi so'rov (ikkala ustun bilan)
SELECT * FROM students WHERE name = 'Ali' AND grade = 'A';

-- Ikkinchi so'rov (faqat name bilan)
SELECT * FROM students WHERE name = 'Ali';

-- Uchinchi so'rov (faqat grade bilan) - index ishlatmaydi
SELECT * FROM students WHERE grade = 'A';
```

**Natija:**
```sql
-- Birinchi va ikkinchi so'rovlar tez ishlaydi
-- Uchinchi so'rov index ishlatmaydi, chunki grade ikkinchi ustun
```

---

### 3. Partial index yaratish

**Vazifa:**
Faqat A bahosi olgan talabalar uchun partial index yaratish.

**Kod:**
```sql
-- Partial index yaratish
CREATE INDEX idx_students_grade_a ON students (name) 
WHERE grade = 'A';

-- Bu so'rov tez ishlaydi (index ishlatadi)
SELECT * FROM students WHERE name = 'Ali' AND grade = 'A';

-- Bu so'rov index ishlatmaydi
SELECT * FROM students WHERE name = 'Vali' AND grade = 'B';

-- Index ma'lumotlarini ko'rish
SELECT indexname, tablename, indexdef 
FROM pg_indexes 
WHERE tablename = 'students';
```

**Natija:**
```sql
-- Faqat A bahosi olgan talabalar uchun index yaratiladi
-- Index o'lchami kichikroq bo'ladi
```

---

### 4. Unique index va cheklovlar

**Vazifa:**
Email ustuni uchun unique index yaratish va duplicate ma'lumotlarni sinab ko'rish.

**Kod:**
```sql
-- Email ustuni qo'shish
ALTER TABLE students ADD COLUMN email varchar(100);

-- Unique index yaratish
CREATE UNIQUE INDEX idx_students_email ON students (email);

-- Birinchi yozuv (muvaffaqiyatli)
INSERT INTO students (name, email) VALUES ('Ali', 'ali@example.com');

-- Ikkinchi yozuv (xatolik - duplicate email)
INSERT INTO students (name, email) VALUES ('Vali', 'ali@example.com');

-- To'g'ri yozuv
INSERT INTO students (name, email) VALUES ('Vali', 'vali@example.com');
```

**Natija:**
```sql
-- Birinchi yozuv muvaffaqiyatli
-- Ikkinchi yozuv xatolik beradi: "duplicate key value violates unique constraint"
-- Uchinchi yozuv muvaffaqiyatli
```

---

### 5. Index samaradorligini taqqoslash

**Vazifa:**
Indexsiz va index bilan so'rovlarni taqqoslash va natijalarni tahlil qilish.

**Kod:**
```sql
-- Indexsiz so'rov
EXPLAIN ANALYZE SELECT * FROM students WHERE name = 'Ali';

-- Index bilan so'rov
EXPLAIN ANALYZE SELECT * FROM students WHERE name = 'Ali';

-- Index o'lchamini ko'rish
SELECT schemaname, tablename, indexname, 
       pg_size_pretty(pg_relation_size(indexname::regclass)) as size
FROM pg_indexes 
WHERE tablename = 'students';
```

**Natija:**
```sql
-- Indexsiz so'rov: "Seq Scan" (sekuensial qidirish)
-- Index bilan so'rov: "Index Scan" (index orqali qidirish)
-- Index o'lchami ko'rsatiladi
```

---

### 6. Index optimizatsiyasi

**Vazifa:**
Index statistikalarini yangilash va fragmentatsiyani tuzatish.

**Kod:**
```sql
-- Index statistikalarini yangilash
ANALYZE students;

-- Index fragmentatsiyasini tuzatish
REINDEX INDEX idx_students_name;

-- Barcha indexlarni ko'rish
SELECT indexname, tablename, indexdef 
FROM pg_indexes 
WHERE tablename = 'students';
```

**Natija:**
```sql
-- Statistikalar yangilandi
-- Index fragmentatsiyasi tuzatildi
-- Barcha indexlar ro'yxati ko'rsatildi
```

---

**Natijalarni SQL kod va qisqacha izoh bilan yozing.** 