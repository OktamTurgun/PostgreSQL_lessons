# 📖 Git Darslari — Lesson 03: Branch va boshqarish

## 🎯 Maqsad
Git'da branch (shox) yaratish, boshqarish va merge qilish jarayonini o'rganish.

---

## 📖 Branch nima?

Branch — bu loyihaning alohida versiyasi bo'lib, asosiy kodga ta'sir qilmasdan yangi funksiyalar qo'shish imkonini beradi.

### Branch'ning afzalliklari:
- ✅ Asosiy kodni himoya qilish
- ✅ Bir nechta ishlarni parallel bajarish
- ✅ Xatolarni oson tuzatish
- ✅ Jamoa bilan ishlash

---

## 🔷 Branch bilan ishlash

### 1. Branch'lar ro'yxatini ko'rish:
```bash
# Barcha branch'lar
git branch

# Barcha branch'lar (remote bilan)
git branch -a

# Batafsil ma'lumot
git branch -v
```

### 2. Yangi branch yaratish:
```bash
# Yangi branch yaratish
git branch <branch_nomi>

# Branch yaratish va o'tish
git checkout -b <branch_nomi>

# Yangi usul (Git 2.23+)
git switch -c <branch_nomi>
```

### 3. Branch'lar orasida o'tish:
```bash
# Branch'ga o'tish
git checkout <branch_nomi>

# Yangi usul
git switch <branch_nomi>
```

---

## 🔷 Amaliy mashg'ulot

### 1. Yangi branch yaratish:
```bash
# Yangi branch yaratish
git checkout -b yangi-funksiya

# Holatni tekshirish
git branch

# Yangi fayl yaratish
echo "Bu yangi funksiya" > yangi_funksiya.txt

# Commit qilish
git add .
git commit -m "Yangi funksiya qo'shildi"
```

### 2. Asosiy branch'ga qaytish:
```bash
# main branch'ga qaytish
git checkout main

# Yoki
git switch main
```

### 3. Branch'lar tarixini ko'rish:
```bash
# Grafik tarix
git log --graph --oneline --all

# Faqat joriy branch
git log --oneline
```

---

## 🔷 Merge (Birlashtirish)

### 1. Branch'ni merge qilish:
```bash
# Asosiy branch'ga o'tish
git checkout main

# Branch'ni merge qilish
git merge <branch_nomi>

# Yoki
git merge yangi-funksiya
```

### 2. Merge turi:
```bash
# Fast-forward merge (oddiy)
git merge feature-branch

# No-fast-forward merge (tarixni saqlash)
git merge --no-ff feature-branch
```

### 3. Merge'ni bekor qilish:
```bash
# Merge'ni bekor qilish
git merge --abort

# Yoki
git reset --hard HEAD
```

---

## 🔷 Conflict (Ziddiyat) hal qilish

### 1. Conflict yuzaga kelganda:
```bash
# Conflict fayllarini ko'rish
git status

# Conflict'ni hal qilish
# Faylni ochib, <<<<<<< HEAD va >>>>>>> belgilarini olib tashlang

# Hal qilingan fayllarni qo'shish
git add <fayl_nomi>

# Merge'ni tugatish
git commit
```

### 2. Conflict misoli:
```bash
# Fayl ichidagi conflict
<<<<<<< HEAD
Bu asosiy branch'dagi matn
=======
Bu yangi branch'dagi matn
>>>>>>> yangi-funksiya
```

**Hal qilish:**
```bash
# Birini tanlang yoki ikkalasini birlashtiring
Bu asosiy branch'dagi matn
Bu yangi branch'dagi matn
```

---

## 🔷 Branch'ni o'chirish

### 1. Branch'ni o'chirish:
```bash
# Branch'ni o'chirish (faqat local)
git branch -d <branch_nomi>

# Majburiy o'chirish
git branch -D <branch_nomi>
```

### 2. Remote branch'ni o'chirish:
```bash
# Remote branch'ni o'chirish
git push origin --delete <branch_nomi>
```

---

## 📋 Branch nomlash konventsiyasi

### Yaxshi branch nomlari:
```bash
git checkout -b feature/yangi-funksiya
git checkout -b bugfix/xatoni-tuzatish
git checkout -b hotfix/urgent-tuzatish
git checkout -b release/v1.0.0
```

### Yomon branch nomlari:
```bash
git checkout -b branch1
git checkout -b test
git checkout -b new
```

---

## 📌 Asosiy buyruqlar jadvali

| Buyruq | Ma'nosi | Misol |
|--------|---------|-------|
| `git branch` | Branch'lar ro'yxati | `git branch` |
| `git checkout -b` | Yangi branch yaratish | `git checkout -b yangi-branch` |
| `git checkout` | Branch'ga o'tish | `git checkout main` |
| `git merge` | Branch'ni birlashtirish | `git merge feature-branch` |
| `git branch -d` | Branch'ni o'chirish | `git branch -d eski-branch` |

---

## 🎯 Dars yakunida bilishingiz kerak:

✅ Branch tushunchasi va afzalliklari  
✅ Branch yaratish va boshqarish  
✅ Merge jarayoni  
✅ Conflict hal qilish  
✅ Branch nomlash qoidalari  

---

## 📚 Keyingi dars:
[Lesson 04 — Remote repository va GitHub](../lesson_04/lesson.md)

---

## 🎯 Uy vazifasi:
1. Yangi branch yarating
2. Fayl yarating va commit qiling
3. Asosiy branch'ga qayting
4. Branch'ni merge qiling
5. Branch'ni o'chiring 