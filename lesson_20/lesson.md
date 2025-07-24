# 📖 Lesson 20 — Trigger va avtomatlashtirish

## 🎯 Maqsad
PostgreSQL’da triggerlar yordamida avtomatlashtirilgan amallarni yaratish, triggerlarning ishlash tamoyillari va amaliy qo‘llanilishini o‘rganish.

---

## 1. Trigger nazariyasi

### Nazariya
- **Trigger** — bu ma’lumotlar bazasida jadvalga ma’lum bir o‘zgarish (INSERT, UPDATE, DELETE) sodir bo‘lganda avtomatik ishga tushadigan maxsus obyekt.
- Triggerlar yordamida ma’lumotlarni tekshirish, log yuritish, avtomatik hisoblash va boshqa ko‘plab amallarni bajarish mumkin.
- Triggerlar quyidagi holatlarda ishlatiladi:
  - Ma’lumot kiritilganda (INSERT)
  - Ma’lumot o‘zgartirilganda (UPDATE)
  - Ma’lumot o‘chirib tashlanganda (DELETE)

---

## 2. Trigger yaratish va asosiy sintaksis

### Nazariya
- Triggerlar **BEFORE** (oldin) yoki **AFTER** (keyin) ishlashi mumkin.
- Triggerlar PL/pgSQL yoki boshqa procedural tillarda yoziladi.

### Sintaksis
```sql
CREATE TRIGGER trigger_nomi
  BEFORE|AFTER INSERT|UPDATE|DELETE
  ON jadval_nomi
  FOR EACH ROW
  EXECUTE FUNCTION funksiya_nomi();
```

### Misol: Oddiy trigger
#### Avvalgi holat
**students** jadvali:
| id | name   | grade |
|----|--------|-------|
| 1  | Ali    | B     |
| 2  | Vali   | C     |

**audit_log** jadvali bo‘sh:
| id | action | changed_at |
|----|--------|------------|

#### Kod
```sql
-- Avtomatik log yurituvchi trigger
CREATE TABLE audit_log (
  id serial PRIMARY KEY,
  action text,
  changed_at timestamp DEFAULT now()
);

CREATE OR REPLACE FUNCTION log_student_update()
RETURNS trigger AS $$
BEGIN
  INSERT INTO audit_log(action) VALUES ('Student yangilandi');
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER student_update_log
  AFTER UPDATE ON students
  FOR EACH ROW
  EXECUTE FUNCTION log_student_update();

-- Misol uchun yangilash
UPDATE students SET grade = 'A' WHERE id = 1;
```
#### Natija
**audit_log** jadvalida yangi yozuv paydo bo‘ladi:
| id | action              | changed_at         |
|----|---------------------|--------------------|
| 1  | Student yangilandi  | 2024-06-01 10:00   |

**Izoh:** Har safar students jadvali yangilansa, audit_log jadvaliga yozuv qo‘shiladi. Bu audit yuritish uchun qulay.

---

## 3. BEFORE va AFTER triggerlar

### Nazariya
- **BEFORE** trigger — asosiy amal bajarilishidan oldin ishga tushadi, ma’lumotni o‘zgartirish yoki tekshirish uchun ishlatiladi.
- **AFTER** trigger — asosiy amal bajarilgandan so‘ng ishga tushadi, log yuritish yoki tashqi amallar uchun qulay.

### Misol: BEFORE trigger
#### Avvalgi holat
**students** jadvali:
| id | name   | grade |
|----|--------|-------|
| 1  | Ali    | B     |

#### Kod
```sql
CREATE OR REPLACE FUNCTION check_grade()
RETURNS trigger AS $$
BEGIN
  IF NEW.grade NOT IN ('A', 'B', 'C', 'D', 'F') THEN
    RAISE EXCEPTION 'Noto‘g‘ri baho!';
  END IF;
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER grade_check
  BEFORE INSERT OR UPDATE ON students
  FOR EACH ROW
  EXECUTE FUNCTION check_grade();

-- Noto‘g‘ri baho kiritish
INSERT INTO students(name, grade) VALUES ('Hasan', 'E');
```
#### Natija
```
ERROR: Noto‘g‘ri baho!
```
**Izoh:** Noto‘g‘ri baho kiritilsa, xatolik yuz beradi va amal bajarilmaydi. Bu ma’lumotlar sifatini nazorat qilish uchun ishlatiladi.

---

## 4. Triggerlar yordamida avtomatlashtirish

### Nazariya
- Triggerlar yordamida hisob-kitoblarni, loglarni, auditlarni va boshqa avtomatik amallarni bajarish mumkin.
- Masalan, balans o‘zgarishini avtomatik logga yozish yoki bonus hisoblash.

### Misol: Balans o‘zgarishini logga yozish
#### Avvalgi holat
**accounts** jadvali:
| id | name   | balance |
|----|--------|---------|
| 1  | Ali    | 500     |
| 2  | Vali   | 300     |

**balance_log** jadvali bo‘sh:
| id | account_id | old_balance | new_balance | changed_at |
|----|------------|-------------|-------------|------------|

#### Kod
```sql
CREATE TABLE balance_log (
  id serial PRIMARY KEY,
  account_id int,
  old_balance numeric,
  new_balance numeric,
  changed_at timestamp DEFAULT now()
);

CREATE OR REPLACE FUNCTION log_balance_change()
RETURNS trigger AS $$
BEGIN
  INSERT INTO balance_log(account_id, old_balance, new_balance)
  VALUES (OLD.id, OLD.balance, NEW.balance);
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER balance_change_log
  AFTER UPDATE ON accounts
  FOR EACH ROW
  EXECUTE FUNCTION log_balance_change();

-- Balansni o‘zgartirish
UPDATE accounts SET balance = 600 WHERE id = 1;
```
#### Natija
**balance_log** jadvalida yangi yozuv paydo bo‘ladi:
| id | account_id | old_balance | new_balance | changed_at         |
|----|------------|-------------|-------------|--------------------|
| 1  | 1          | 500         | 600         | 2024-06-01 10:05   |

**Izoh:** Har safar accounts jadvalidagi balans o‘zgarsa, logga yoziladi. Bu o‘zgarishlarni kuzatish uchun foydali.

---

## 5. Triggerlar bilan bog‘liq muammolar va best practices
- Triggerlar noto‘g‘ri ishlatilsa, ma’lumotlar bazasini sekinlashtirishi mumkin
- Triggerlarni faqat zarur bo‘lsa ishlating
- Triggerlar zanjiri (chain)dan ehtiyot bo‘ling — bir trigger boshqasini chaqirishi mumkin
- Har doim triggerlar natijasini va xatoliklarni tekshiring
- Katta o‘zgarishlardan oldin backup oling

---

## 6. Xulosa
- Triggerlar yordamida ma’lumotlar bazasida avtomatlashtirish va nazoratni kuchaytirish mumkin
- BEFORE va AFTER triggerlar turli vazifalar uchun ishlatiladi
- Triggerlar yordamida audit, tekshiruv va hisob-kitoblarni avtomatlashtirish mumkin

---

## 📌 Keyingi dars:
[Lesson 21 — View va virtual jadvallar](../lesson_21/lesson.md) 