# 📝 Amaliyot — Transaction va ACID xususiyatlari

Quyidagi amaliy mashqlarni bajaring. Har bir topshiriq uchun kod va natijani yozing.

---

### 1. Oddiy transaction yaratish

**Vazifa:**
Ikki talaba qo'shish va ularning baholarini yangilash operatsiyalarini bitta transactionda bajarish. Agar xatolik bo'lsa, hammasi bekor qilinsin.

**Kod:**
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

**Natija:**
```sql
-- Barcha operatsiyalar muvaffaqiyatli bajariladi
-- Yoki xatolik bo'lsa, hammasi bekor qilinadi
```

---

### 2. SAVEPOINT bilan transaction

**Vazifa:**
Bir nechta operatsiyalarni bajarib, SAVEPOINT yordamida oraliq nuqtalarni saqlash. Agar xatolik bo'lsa, SAVEPOINTga qaytish.

**Kod:**
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

**Natija:**
```sql
-- Operatsiyalar bajariladi, SAVEPOINTlar saqlanadi
-- Xatolik bo'lsa, SAVEPOINTga qaytish mumkin
```

---

### 3. Xatolik bilan transaction

**Vazifa:**
Bir nechta operatsiyalarni bajarib, xatolik yuzaga kelganda transactionni bekor qilish. Natijada ma'lumotlar avvalgi holatiga qaytishi kerak.

**Kod:**
```sql
BEGIN;

-- Birinchi operatsiya
INSERT INTO students (name, grade) VALUES ('Zafar', 'A');

-- Ikkinchi operatsiya
INSERT INTO students (name, grade) VALUES ('Malika', 'B');

-- Xatolik yuzaga keladi (masalan, noto'g'ri ma'lumot)
INSERT INTO students (name, grade) VALUES ('', 'X'); -- Xatolik!

-- Transactionni bekor qilish
ROLLBACK;
```

**Natija:**
```sql
-- Xatolik yuzaga kelganda ROLLBACK qilinadi
-- Ma'lumotlar avvalgi holatiga qaytadi
```

---

### 4. Isolation level o'rnatish

**Vazifa:**
Transaction isolation level o'rnatib, ma'lumotlarni o'qish va yozish operatsiyalarini bajarish.

**Kod:**
```sql
BEGIN;
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;

-- Ma'lumotlarni o'qish
SELECT * FROM students WHERE grade = 'A';

-- Yangi ma'lumot qo'shish
INSERT INTO students (name, grade) VALUES ('Sardor', 'A');

-- Yana o'qish
SELECT * FROM students WHERE grade = 'A';

COMMIT;
```

**Natija:**
```sql
-- Ma'lumotlar isolation level asosida o'qiladi va yoziladi
-- READ COMMITTED darajasida faqat tasdiqlangan ma'lumotlar ko'rinadi
```

---

### 5. ACID xususiyatlarini tushuntirish

**Vazifa:**
ACID xususiyatlarining har birini qisqacha tushuntiring va ularning ahamiyatini yozing.

**Javob:**
```
A - Atomicity (Atomiylik):
- Transaction butunlay bajariladi yoki butunlay bekor qilinadi
- Yarim bajarilgan operatsiyalar bo'lmaydi
- Ma'lumotlar tozaligini ta'minlaydi

C - Consistency (Tutarlilik):
- Ma'lumotlar bazasi har doim tozal holatda qoladi
- Barcha qoidalar va cheklovlar saqlanadi
- Ma'lumotlar o'zaro mos keladi

I - Isolation (Izolyatsiya):
- Bir vaqtda bajarilayotgan transactionlar bir-biriga ta'sir qilmaydi
- Har bir transaction o'ziga xos natija beradi
- Concurrent access muammolarini hal qiladi

D - Durability (Doimiy):
- Bajarilgan transaction natijalari doimiy saqlanadi
- Tizim o'chgandan keyin ham ma'lumotlar saqlanadi
- Ma'lumotlar yo'qolib ketmaydi
```

---

**Natijalarni SQL kod va qisqacha izoh bilan yozing.** 