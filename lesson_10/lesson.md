# 📖 Lesson 10 — WHERE va filtratsiya

## 🎯 Maqsad
PostgreSQLʼda WHERE buyrugʼi va filtratsiya operatorlari yordamida maʼlumotlarni aniq tanlashni oʼrganish.

---

## 📖 Nazariya

WHERE buyrugʼi — SELECT, UPDATE, DELETE soʼrovlarida maʼlumotlarni filtrlash uchun ishlatiladi.

**WHERE yordamida:**
- Faqat kerakli qatorlarni tanlash
- Shartli soʼrovlar tuzish
- Maʼlumotlarni tahlil qilish va hisobotlar olish

---

## 🔷 WHERE buyrugʼining asosiy sintaksisi

```sql
SELECT ustunlar FROM jadval WHERE shart;
```

---

## 🔷 Solishtirish operatorlari

## 🔷 Asosiy operatorlar va misollar

### 📋 1. Tenglik va teng emas
```sql
SELECT * FROM students WHERE grade = 'A';
SELECT * FROM students WHERE age <> 20;
```

### 📋 2. Katta, kichik, oraliq
```sql
SELECT * FROM students WHERE age > 18;
SELECT * FROM students WHERE age BETWEEN 18 AND 22;
```

### 📋 3. IN va NOT IN
```sql
SELECT * FROM students WHERE grade IN ('A', 'B');
SELECT * FROM students WHERE age NOT IN (18, 19);
```

### 📋 4. LIKE va ILIKE (matn boʼyicha qidirish)
```sql
SELECT * FROM students WHERE name LIKE 'A%';   -- 'A' harfi bilan boshlanadi
SELECT * FROM students WHERE name LIKE '%ov';  -- 'ov' bilan tugaydi
SELECT * FROM students WHERE name ILIKE '%ali%'; -- 'ali' boʼlsa, katta-kichik harf farqsiz
```

### 📋 5. IS NULL va IS NOT NULL
```sql
SELECT * FROM students WHERE email IS NULL;
SELECT * FROM students WHERE phone IS NOT NULL;
```

### 📋 6. Mantiqiy operatorlar (AND, OR, NOT)
```sql
SELECT * FROM students WHERE grade = 'A' AND age > 20;
SELECT * FROM students WHERE grade = 'B' OR age < 20;
SELECT * FROM students WHERE NOT (grade = 'C');
```

---

## 🔷 Amaliy maslahatlar
- WHERE bilan natijani qisqartiring
- Bir nechta shartlarni AND/OR bilan birlashtiring
- LIKE va ILIKE yordamida matn boʼyicha qidiring
- NULL qiymatlarni IS NULL/IS NOT NULL bilan tekshiring
- IN va BETWEEN yordamida koʼp qiymatli shartlar yozing

---

## 📌 Eng koʼp ishlatiladigan WHERE usullari
✅ `WHERE ... = ...`  
✅ `WHERE ... <> ...`  
✅ `WHERE ... > ...`  
✅ `WHERE ... BETWEEN ... AND ...`  
✅ `WHERE ... IN (...)`  
✅ `WHERE ... LIKE ...`  
✅ `WHERE ... IS NULL`  
✅ `WHERE ... AND ...`  
✅ `WHERE ... OR ...`

---

## 📌 Keyingi dars:
[Lesson 11 — ORDER BY va LIMIT](../lesson_11/lesson.md) 