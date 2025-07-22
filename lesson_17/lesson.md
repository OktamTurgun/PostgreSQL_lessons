# 📖 Lesson 17 — UPDATE operatori: Ma'lumotlarni yangilash

## 🎯 Maqsad
PostgreSQLʼda maʼlumotlarni yangilash, UPDATE operatorining imkoniyatlari va xavfsiz ishlatilishini o‘rganish.

---

## 📖 Nazariya

UPDATE operatori jadvaldagi mavjud yozuvlarni o‘zgartirish uchun ishlatiladi. Ehtiyot bo‘lish kerak, noto‘g‘ri ishlatilsa, barcha yozuvlar o‘zgarib ketishi mumkin.

---

## 🔷 UPDATE operatorining asosiy sintaksisi

```sql
UPDATE jadval_nomi SET ustun1 = qiymat1, ustun2 = qiymat2 WHERE shart;
```

- **WHERE** sharti ko‘rsatilmasa, jadvaldagi barcha yozuvlar yangilanadi!

---

## 📋 Misollar

### 1. Bitta ustunni yangilash
```sql
-- ID si 2 bo‘lgan o‘quvchining yoshini 21 ga o‘zgartirish
UPDATE students SET age = 21 WHERE id = 2;
```

### 2. Bir nechta ustunni yangilash
```sql
-- ID si 4 bo‘lgan o‘quvchining yoshini va ballini o‘zgartirish
UPDATE students SET age = 19, grade = 'B' WHERE id = 4;
```

### 3. Bir nechta yozuvlarni yangilash
```sql
-- Tashkent shahridagi barcha o‘quvchilarning ballini 'A' ga o‘zgartirish
UPDATE students SET grade = 'A' WHERE city = 'Tashkent';
```

### 4. Barcha yozuvlarni yangilash (EHTIYOT BO‘LING!)
```sql
-- Barcha o‘quvchilarning ballini 'C' ga o‘zgartirish
UPDATE students SET grade = 'C';
```

---

## 🔷 UPDATE va boshqa operatorlar

### 1. RETURNING bilan yangilangan maʼlumotlarni ko‘rish
```sql
-- Balli 'B' bo‘lgan o‘quvchilarning ballini 'A' ga o‘zgartirib, ism va familiyasini qaytarish
UPDATE students SET grade = 'A' WHERE grade = 'B' RETURNING name, surname;
```

### 2. Tranzaksiya bilan yangilash
```sql
BEGIN;
UPDATE students SET city = 'Toshkent' WHERE city = 'Samarkand';
-- SELECT * FROM students WHERE city = 'Toshkent';
ROLLBACK; -- yoki COMMIT;
```

---

## 🔷 UPDATE operatori bilan ehtiyot choralari
- Har doim **WHERE** shartini yozing
- Avval **SELECT** bilan tekshirib ko‘ring
- Katta hajmdagi yangilashlarda tranzaksiyadan foydalaning (BEGIN ... COMMIT)
- Yangilashdan oldin maʼlumotlarni zaxiralash (backup) tavsiya etiladi

---

## 📌 Amaliy maslahatlar
- **UPDATE** — maʼlumotlarni yangilash uchun asosiy operator
- **SET** — o‘zgartiriladigan ustun va qiymat
- **WHERE** — faqat kerakli yozuvlarni yangilash uchun
- **RETURNING** — yangilangan yozuvlarni ko‘rish uchun
- **Tranzaksiya** — xavfsiz yangilash uchun

---

## 📌 Keyingi dars:
[Lesson 18 — Jadvallar dizayni](../lesson_18/lesson.md) 