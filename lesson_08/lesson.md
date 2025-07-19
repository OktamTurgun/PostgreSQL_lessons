# 📖 Lesson 08 — NULL va DEFAULT qiymatlar

## 🎯 Maqsad
PostgreSQLʼda NULL va DEFAULT qiymatlar tushunchasi, ularning farqi va amaliy qoʼllanilishini oʼrganish.

---

## 📖 Nazariya

Maʼlumotlar bazasida har bir ustun uchun qiymat kiritilishi shart emas. Baʼzi ustunlar boʼsh (NULL) yoki standart (DEFAULT) qiymatga ega boʼlishi mumkin.

### NULL qiymat nima?
- **NULL** — qiymat yoʼqligini bildiradi ("maʼlumot kiritilmagan").
- NULL — bu 0, boʼsh string yoki FALSE emas, balki "nomaʼlum" yoki "aniqlanmagan" qiymat.

### DEFAULT qiymat nima?
- **DEFAULT** — ustun uchun avtomatik tarzda beriladigan standart qiymat.
- Agar qiymat kiritilmasa, ustun DEFAULT qiymat bilan toʼldiriladi.

---

## 🔷 NULL va DEFAULT bilan ishlash

### 📋 Jadval yaratishda
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INTEGER,
    email VARCHAR(255) DEFAULT 'noemail@example.com',
    is_active BOOLEAN DEFAULT TRUE,
    created_at DATE DEFAULT CURRENT_DATE
);
```

---

### 📋 Maʼlumot kiritishda
```sql
-- NULL qiymat kiritish
INSERT INTO users (name, age) VALUES ('Ali', NULL);

-- DEFAULT qiymatdan foydalanish (ustunni tashlab ketish)
INSERT INTO users (name) VALUES ('Vali');

-- DEFAULT kalit soʼzi bilan
INSERT INTO users (name, age, email) VALUES ('Gulbahor', 28, DEFAULT);
```

---

### 📋 NULL va DEFAULT qiymatlarni SELECT bilan koʼrish
```sql
SELECT * FROM users;

-- Faqat NULL qiymatlarni koʼrish
SELECT * FROM users WHERE email IS NULL;

-- Faqat DEFAULT qiymatdagi yozuvlarni koʼrish
SELECT * FROM users WHERE email = 'noemail@example.com';
```

---

### 📋 NULL bilan ishlashda muhim operatorlar
- `IS NULL` — qiymat NULL boʼlsa
- `IS NOT NULL` — qiymat NULL boʼlmasa
- `COALESCE(val, default)` — NULL boʼlsa, default qiymatni qaytaradi

```sql
SELECT name, COALESCE(email, 'yoʼq') AS email_koʼrinishi FROM users;
```

---

### 📋 NOT NULL cheklovi
- Ustun NOT NULL boʼlsa, qiymat kiritish majburiy
- NULL qiymat kiritilsa, xatolik yuz beradi

```sql
-- Xato: name NOT NULL boʼlgani uchun qiymat kiritilmagan
INSERT INTO users (age) VALUES (25); -- XATO!
```

---

### 📋 DEFAULT qiymatni oʼzgartirish
```sql
ALTER TABLE users ALTER COLUMN email SET DEFAULT 'user@example.com';
ALTER TABLE users ALTER COLUMN is_active SET DEFAULT FALSE;
```

---

## 🔷 Amaliy maslahatlar
- NULL va DEFAULT qiymatlarni toʼgʼri ishlating
- NULL qiymatlarni tahlil qilishda ehtiyot boʼling
- DEFAULT qiymatlar yordamida kodni soddalashtiring
- NOT NULL cheklovlari bilan maʼlumot yaxlitligini taʼminlang

---

## 📌 Eng koʼp ishlatiladigan usullar
✅ **NULL qiymat** — `IS NULL`, `IS NOT NULL`, `COALESCE()`  
✅ **DEFAULT qiymat** — ustunni tashlab ketish yoki `DEFAULT` kalit soʼzi  
✅ **NOT NULL** — majburiy ustunlar uchun

---

## 📌 Keyingi dars:
[Lesson 09 — SELECT ga kirish (Intro to SELECT)](../lesson_09/lesson.md) 