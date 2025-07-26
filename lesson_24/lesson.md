# 📖 Lesson 24 — Transaction va ACID xususiyatlari

## 🎯 Maqsad
PostgreSQL’da transactionlar tushunchasi, ACID xususiyatlari, ularni boshqarish va amaliyotda qo‘llashni o‘rganish.

---

## 1. Transaction nazariyasi

### Nazariya
- **Transaction** — bu ma’lumotlar bazasida bajariladigan bir nechta operatsiyalar to‘plami, ular bir butun sifatida bajariladi yoki butunlay bekor qilinadi.
- Transactionlar ma’lumotlar tozaligini ta’minlaydi va xatoliklar paydo bo‘lganda ma’lumotlarni avvalgi holatiga qaytaradi.
- Har bir transaction ACID xususiyatlariga ega bo‘lishi kerak.

### ACID xususiyatlari
| Xususiyat | Tushuntirish |
|-----------|-------------|
| **A**tomicity | Transaction butunlay bajariladi yoki butunlay bekor qilinadi |
| **C**onsistency | Ma’lumotlar bazasi har doim tozal holatda qoladi |
| **I**solation | Bir vaqtda bajarilayotgan transactionlar bir-biriga ta’sir qilmaydi |
| **D**urability | Bajarilgan transaction natijalari doimiy saqlanadi |

---

## 2. Transaction boshqarish va asosiy sintaksis

### Sintaksis
#### Transaction boshlash:
```sql
BEGIN;
-- yoki
START TRANSACTION;
```

#### Transactionni tasdiqlash:
```sql
COMMIT;
```

#### Transactionni bekor qilish:
```sql
ROLLBACK;
```

#### SAVEPOINT yaratish:
```sql
SAVEPOINT savepoint_nomi;
```

#### SAVEPOINTga qaytish:
```sql
ROLLBACK TO SAVEPOINT savepoint_nomi;
```

---

## 3. Amaliy misollar

### Misol 1: Oddiy transaction
**Vazifa:** Ikki talaba qo‘shish va ularning baholarini yangilash operatsiyalarini bitta transactionda bajarish.

```sql
BEGIN;

-- Birinchi talaba qo'shish
INSERT INTO students (name, grade) VALUES ('Ali', 'A');

-- Ikkinchi talaba qo'shish
INSERT INTO students (name, grade) VALUES ('Vali', 'B');

-- Baholarni yangilash
UPDATE students SET grade = 'A+' WHERE name = 'Ali';

-- Transactionni tasdiqlash
COMMIT;
```

**Natija:** Barcha operatsiyalar muvaffaqiyatli bajariladi yoki xatolik bo‘lsa, hammasi bekor qilinadi.

### Misol 2: SAVEPOINT bilan transaction
**Vazifa:** Bir nechta operatsiyalarni bajarib, oraliq nuqtalarni saqlash.

```sql
BEGIN;

-- Birinchi operatsiya
INSERT INTO students (name, grade) VALUES ('Hasan', 'C');
SAVEPOINT sp1;

-- Ikkinchi operatsiya
UPDATE students SET grade = 'B' WHERE name = 'Hasan';
SAVEPOINT sp2;

-- Uchinchi operatsiya
DELETE FROM students WHERE name = 'Hasan';

-- Agar xatolik bo'lsa, sp2 ga qaytish
ROLLBACK TO SAVEPOINT sp2;

-- Yoki transactionni tasdiqlash
COMMIT;
```

### Misol 3: Xatolik bilan transaction
**Vazifa:** Xatolik yuzaga kelganda transactionni bekor qilish.

```sql
BEGIN;

INSERT INTO students (name, grade) VALUES ('Zafar', 'A');
INSERT INTO students (name, grade) VALUES ('Malika', 'B');

-- Xatolik yuzaga keladi (masalan, noto'g'ri ma'lumot)
INSERT INTO students (name, grade) VALUES ('', 'X'); -- Xatolik!

-- Transactionni bekor qilish
ROLLBACK;
```

**Natija:** Barcha operatsiyalar bekor qilinadi, ma’lumotlar avvalgi holatiga qaytadi.

---

## 4. Transaction isolation levels

### Isolation darajalari
| Daraja | Tushuntirish |
|--------|-------------|
| **READ UNCOMMITTED** | Boshqa transactionlar tomonidan tasdiqlanmagan ma’lumotlarni o‘qish |
| **READ COMMITTED** | Faqat tasdiqlangan ma’lumotlarni o‘qish (PostgreSQL default) |
| **REPEATABLE READ** | Bir xil transaction davomida bir xil natijalarni olish |
| **SERIALIZABLE** | Eng yuqori izolyatsiya darajasi |

### Isolation level o‘rnatish:
```sql
BEGIN;
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
-- operatsiyalar
COMMIT;
```

---

## 5. Best practices va muammolar
- Transactionlarni qisqa tuting — uzoq transactionlar boshqa foydalanuvchilarni bloklashga olib keladi.
- Xatoliklarni to‘g‘ri boshqaring — har doim ROLLBACK yoki COMMIT qiling.
- SAVEPOINTlardan foydalaning murakkab transactionlarda.
- Deadlock muammolarini oldini olish uchun ma’lumotlarga bir xil tartibda kirish.
- Transactionlarni test qiling — xatolik holatlarini sinab ko‘ring.

---

## 6. Xulosa
- Transactionlar ma’lumotlar tozaligini ta’minlaydi va xatoliklar paydo bo‘lganda ma’lumotlarni avvalgi holatiga qaytaradi.
- ACID xususiyatlari har bir transaction uchun zarur.
- Transactionlarni to‘g‘ri boshqarish ma’lumotlar bazasi ishonchliligini ta’minlaydi.
- SAVEPOINT va isolation level yordamida murakkab operatsiyalarni boshqarish mumkin.

---

## 📌 Keyingi dars:
[Lesson 25 — Index va samaradorlik optimizatsiyasi](../lesson_25/lesson.md) 