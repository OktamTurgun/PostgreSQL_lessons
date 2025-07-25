# 📖 Lesson 23 — Triggerlar va ularning amaliyoti

## 🎯 Maqsad
PostgreSQL’da triggerlar tushunchasi, ularni yaratish, ishlatish, amaliyotda qo‘llash va samarali foydalanishni o‘rganish.

---

## 1. Trigger nazariyasi

### Nazariya
- **Trigger** — bu jadvalda ma’lum bir hodisa (INSERT, UPDATE, DELETE) sodir bo‘lganda avtomatik ishga tushadigan maxsus obyekt.
- Triggerlar yordamida ma’lumotlarni avtomatik nazorat qilish, log yuritish, hisob-kitoblarni avtomatlashtirish mumkin.
- Triggerlar PL/pgSQL yoki boshqa tillarda yozilishi mumkin.

### Trigger turlari
| Trigger turi | Qachon ishga tushadi         |
|-------------|-----------------------------|
| BEFORE      | Hodisadan oldin             |
| AFTER       | Hodisadan so‘ng             |
| INSTEAD OF  | View’larda, hodisa o‘rniga  |

- Triggerlar INSERT, UPDATE, DELETE hodisalari uchun yozilishi mumkin.

---

## 2. Trigger yaratish va asosiy sintaksis

### Sintaksis
#### Trigger function yaratish:
```sql
CREATE FUNCTION function_nomi() RETURNS trigger AS $$
BEGIN
    -- kodlar
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

#### Trigger yaratish:
```sql
CREATE TRIGGER trigger_nomi
    BEFORE|AFTER INSERT|UPDATE|DELETE
    ON jadval_nomi
    FOR EACH ROW
    EXECUTE FUNCTION function_nomi();
```

#### Trigger o‘chirish:
```sql
DROP TRIGGER trigger_nomi ON jadval_nomi;
```

---

## 3. Amaliy misollar

### Misol 1: Log yurituvchi trigger
**Vazifa:** Har safar students jadvaliga yangi talaba qo‘shilganda, log_students jadvaliga yozuv qo‘shilsin.

```sql
-- Log jadvali
CREATE TABLE log_students (
    id serial PRIMARY KEY,
    student_id integer,
    action text,
    log_time timestamp DEFAULT now()
);

-- Trigger function
CREATE FUNCTION log_student_insert() RETURNS trigger AS $$
BEGIN
    INSERT INTO log_students(student_id, action)
    VALUES (NEW.id, 'INSERT');
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

-- Trigger
CREATE TRIGGER trg_student_insert
    AFTER INSERT ON students
    FOR EACH ROW
    EXECUTE FUNCTION log_student_insert();
```

### Misol 2: Ma’lumotni avtomatik yangilovchi trigger
**Vazifa:** students jadvalida grade o‘zgarsa, log_students jadvaliga o‘zgarish haqida yozuv qo‘shilsin.

```sql
CREATE FUNCTION log_student_update() RETURNS trigger AS $$
BEGIN
    IF OLD.grade IS DISTINCT FROM NEW.grade THEN
        INSERT INTO log_students(student_id, action)
        VALUES (NEW.id, 'UPDATE grade');
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_student_update
    AFTER UPDATE ON students
    FOR EACH ROW
    EXECUTE FUNCTION log_student_update();
```

---

## 4. Best practices va muammolar
- Triggerlarni faqat zarur hollarda ishlating — haddan tashqari triggerlar samaradorlikka salbiy ta’sir qilishi mumkin.
- Triggerlar zanjiri (bir trigger boshqasini chaqirishi) murakkablik va xatoliklarni oshiradi.
- Debug qilish uchun RAISE NOTICE yoki log yozishdan foydalaning.
- Trigger function har doim `RETURN NEW;` yoki `RETURN OLD;` bilan tugashi kerak.

---

## 5. Xulosa
- Triggerlar yordamida ma’lumotlar ustida avtomatik nazorat va amaliyotlarni bajarish mumkin.
- BEFORE va AFTER triggerlar yordamida turli vazifalarni avtomatlashtirish mumkin.
- Triggerlardan samarali va ehtiyotkorlik bilan foydalanish kerak.

---

## 📌 Keyingi dars:
[Lesson 24 — Transaction va ACID xususiyatlari](../lesson_24/lesson.md) 