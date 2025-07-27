# 📖 Lesson 25 — Index va samaradorlik optimizatsiyasi

## 🎯 Maqsad
PostgreSQL'da indexlar tushunchasi, ularni yaratish, ishlatish, samaradorlikni oshirish va amaliyotda qo'llashni o'rganish.

---

## 1. Index nazariyasi

### Nazariya
- **Index** — bu ma'lumotlar bazasida so'rovlarni tezlashtirish uchun ishlatiladigan maxsus struktura.
- Indexlar yordamida ma'lumotlarni tez qidirish, tartiblash va filtrlash mumkin.
- Indexlar ma'lumotlarni saqlash uchun qo'shimcha joy talab qiladi va yozish operatsiyalarini sekinlashtiradi.

### Index turlari
| Index turi | Tushuntirish | Qachon ishlatiladi |
|------------|-------------|-------------------|
| **B-tree** | Eng keng tarqalgan, tenglik va diapazon so'rovlar uchun | Har xil turdagi ma'lumotlar |
| **Hash** | Faqat tenglik so'rovlari uchun | INTEGER, TEXT |
| **GiST** | Geometrik ma'lumotlar uchun | POINT, POLYGON |
| **GIN** | Massiv va JSON ma'lumotlar uchun | ARRAY, JSONB |
| **BRIN** | Katta jadvallar uchun | Sekuensial ma'lumotlar |

---

## 2. Index yaratish va asosiy sintaksis

### Sintaksis
#### Oddiy index yaratish:
```sql
CREATE INDEX index_nomi ON jadval_nomi (ustun_nomi);
```

#### Ko'p ustunli index:
```sql
CREATE INDEX index_nomi ON jadval_nomi (ustun1, ustun2);
```

#### Unique index:
```sql
CREATE UNIQUE INDEX index_nomi ON jadval_nomi (ustun_nomi);
```

#### Partial index (qismiy):
```sql
CREATE INDEX index_nomi ON jadval_nomi (ustun_nomi) 
WHERE shart;
```

#### Index o'chirish:
```sql
DROP INDEX index_nomi;
```

---

## 3. Amaliy misollar

### Misol 1: Oddiy index yaratish
**Vazifa:** students jadvalida name ustuni uchun index yaratish.

```sql
-- Jadval yaratish
CREATE TABLE students (
    id serial PRIMARY KEY,
    name varchar(100),
    grade char(1),
    age integer
);

-- Index yaratish
CREATE INDEX idx_students_name ON students (name);

-- So'rov tezlashtiriladi
SELECT * FROM students WHERE name = 'Ali';
```

### Misol 2: Ko'p ustunli index
**Vazifa:** name va grade ustunlari uchun birgalikda index yaratish.

```sql
CREATE INDEX idx_students_name_grade ON students (name, grade);

-- Bu so'rov tez ishlaydi
SELECT * FROM students WHERE name = 'Ali' AND grade = 'A';

-- Bu so'rov ham tez ishlaydi (faqat name bo'yicha)
SELECT * FROM students WHERE name = 'Ali';
```

### Misol 3: Partial index
**Vazifa:** Faqat A bahosi olgan talabalar uchun index yaratish.

```sql
CREATE INDEX idx_students_grade_a ON students (name) 
WHERE grade = 'A';

-- Bu so'rov tez ishlaydi
SELECT * FROM students WHERE name = 'Ali' AND grade = 'A';

-- Bu so'rov index ishlatmaydi
SELECT * FROM students WHERE name = 'Vali' AND grade = 'B';
```

### Misol 4: Unique index
**Vazifa:** Email ustuni uchun unique index yaratish.

```sql
-- Jadvalga email ustuni qo'shish
ALTER TABLE students ADD COLUMN email varchar(100);

-- Unique index yaratish
CREATE UNIQUE INDEX idx_students_email ON students (email);

-- Bu xatolik beradi (duplicate email)
INSERT INTO students (name, email) VALUES ('Ali', 'ali@example.com');
INSERT INTO students (name, email) VALUES ('Vali', 'ali@example.com'); -- Xatolik!
```

---

## 4. Index samaradorligini tekshirish

### EXPLAIN ANALYZE
```sql
-- Indexsiz so'rov
EXPLAIN ANALYZE SELECT * FROM students WHERE name = 'Ali';

-- Index bilan so'rov
CREATE INDEX idx_students_name ON students (name);
EXPLAIN ANALYZE SELECT * FROM students WHERE name = 'Ali';
```

### Index ma'lumotlarini ko'rish
```sql
-- Barcha indexlarni ko'rish
SELECT indexname, tablename, indexdef 
FROM pg_indexes 
WHERE tablename = 'students';

-- Index o'lchamini ko'rish
SELECT schemaname, tablename, indexname, 
       pg_size_pretty(pg_relation_size(indexname::regclass)) as size
FROM pg_indexes 
WHERE tablename = 'students';
```

---

## 5. Best practices va muammolar

### Index yaratish qoidalari:
- **Ko'p ishlatiladigan ustunlar** uchun index yarating
- **WHERE, ORDER BY, JOIN** shartlarida ishlatiladigan ustunlar uchun index yarating
- **Ko'p ustunli indexlarda** ustunlar tartibini to'g'ri belgilang
- **Partial index** yordamida faqat kerakli ma'lumotlar uchun index yarating

### Index muammolari:
- **Haddan tashqari ko'p indexlar** yozish operatsiyalarini sekinlashtiradi
- **Katta indexlar** disk joyini ko'p egallaydi
- **Noto'g'ri indexlar** so'rovlarni sekinlashtiradi

### Indexni optimizatsiya qilish:
```sql
-- Index statistikalarini yangilash
ANALYZE students;

-- Index fragmentatsiyasini tuzatish
REINDEX INDEX idx_students_name;
```

---

## 6. Xulosa
- Indexlar so'rovlarni tezlashtiradi, lekin disk joyini egallaydi
- To'g'ri index tanlash samaradorlikni oshirishda muhim
- EXPLAIN ANALYZE yordamida so'rov samaradorligini tekshirish mumkin
- Indexlarni muntazam monitoring va optimizatsiya qilish kerak

---

## 📌 Keyingi dars:
[Lesson 26 — Backup va restore](lesson_26/lesson.md) 