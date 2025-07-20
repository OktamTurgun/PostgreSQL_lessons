# 📖 Git Darslari — Lesson 01: Kirish va o'rnatish

## 🎯 Maqsad
Git versiya boshqaruvi tizimi bilan tanishingiz va uni o'zbek tilida o'rganish.

---

## 📖 Git nima?

Git — bu dasturiy ta'minot loyihalarida o'zgarishlarni kuzatib borish va boshqarish uchun ishlatiladigan versiya boshqaruvi tizimi.

### Git'ning asosiy vazifalari:
- ✅ Kod o'zgarishlarini saqlash
- ✅ Loyiha tarixini kuzatib borish
- ✅ Jamoa bilan ishlash
- ✅ Xatolarni tuzatish va qaytish
- ✅ Loyiha nusxalarini boshqarish

---

## 🔧 Git o'rnatish

### Windows uchun:
1. **Git'ni yuklab olish:**
   - [Git for Windows](https://git-scm.com/download/win) sahifasiga boring
   - "Click here to download" tugmasini bosing
   - .exe faylini yuklab oling

2. **O'rnatish:**
   ```bash
   # Git o'rnatilganini tekshirish
   git --version
   ```

### macOS uchun:
```bash
# Homebrew orqali
brew install git

# Yoki Xcode Command Line Tools orqali
xcode-select --install
```

### Linux uchun:
```bash
# Ubuntu/Debian
sudo apt-get install git

# CentOS/RHEL
sudo yum install git
```

---

## 🔧 Birinchi sozlashlar

### 1. Foydalanuvchi ma'lumotlarini o'rnatish:
```bash
git config --global user.name "Sizning ismingiz"
git config --global user.email "sizning@email.com"
```

### 2. Sozlashlarni tekshirish:
```bash
git config --list
```

### 3. Git'ning asosiy buyruqlari:
```bash
# Git versiyasini ko'rish
git --version

# Yordam olish
git help
git help <buyruq_nomi>
```

---

## 📁 Repository (Loyiha) tushunchasi

### Repository turlari:
- **Local Repository** — kompyuteringizda joylashgan
- **Remote Repository** — GitHub, GitLab kabi serverlarda joylashgan

### Repository yaratish:
```bash
# Yangi repository yaratish
git init

# Mavjud repository'ni klonlash
git clone <repository_url>
```

---

## 🔷 Amaliy mashg'ulot

### 1. Yangi loyiha yaratish:
```bash
# Papka yaratish
mkdir my_first_project
cd my_first_project

# Git repository'ni ishga tushirish
git init
```

### 2. Birinchi fayl yaratish:
```bash
# README.md faylini yaratish
echo "# Mening birinchi loyiham" > README.md

# Fayl mavjudligini tekshirish
ls
cat README.md
```

### 3. Git holatini tekshirish:
```bash
# Repository holatini ko'rish
git status
```

---

## 📌 Asosiy buyruqlar

| Buyruq | Ma'nosi | Misol |
|--------|---------|-------|
| `git init` | Yangi repository yaratish | `git init` |
| `git clone` | Repository'ni nusxalash | `git clone https://github.com/user/repo.git` |
| `git status` | Holatni ko'rish | `git status` |
| `git config` | Sozlashlar | `git config --global user.name "Ism"` |

---

## 🎯 Dars yakunida bilishingiz kerak:

✅ Git nima va nima uchun kerak  
✅ Git'ni o'rnatish va sozlash  
✅ Repository tushunchasi  
✅ Asosiy buyruqlar  
✅ Terminalda ishlash  

---

## 📚 Keyingi dars:
[Lesson 02 — Birinchi commit va o'zgarishlar](../lesson_02/lesson.md)

---

## 🎯 Uy vazifasi:
1. Git'ni o'rnating
2. Foydalanuvchi ma'lumotlarini sozlang
3. Yangi repository yarating
4. README.md faylini yarating 