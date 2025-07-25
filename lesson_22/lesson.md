# 📖 Lesson 22 — Stored procedure va functionlar

## 🎯 Maqsad
PostgreSQL’da stored procedure va functionlar tushunchasi, ularni yaratish, ishlatish va amaliyotda qo‘llashni o‘rganish.

---

## 1. Stored procedure va function nazariyasi

### Nazariya
- **Stored procedure** — bu ma’lum bir vazifani bajarish uchun serverda saqlanadigan va bajariladigan SQL kodlar to‘plami.
- **Function** — bu ma’lum bir qiymat qaytaradigan va ko‘pincha hisob-kitob yoki qayta ishlash uchun ishlatiladigan SQL kodlar to‘plami.
- Ikkalasi ham PL/pgSQL tilida yozilishi mumkin va kodni qayta ishlatish, murakkab operatsiyalarni soddalashtirish uchun ishlatiladi.

---

## 2. Stored procedure va function yaratish va asosiy sintaksis

### Nazariya
- Procedure va functionlar yordamida bir nechta SQL buyruqlarini bitta nom ostida bajarish mumkin.
- Function natija qaytaradi, procedure esa natija qaytarmasligi mumkin.

### Sintaksis
#### Function yaratish:
```sql
CREATE FUNCTION function_nomi(parametrlar) RETURNS return_type AS $$
BEGIN
    -- kodlar
END;
$$ LANGUAGE plpgsql;
```

#### Procedure yaratish:
```sql
CREATE PROCEDURE procedure_nomi(parametrlar) AS $$
BEGIN
    -- kodlar
END;
$$ LANGUAGE plpgsql;
```

---

## 3. Misollar

### Misol: Oddiy function yaratish
```sql
CREATE FUNCTION kvadrat(x integer) RETURNS integer AS $$
BEGIN
    RETURN x * x;
END;
$$ LANGUAGE plpgsql;
```

#### Chaqarish:
```sql
SELECT kvadrat(5); -- Natija: 25
```

### Misol: Oddiy procedure yaratish
```sql
CREATE PROCEDURE salom_ber(ism text) AS $$
BEGIN
    RAISE NOTICE 'Salom, %!', ism;
END;
$$ LANGUAGE plpgsql;
```

#### Chaqarish:
```sql
CALL salom_ber('Ali');
-- Natija: Salom, Ali!
```

---

## 4. Amaliyot
- Function/procedure yordamida hisob-kitob yoki ma’lumotlarni qayta ishlashni avtomatlashtirish mumkin.
- Ularni boshqa so‘rovlarda chaqirish va qayta ishlatish mumkin.

---

## 5. Xulosa
- Stored procedure va functionlar yordamida kodni qayta ishlatish va murakkab operatsiyalarni soddalashtirish mumkin.
- Function natija qaytaradi, procedure esa natija qaytarmasligi mumkin.
- PL/pgSQL yordamida yoziladi.

---

## 📌 Keyingi dars:
[Lesson 23 — Triggerlar va ularning amaliyoti](../lesson_23/lesson.md) 