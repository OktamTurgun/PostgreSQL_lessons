# 📝 Amaliyot — Transactionlar va xavfsiz o‘zgartirishlar

Quyidagi topshiriqlarda har bir misol uchun:
- Avvalgi holat (jadval ko‘rinishida)
- SQL kod
- Natija holati (jadval ko‘rinishida)
- Izoh

---

## 1. Oddiy transaction
**Vazifa:** Bir nechta o‘zgarishni transactionda bajarib, COMMIT va ROLLBACK farqini ko‘rsating.

**Avvalgi holat (students):**
| id | name  | grade |
|----|-------|-------|
| 1  | Ali   | B     |
| 2  | Vali  | C     |

**Avvalgi holat (orders):**
| id | student_id | total_amount |
|----|------------|--------------|
| 1  | 1          | 100000       |
| 2  | 2          | 200000       |

**SQL kod:**
```sql
BEGIN;
UPDATE students SET grade = 'A' WHERE id = 1;
DELETE FROM orders WHERE student_id = 1;
COMMIT;
```

**Natija holati:**
| id | name  | grade |
|----|-------|-------|
| 1  | Ali   | A     |
| 2  | Vali  | C     |

| id | student_id | total_amount |
|----|------------|--------------|
| 2  | 2          | 200000       |

**Izoh:** Ikkala o‘zgarish ham birga bajariladi.

---

**SQL kod (ROLLBACK):**
```sql
BEGIN;
UPDATE students SET grade = 'B' WHERE id = 2;
ROLLBACK;
```
**Natija holati:**
| id | name  | grade |
|----|-------|-------|
| 1  | Ali   | A     |
| 2  | Vali  | C     |

**Izoh:** O‘zgarishlar bekor qilinadi, jadval avvalgi holatga qaytadi.

---

## 2. Transaction bilan xavfsiz pul o‘tkazish
**Vazifa:** accounts jadvalidan bir hisobdan boshqasiga pul o‘tkazishni transactionda bajaring. Xatolik yuz bersa, rollback qiling.

**Avvalgi holat (accounts):**
| id | name   | balance |
|----|--------|---------|
| 1  | Ali    | 500     |
| 2  | Vali   | 300     |

**SQL kod:**
```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

**Natija holati:**
| id | name   | balance |
|----|--------|---------|
| 1  | Ali    | 400     |
| 2  | Vali   | 400     |

**Izoh:** Transaction bo‘lmasa, pul noto‘g‘ri o‘tkazilishi mumkin.

---

## 3. SAVEPOINT bilan qisman bekor qilish
**Vazifa:** Transaction ichida SAVEPOINT va ROLLBACK TO SAVEPOINT ishlatib ko‘ring.

**Avvalgi holat (students):**
| id | name  | grade |
|----|-------|-------|
| 3  | Gulbahor | B  |

**SQL kod:**
```sql
BEGIN;
UPDATE students SET grade = 'C' WHERE id = 3;
SAVEPOINT old_grade;
UPDATE students SET grade = 'A' WHERE id = 3;
ROLLBACK TO old_grade;
COMMIT;
```

**Natija holati:**
| id | name  | grade |
|----|-------|-------|
| 3  | Gulbahor | C  |

**Izoh:** Faqat ikkinchi o‘zgarish bekor qilinadi, birinchisi saqlanadi.

---

## 4. Isolation levelni o‘zgartirish
**Vazifa:** Transactionda isolation levelni REPEATABLE READ qilib, natijani tahlil qiling.

**Avvalgi holat (accounts):**
| id | name   | balance |
|----|--------|---------|
| 1  | Ali    | 400     |

**SQL kod:**
```sql
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
BEGIN;
SELECT * FROM accounts WHERE id = 1;
-- Boshqa transaction o‘zgartirsa ham, natija o‘zgarmaydi
COMMIT;
```

**Natija holati:**
| id | name   | balance |
|----|--------|---------|
| 1  | Ali    | 400     |

**Izoh:** Transaction davomida natija o‘zgarmaydi.

---

## 5. Deadlock holatini ko‘rsatish
**Vazifa:** Ikki transaction bir-birini kutib qoladigan (deadlock) vaziyatni misol bilan ko‘rsating.

**Avvalgi holat (accounts):**
| id | name   | balance |
|----|--------|---------|
| 1  | Ali    | 400     |
| 2  | Vali   | 400     |

**SQL kod:**
```sql
-- Transaction 1
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
-- Transaction 2
BEGIN;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
-- Endi har biri boshqasining lockini kutadi va deadlock yuz beradi
```

**Natija holati:**
| id | name   | balance |
|----|--------|---------|
| 1  | Ali    | 400     |
| 2  | Vali   | 400     |

**Izoh:** Deadlocklarni oldini olish uchun transactionlarni qisqa va tartibli yozing.

---

## 6. Amaliy maslahatlar
- Transactionlarni faqat zarur bo‘lsa ishlating
- Transactionlarni imkon qadar qisqa tuting
- Har doim xatoliklarni tekshiring va ROLLBACK dan foydalaning
- Isolation levelni ehtiyojga qarab tanlang
- Katta o‘zgarishlardan oldin backup oling

---

Har bir topshiriqni bajaring, natijani tahlil qiling va savollaringiz bo‘lsa, yozib qoldiring. 