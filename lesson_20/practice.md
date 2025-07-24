# 📝 Amaliy mashqlar — Trigger va avtomatlashtirish

---

### 1. Oddiy trigger yaratish
**Vazifa:** students jadvalida har safar yangi talaba qo‘shilganda, audit_log jadvaliga yozuv qo‘shiladigan trigger yozing.

**Kod:**
```sql
CREATE OR REPLACE FUNCTION log_student_insert()
RETURNS trigger AS $$
BEGIN
  INSERT INTO audit_log(action) VALUES ('Yangi talaba qo‘shildi');
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER student_insert_log
  AFTER INSERT ON students
  FOR EACH ROW
  EXECUTE FUNCTION log_student_insert();

INSERT INTO students(name, grade) VALUES ('Hasan', 'A');
```
**Natija:**
| id | action                | changed_at         |
|----|-----------------------|--------------------|
| 1  | Yangi talaba qo‘shildi| 2024-06-01 10:10   |

**Izoh:** Har safar yangi talaba qo‘shilganda, audit_log jadvaliga yozuv qo‘shiladi. Bu audit yuritish uchun qulay.

---

### 2. BEFORE trigger orqali bahoni tekshirish
**Vazifa:** students jadvaliga baho kiritilganda, faqat 'A', 'B', 'C', 'D', 'F' qiymatlariga ruxsat beradigan trigger yozing.

**Kod:**
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

INSERT INTO students(name, grade) VALUES ('Vali', 'E');
```
**Natija:**
```
ERROR: Noto‘g‘ri baho!
```
**Izoh:** Noto‘g‘ri baho kiritilsa, xatolik yuz beradi va amal bajarilmaydi. Bu ma’lumotlar sifatini nazorat qilish uchun ishlatiladi.

---

### 3. Balans logi triggeri
**Vazifa:** accounts jadvalida balans o‘zgarganda, eski va yangi qiymatlarni balance_log jadvaliga yozadigan trigger yozing.

**Kod:**
```sql
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

UPDATE accounts SET balance = 700 WHERE id = 1;
```
**Natija:**
| id | account_id | old_balance | new_balance | changed_at         |
|----|------------|-------------|-------------|--------------------|
| 1  | 1          | 600         | 700         | 2024-06-01 10:15   |

**Izoh:** Balans o‘zgarganda, eski va yangi qiymatlar logga yoziladi. Bu o‘zgarishlarni kuzatish uchun foydali.

---

### 4. DELETE trigger va arxivlash
**Vazifa:** orders jadvalidan buyurtma o‘chirib tashlanganda, o‘chirilgan buyurtma ma’lumotlarini order_archive jadvaliga saqlaydigan trigger yozing.

**Kod:**
```sql
CREATE OR REPLACE FUNCTION archive_order()
RETURNS trigger AS $$
BEGIN
  INSERT INTO order_archive(id, student_id, product, amount)
  VALUES (OLD.id, OLD.student_id, OLD.product, OLD.amount);
  RETURN OLD;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER order_delete_archive
  AFTER DELETE ON orders
  FOR EACH ROW
  EXECUTE FUNCTION archive_order();

DELETE FROM orders WHERE id = 5;
```
**Natija:**
| id | student_id | product | amount |
|----|------------|---------|--------|
| 5  | 2          | Kitob   | 2      |

**Izoh:** Buyurtma o‘chirilganda, uning ma’lumotlari order_archive jadvaliga saqlanadi. Bu tarixni saqlash uchun qulay.

---

### 5. Trigger xatoliklari va muammolari
**Vazifa:** Triggerlar noto‘g‘ri ishlatilganda qanday muammolar yuzaga kelishi mumkinligini misollar bilan tushuntiring.

**Tafsif va tushuntirish:**
- **Performance (sekinlik):** Juda ko‘p triggerlar yoki murakkab triggerlar bazani sekinlashtiradi.
- **Zanjirli triggerlar:** Bir trigger boshqasini chaqirsa, kutilmagan natijalar yoki cheksiz sikl bo‘lishi mumkin.
- **Xatoliklarni aniqlash qiyin:** Triggerlar yashirin ishlaydi, xatoliklarni topish qiyin bo‘lishi mumkin.
- **Misol:**
```sql
-- Bir jadvalda UPDATE trigger, ikkinchisida INSERT trigger bo‘lsa,
-- birinchi trigger ikkinchisiga sabab bo‘lishi va natijada cheksiz sikl yuzaga kelishi mumkin.
```
**Izoh:** Triggerlardan foydalanishda ehtiyot bo‘lish, faqat zarur joyda ishlatish va natijalarni doim tekshirish kerak.

---

## Qo‘shimcha savollar
- Triggerlar va stored procedure’lar o‘rtasidagi farq nima?
- BEFORE va AFTER triggerlar qachon ishlatiladi?
- Triggerlar yordamida audit yuritishning afzalliklari va kamchiliklari nimalardan iborat? 