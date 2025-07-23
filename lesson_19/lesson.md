# 📖 Lesson 19 — Transactionlar va xavfsiz o‘zgartirishlar

## 🎯 Maqsad
PostgreSQL’da transactionlar yordamida ma’lumotlarni xavfsiz va ishonchli o‘zgartirish, ACID tamoyillari va transaction xatoliklarini chuqur o‘rganish.

---

## 1. Transaction nazariyasi

### Nazariya
- **Transaction** — bir nechta SQL amallarini bitta yaxlit blokda bajarish.
- **ACID** tamoyillari:
  - **A**tomicity — transaction to‘liq bajariladi yoki umuman bajarilmaydi
  - **C**onsistency — transactiondan oldin va keyin ma’lumotlar bazasi yaxlit bo‘ladi
  - **I**solation — transactionlar bir-biriga ta’sir qilmaydi
  - **D**urability — transaction yakunlangach, natija saqlanib qoladi

---

## 2. Transaction sintaksisi va asosiy amallar

### Nazariya
- Transactionlar yordamida bir nechta o‘zgarishlarni xavfsiz bajarish mumkin
- Asosiy buyruqlar: `BEGIN`, `COMMIT`, `ROLLBACK`, `SAVEPOINT`, `RELEASE`

### Misollar
```sql
-- Transaction boshlash
BEGIN;

-- Bir nechta o‘zgarishlar
UPDATE students SET grade = 'A' WHERE id = 1;
DELETE FROM orders WHERE student_id = 1;

-- Transactionni yakunlash
COMMIT;
```
**Natija:** Ikkala o‘zgarish ham birga bajariladi yoki umuman bajarilmaydi.

```sql
-- Transactionni bekor qilish
BEGIN;
UPDATE students SET grade = 'B' WHERE id = 2;
ROLLBACK;
```
**Natija:** O‘zgarishlar bekor qilinadi, ma’lumotlar avvalgi holatga qaytadi.

---

## 3. Transactionlar bilan xavfsiz o‘zgartirishlar

### Nazariya
- Transactionlar katta hajmdagi o‘zgarishlarni xavfsiz bajarish uchun ishlatiladi
- Xatolik yuz bersa, barcha o‘zgarishlar bekor qilinadi

### Misol
```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
-- Xatolik bo‘lsa
ROLLBACK;
-- Hammasi to‘xtaydi va pul o‘tkazilmaydi
-- Aks holda
COMMIT;
-- Pul muvaffaqiyatli o‘tkaziladi
```
**Izoh:** Transactionlar bank operatsiyalari kabi muhim amallarda juda zarur.

---

## 4. SAVEPOINT va nested transaction

### Nazariya
- **SAVEPOINT** — transaction ichida oraliq nuqta belgilash
- **ROLLBACK TO SAVEPOINT** — faqat shu nuqtadan keyingi o‘zgarishlarni bekor qilish

### Misol
```sql
BEGIN;
UPDATE students SET grade = 'C' WHERE id = 3;
SAVEPOINT old_grade;
UPDATE students SET grade = 'A' WHERE id = 3;
-- Xatolik bo‘lsa
ROLLBACK TO old_grade;
-- Faqat ikkinchi o‘zgarish bekor qilinadi
COMMIT;
```
**Izoh:** SAVEPOINT yordamida transaction ichida qisman bekor qilish mumkin.

---

## 5. Isolation levels

### Nazariya
- Transactionlar bir-biriga ta’sir qilmasligi uchun isolation levels ishlatiladi
- Asosiy isolation levels:
  - **READ COMMITTED** (default): faqat commit qilingan o‘zgarishlarni ko‘radi
  - **REPEATABLE READ**: transaction davomida natija o‘zgarmaydi
  - **SERIALIZABLE**: eng yuqori xavfsizlik, transactionlar to‘liq izolyatsiya

### Misol
```sql
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
BEGIN;
SELECT * FROM accounts WHERE id = 1;
-- Boshqa transaction o‘zgartirsa ham, natija o‘zgarmaydi
COMMIT;
```
**Izoh:** Isolation level tanlash — xavfsizlik va samaradorlik muvozanati.

---

## 6. Transaction xatolari va muammolari

### Nazariya
- **Deadlock** — ikki transaction bir-birini kutib qoladi
- **Lost update** — bir transaction boshqasining o‘zgarishini yo‘qotadi
- **Dirty read** — commit qilinmagan o‘zgarishlarni ko‘rish
- **Phantom read** — transaction davomida natijalar o‘zgarib ketadi

### Misol (deadlock):
```sql
-- Transaction 1
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
-- Transaction 2
BEGIN;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
-- Endi har biri boshqasining lockini kutadi va deadlock yuz beradi
```
**Izoh:** Deadlocklarni oldini olish uchun transactionlarni qisqa va tartibli yozish kerak.

---

## 7. Amaliy maslahatlar va best practices
- Transactionlarni faqat zarur bo‘lsa ishlating
- Transactionlarni imkon qadar qisqa tuting
- Har doim xatoliklarni tekshiring va ROLLBACK dan foydalaning
- Isolation levelni ehtiyojga qarab tanlang
- Katta o‘zgarishlardan oldin backup oling

---

## 8. Xulosa
- Transactionlar — xavfsiz va ishonchli o‘zgarishlar uchun asos
- ACID tamoyillari — transactionlarning poydevori
- ROLLBACK va SAVEPOINT yordamida xatoliklarni boshqarish mumkin
- Isolation level — xavfsizlik va samaradorlik muvozanati

---

## 📌 Keyingi dars:
[Lesson 20 — Trigger va avtomatlashtirish](../lesson_20/lesson.md) 