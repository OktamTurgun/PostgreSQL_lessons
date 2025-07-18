# 📖 Lesson 09 — SELECTga kirish (Intro to SELECT)

## 🎯 Maqsad
PostgreSQLʼda SELECT buyrugʼining asosiy sintaksisi va undan foydalanishni oʼrganish.

---

## 📖 Nazariya

SELECT buyrugʼi — maʼlumotlar bazasidan maʼlumotlarni oʼqish va koʼrish uchun eng muhim buyruqdir.

**SELECT buyrugʼi yordamida:**
- Jadvaldagi barcha yoki kerakli ustunlarni koʼrish
- Maʼlumotlarni filtrlash va tartiblash
- Natijani cheklash va tahlil qilish

---

## 🔷 SELECT buyrugʼining asosiy sintaksisi

```sql
SELECT ustun1, ustun2, ...
FROM jadval_nomi;
```

**Qismlar:**
- `SELECT` — qaysi ustunlarni olish
- `FROM` — qaysi jadvaldan olish

---

## 🔷 SELECT buyrugʼining asosiy usullari

### 📋 1. Barcha ustunlarni olish
```sql
SELECT * FROM students;
```

### 📋 2. Faqat kerakli ustunlarni olish
```sql
SELECT name, age FROM students;
```

### 📋 3. Ustunlarga nom berish (AS)
```sql
SELECT name AS talaba_ismi, age AS yosh FROM students;
```

---

## 🔷 Maʼlumotlarni filtrlash: WHERE

```sql
SELECT * FROM students WHERE age > 20;
SELECT * FROM students WHERE grade = 'A';
```

---

## 🔷 Maʼlumotlarni tartiblash: ORDER BY

```sql
SELECT * FROM students ORDER BY age;
SELECT name, grade FROM students ORDER BY grade DESC;
```

---

## 🔷 Natijani cheklash: LIMIT

```sql
SELECT * FROM students LIMIT 3;
```

---

## 🔷 Amaliy maslahatlar
- Faqat kerakli ustunlarni tanlang (`SELECT *` oʼrniga aniq ustunlar)
- WHERE bilan natijani qisqartiring
- ORDER BY va LIMIT bilan natijani tartiblang va cheklang

---

## 📌 Eng koʼp ishlatiladigan SELECT usullari
✅ **Barcha maʼlumotlar** — `SELECT * FROM table`  
✅ **Filtrlash** — `SELECT ... WHERE ...`  
✅ **Tartiblash** — `SELECT ... ORDER BY ...`  
✅ **Cheklash** — `SELECT ... LIMIT ...`

---

## 📌 Keyingi dars:
[Lesson 10 — WHERE va filtratsiya](../lesson_10/lesson.md) 