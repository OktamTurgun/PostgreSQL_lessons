# 📖 Lesson 16 — DELETE operatori: Ma'lumotlarni o'chirish

## 🎯 Maqsad
PostgreSQLʼda maʼlumotlarni xavfsiz va to‘g‘ri o‘chirishni o‘rganish, DELETE operatorining imkoniyatlari va amaliyotini tushunish.

---

## 📖 Nazariya

DELETE operatori jadvaldan maʼlumotlarni o‘chirish uchun ishlatiladi. O‘chirishda ehtiyot bo‘lish kerak, chunki o‘chirilgan maʼlumotlarni qayta tiklash qiyin.

---

## 🔷 DELETE operatorining asosiy sintaksisi

```sql
DELETE FROM jadval_nomi WHERE shart;
```

- **WHERE** sharti ko‘rsatilmasa, jadvaldagi barcha yozuvlar o‘chiriladi!

---

## 📋 Misollar

### 1. Bitta yozuvni o‘chirish
```sql
-- ID si 5 bo‘lgan o‘quvchini o‘chirish
DELETE FROM students WHERE id = 5;
```

### 2. Bir nechta yozuvlarni o‘chirish
```sql
-- Tashkent shahridagi barcha o‘quvchilarni o‘chirish
DELETE FROM students WHERE city = 'Tashkent';
```

### 3. Barcha yozuvlarni o‘chirish (EHTIYOT BO‘LING!)
```sql
-- Jadvaldagi barcha o‘quvchilarni o‘chirish
DELETE FROM students;
```

---

## 🔷 DELETE va boshqa operatorlar

### 1. LIMIT bilan o‘chirish (faqat PostgreSQL 13+)
```sql
-- Faqat 3 ta yozuvni o‘chirish
DELETE FROM students WHERE city = 'Samarkand' LIMIT 3;
```

### 2. RETURNING bilan o‘chirilgan maʼlumotlarni ko‘rish
```sql
-- O‘chirilgan o‘quvchilar ismini qaytarish
DELETE FROM students WHERE grade = 'C' RETURNING name, surname;
```

---

## 🔷 DELETE va FOREIGN KEY

Agar jadvalda FOREIGN KEY mavjud bo‘lsa, bog‘liq yozuvlarni o‘chirishda xatolik chiqishi mumkin. Bunday holatda:
- ON DELETE CASCADE — bog‘liq yozuvlar ham o‘chiriladi
- ON DELETE SET NULL — bog‘liq ustunlar NULL bo‘ladi

---

## 🔷 DELETE operatori bilan ehtiyot choralari
- Har doim **WHERE** shartini yozing
- Avval **SELECT** bilan tekshirib ko‘ring
- Katta hajmdagi o‘chirishlarda tranzaksiyadan foydalaning (BEGIN ... COMMIT)
- O‘chirishdan oldin maʼlumotlarni zaxiralash (backup) tavsiya etiladi

---

## 🔷 Tranzaksiya bilan o‘chirish
```sql
BEGIN;
DELETE FROM students WHERE city = 'Bukhara';
-- Tekshirib ko‘ring
ROLLBACK; -- yoki COMMIT;
```

---

## 📌 Amaliy maslahatlar
- **DELETE** — maʼlumotlarni o‘chirish uchun asosiy operator
- **WHERE** — faqat kerakli yozuvlarni o‘chirish uchun
- **RETURNING** — o‘chirilgan yozuvlarni ko‘rish uchun
- **Tranzaksiya** — xavfsiz o‘chirish uchun
- **FOREIGN KEY** — bog‘liq jadvallarni hisobga olish

---

## 📌 Keyingi dars:
[Lesson 17 — UPDATE operatori: Ma'lumotlarni yangilash](../lesson_17/lesson.md) 