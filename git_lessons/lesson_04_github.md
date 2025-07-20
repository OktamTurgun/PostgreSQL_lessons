# 📖 Git Darslari — Lesson 04: GitHub va remote repository

## 🎯 Maqsad
GitHub bilan ishlash, remote repository yaratish va boshqarish jarayonini o'rganish.

---

## 📖 GitHub nima?

GitHub — bu Git repository'larni saqlash va boshqarish uchun ishlatiladigan platforma.

### GitHub'ning afzalliklari:
- ✅ Kodni cloud'da saqlash
- ✅ Jamoa bilan ishlash
- ✅ Loyiha tarixini ko'rish
- ✅ Pull Request va Code Review
- ✅ Issue va Project boshqarish

---

## 🔧 GitHub'da hisob yaratish

### 1. Hisob yaratish:
- [GitHub.com](https://github.com) sahifasiga boring
- "Sign up" tugmasini bosing
- Email, parol va username kiriting

### 2. SSH key yaratish:
```bash
# SSH key yaratish
ssh-keygen -t rsa -b 4096 -C "sizning@email.com"

# SSH key'ni ko'rish
cat ~/.ssh/id_rsa.pub

# SSH agent'ni ishga tushirish
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

---

## 🔷 Remote repository bilan ishlash

### 1. Remote repository'ni qo'shish:
```bash
# Remote repository'ni qo'shish
git remote add origin <repository_url>

# Remote'lar ro'yxatini ko'rish
git remote -v

# Remote'ni o'chirish
git remote remove origin
```

### 2. Repository'ni push qilish:
```bash
# Birinchi push
git push -u origin main

# Keyingi push'lar
git push origin main

# Barcha branch'lar
git push --all origin
```

### 3. Repository'ni pull qilish:
```bash
# O'zgarishlarni yuklab olish
git pull origin main

# Faqat ma'lumotlarni ko'rish
git fetch origin
```

---

## 🔷 Amaliy mashg'ulot

### 1. GitHub'da repository yaratish:
```bash
# Local repository yaratish
mkdir my-github-project
cd my-github-project
git init

# README faylini yaratish
echo "# Mening GitHub loyiham" > README.md

# Commit qilish
git add .
git commit -m "Birinchi commit"
```

### 2. GitHub'ga ulanish:
```bash
# Remote repository'ni qo'shish
git remote add origin https://github.com/username/repository-name.git

# Push qilish
git push -u origin main
```

### 3. O'zgarishlarni yuklash:
```bash
# Yangi fayl yaratish
echo "Bu yangi fayl" > new_file.txt

# Commit va push
git add .
git commit -m "Yangi fayl qo'shildi"
git push origin main
```

---

## 🔷 Repository'ni klonlash

### 1. Repository'ni yuklab olish:
```bash
# HTTPS orqali
git clone https://github.com/username/repository-name.git

# SSH orqali
git clone git@github.com:username/repository-name.git
```

### 2. Ma'lum branch'ni klonlash:
```bash
# Faqat ma'lum branch'ni klonlash
git clone -b branch-name https://github.com/username/repository-name.git
```

---

## 🔷 Fork va Pull Request

### 1. Repository'ni fork qilish:
- GitHub'da repository sahifasiga boring
- "Fork" tugmasini bosing
- O'zingizning hisobingizga nusxalangan

### 2. Fork'ni klonlash:
```bash
# Fork'ni klonlash
git clone https://github.com/your-username/repository-name.git

# Original repository'ni qo'shish
git remote add upstream https://github.com/original-owner/repository-name.git
```

### 3. Pull Request yaratish:
```bash
# Yangi branch yaratish
git checkout -b feature/yangi-funksiya

# O'zgarishlar qilish
echo "Yangi funksiya" > new_feature.txt

# Commit va push
git add .
git commit -m "Yangi funksiya qo'shildi"
git push origin feature/yangi-funksiya
```

---

## 🔷 GitHub'da ishlash

### 1. Issue yaratish:
- Repository sahifasida "Issues" bo'limiga boring
- "New issue" tugmasini bosing
- Muammo yoki taklifni yozing

### 2. Code Review:
- Pull Request'da "Files changed" bo'limini ko'ring
- Har bir o'zgarishni tekshiring
- Comment yozing

### 3. Repository sozlamalari:
- "Settings" bo'limiga boring
- Repository nomini o'zgartiring
- Description qo'shing
- Topics qo'shing

---

## 📋 GitHub workflow

### 1. Oddiy workflow:
```bash
# 1. Repository'ni klonlash
git clone https://github.com/username/repo.git

# 2. Yangi branch yaratish
git checkout -b feature/yangi-funksiya

# 3. O'zgarishlar qilish
# Fayllarni o'zgartiring

# 4. Commit qilish
git add .
git commit -m "Yangi funksiya qo'shildi"

# 5. Push qilish
git push origin feature/yangi-funksiya

# 6. Pull Request yaratish (GitHub'da)
```

### 2. Jamoa bilan ishlash:
```bash
# O'zgarishlarni yuklab olish
git pull origin main

# Conflict'ni hal qilish (agar bor bo'lsa)
# Fayllarni o'zgartiring

# Commit va push
git add .
git commit -m "Conflict hal qilindi"
git push origin main
```

---

## 📌 Asosiy buyruqlar jadvali

| Buyruq | Ma'nosi | Misol |
|--------|---------|-------|
| `git remote add` | Remote qo'shish | `git remote add origin URL` |
| `git push` | O'zgarishlarni yuklash | `git push origin main` |
| `git pull` | O'zgarishlarni yuklab olish | `git pull origin main` |
| `git clone` | Repository'ni klonlash | `git clone URL` |
| `git fetch` | Ma'lumotlarni yuklab olish | `git fetch origin` |

---

## 🎯 Dars yakunida bilishingiz kerak:

✅ GitHub tushunchasi va afzalliklari  
✅ Remote repository bilan ishlash  
✅ Push va pull jarayoni  
✅ Fork va Pull Request  
✅ Jamoa bilan ishlash  

---

## 📚 Keyingi dars:
[Lesson 05 — Advanced Git buyruqlari](../lesson_05/lesson.md)

---

## 🎯 Uy vazifasi:
1. GitHub'da hisob yarating
2. Yangi repository yarating
3. Local repository'ni GitHub'ga ulang
4. O'zgarishlarni push qiling
5. README faylini yangilang 