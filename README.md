# 📘 PostgreSQL Lessons

Ushbu repozitoriy — PostgreSQL maʼlumotlar bazasi tizimini o'zbek tilida bosqichma-bosqich o'rganish uchun to'liq darslar to'plami.

## 📚 Tuzilma

Har bir dars alohida papkada joylashgan va ikki qismdan iborat:
- `lesson.md` — Nazariy qism (asosiy tushunchalar, misollar, izohlar)
- `practice.md` — Amaliy mashqlar (mustahkamlash uchun topshiriqlar va kodlar)

## 🚀 Boshlash

1. Repozitoriyani yuklab oling yoki klonlang:
   ```sh
   git clone https://github.com/OktamTurgun/PostgreSQL_lessons.git
   ```
2. Har bir dars papkasiga kirib, `lesson.md` va `practice.md` fayllarini o'qing va amaliyotlarni bajaring.

## 📋 Darslar ro'yxati

- [Lesson 01 — Kirish](lesson_01/lesson_01_kirish.md)  
  *PostgreSQL va maʼlumotlar bazasi tushunchasi bilan tanishuv.*
- [Lesson 02 — Windows'da o'rnatish](lesson_02/lesson.md)  
  *PostgreSQL'ni Windows operatsion tizimiga o'rnatish bo'yicha ko'rsatma.*
- [Lesson 03 — Maʼlumotlar va Jadvallar](lesson_03/lesson.md)  
  *Jadval, ustun, qator, primary key va asosiy SQL buyruqlari bilan tanishuv.*
- [Lesson 04 — Maʼlumotlar bazasini yaratish](lesson_04/lesson.md)  
  *Yangi maʼlumotlar bazasi yaratish va asosiy amallar.*
- [Lesson 05 — Maʼlumot turlari](lesson_05/lesson.md)  
  *PostgreSQL'dagi asosiy maʼlumot turlari va ularni to'g'ri ishlatish.*
- [Lesson 06 — Foydali buyruqlar](lesson_06/lesson.md)  
  *psql va SQL buyruqlari, jadval va baza boshqaruvi.*
- [Lesson 07 — Maʼlumotlarni kiritish (INSERT)](lesson_07/lesson.md)  
  *INSERT operatori va maʼlumot kiritish usullari.*
- [Lesson 08 — NULL va DEFAULT qiymatlar](lesson_08/lesson.md)  
  *NULL va DEFAULT qiymatlar, ularni ishlatish va boshqarish.*
- [Lesson 09 — SELECTga kirish (Intro to SELECT)](lesson_09/lesson.md)  
  *SELECT operatori, ustunlar, WHERE, ORDER BY, LIMIT, filtrlash va tartiblash.*
- [Lesson 10 — WHERE va filtratsiya](lesson_10/lesson.md)  
  *WHERE operatori, shartli so'rovlar va filtrlash.*
- [Lesson 11 — ORDER BY va LIMIT](lesson_11/lesson.md)  
  *Natijalarni tartiblash va cheklash.*
- [Lesson 12 — LIKE, ILIKE, BETWEEN, IN, IS NULL](lesson_12/lesson.md)  
  *Qo'shimcha operatorlar va pattern matching.*
- [Lesson 13 — ORDER BY, LIMIT, OFFSET va natijalarni tartiblash](lesson_13/lesson.md)  
  *So'rov natijalarini tartiblash, cheklash va sahifalash (pagination).* 
- [Lesson 14 — Aggregate funksiyalar va GROUP BY](lesson_14/lesson.md)  
  *COUNT, SUM, AVG, MAX, MIN, GROUP BY, HAVING va statistik so'rovlar.*
- [Lesson 15 — JOIN operatorlari va jadvallarni birlashtirish](lesson_15/lesson.md)  
  *INNER, LEFT, RIGHT, FULL, CROSS JOIN va murakkab birlashtirishlar.*
- [Lesson 16 — DELETE operatori: Ma'lumotlarni o'chirish](lesson_16/lesson.md)  
  *DELETE operatori, xavfsiz o'chirish, CASCADE va ehtiyot choralari.*
- [Lesson 17 — UPDATE operatori: Ma'lumotlarni yangilash](lesson_17/lesson.md)  
  *UPDATE operatori, RETURNING, tranzaksiya va xavfsiz yangilash.*
- [Lesson 18 — Jadvallarni to'g'ri dizayn qilish (mukammal)](lesson_18/lesson.md)  
  *Jadval dizayni, normalizatsiya, relationshiplar, denormalizatsiya, ALTER TABLE, CASCADE, ER-diagram va best practices.*
- [Lesson 19 — Transactionlar va xavfsiz o'zgartirishlar](lesson_19/lesson.md)  
  *Transactionlar (BEGIN, COMMIT, ROLLBACK), isolation levels, xavfsiz o'zgartirishlar va amaliy misollar.*

> **Eslatma:** Har bir darsda amaliy mashqlar uchun `practice.md` fayli mavjud.

## 🎯 O'rganiladigan mavzular

### Asosiy SQL operatorlari
- ✅ SELECT — maʼlumotlarni o'qish
- ✅ INSERT — yangi maʼlumotlar qo'shish  
- ✅ UPDATE — maʼlumotlarni yangilash
- ✅ DELETE — maʼlumotlarni o'chirish

### Filtrlash va qidirish
- ✅ WHERE — shartli so'rovlar
- ✅ Comparison operators — taqqoslash
- ✅ Logical operators — mantiqiy operatorlar
- ✅ Pattern matching — LIKE, ILIKE
- ✅ Range queries — BETWEEN
- ✅ List queries — IN
- ✅ Null handling — IS NULL

## 🤝 Hissa qo'shish

Taklif va tuzatishlar uchun pull request yoki issue qoldirishingiz mumkin.

---

**Loyiha muallifi:**  
[OktamTurgun](https://github.com/OktamTurgun)