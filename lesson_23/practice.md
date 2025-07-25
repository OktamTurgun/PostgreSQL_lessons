# 📝 Amaliyot — Triggerlar va ularning amaliyoti

Quyidagi amaliy mashqlarni bajaring. Har bir topshiriq uchun kod va natijani yozing.

---

### 1. Yangi yozuv qo‘shilganda log yurituvchi trigger

**Vazifa:**
Har safar students jadvaliga yangi talaba qo‘shilganda, log_students jadvaliga yozuv qo‘shiladigan trigger yozing.

**Kod:**
```sql
-- Log jadvali va trigger function, trigger kodini yozing
```

**Natija:**
```sql
INSERT INTO students (name, grade) VALUES ('Ali', 'A');
-- log_students jadvalida yangi yozuv paydo bo‘ladi
```

---

### 2. Ma’lumot o‘zgarganda avtomatik log yozuvchi trigger

**Vazifa:**
Agar students jadvalida grade ustuni o‘zgarsa, log_students jadvaliga o‘zgarish haqida yozuv qo‘shiladigan trigger yozing.

**Kod:**
```sql
-- Trigger function va trigger kodini yozing
```

**Natija:**
```sql
UPDATE students SET grade = 'B' WHERE name = 'Ali';
-- log_students jadvalida 'UPDATE grade' yozuvi paydo bo‘ladi
```

---

### 3. DELETE hodisasini log qiluvchi trigger

**Vazifa:**
Talaba o‘chirib tashlanganda, log_students jadvaliga 'DELETE' yozuvi qo‘shiladigan trigger yozing.

**Kod:**
```sql
-- Trigger function va trigger kodini yozing
```

**Natija:**
```sql
DELETE FROM students WHERE name = 'Ali';
-- log_students jadvalida 'DELETE' yozuvi paydo bo‘ladi
```

---

### 4. BEFORE trigger yordamida ma’lumotni tekshirish

**Vazifa:**
Talaba qo‘shilganda, grade qiymati faqat 'A', 'B', 'C' bo‘lishini tekshiradigan BEFORE trigger yozing. Noto‘g‘ri qiymat kiritilsa, xatolik chiqsin.

**Kod:**
```sql
-- BEFORE trigger function va trigger kodini yozing
```

**Natija:**
```sql
INSERT INTO students (name, grade) VALUES ('Vali', 'D');
-- Xatolik: grade faqat 'A', 'B', 'C' bo‘lishi mumkin
```

---

**Natijalarni SQL kod va qisqacha izoh bilan yozing.** 