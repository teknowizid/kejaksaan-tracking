# 🖥️ Platform Build Guide - E-Kejaksaan Desktop App

## ⚠️ PENTING: Cross-Platform Build

PyInstaller **TIDAK BISA** cross-compile. Artinya:

| Build di | Hasil |
|----------|-------|
| 🪟 Windows | ✅ `.exe` untuk Windows |
| 🐧 Linux | ✅ Executable untuk Linux |
| 🍎 macOS | ✅ `.app` untuk macOS |

**Kesimpulan:** Untuk build `.exe` Windows, **HARUS** build di Windows!

---

## 📋 Skenario Build

### Skenario 1: Anda di Windows ✅
```bash
# Langsung build
python build_exe.py

# Hasil: dist/E-Kejaksaan.exe (Windows executable)
```

### Skenario 2: Anda di Linux (Sekarang) ⚠️

**Opsi A: Build untuk Linux (Testing)**
```bash
# Build executable Linux
python3 build_exe.py
# Ketik 'y' untuk lanjut

# Hasil: dist/E-Kejaksaan (Linux executable)
# Bisa dijalankan di Linux, TIDAK bisa di Windows
```

**Opsi B: Build .exe Windows (Recommended)**

Ada 3 cara:

#### 1. Dual Boot / Windows PC 🎯 (Paling Mudah)
```bash
# Di Windows:
1. Clone repo
2. Install Python 3.8+
3. pip install -r requirements.txt
4. Copy file .env dari Linux
5. python build_exe.py
```

#### 2. Virtual Machine (VirtualBox/VMware)
```bash
# Install Windows di VM
1. Install VirtualBox
2. Install Windows 10/11
3. Share folder project ke VM
4. Build di dalam VM
```

#### 3. Wine (Tidak Recommended)
```bash
# Jalankan Python Windows di Linux pakai Wine
# Kompleks dan sering error, tidak direkomendasikan
```

---

## 🚀 Recommended Workflow

### Untuk Development (Linux/macOS)
```bash
# Jalankan sebagai web app
python3 app.py

# Atau desktop app (tanpa build)
python3 desktop.py
```

### Untuk Production (Windows .exe)
```bash
# Build di Windows PC/VM
python build_exe.py

# Distribusi .exe ke user
```

---

## 🔄 Alternative: Web App Deployment

Jika tidak punya akses Windows, deploy sebagai web app:

### Opsi 1: Vercel (Serverless)
```bash
# Deploy ke Vercel (gratis)
vercel deploy

# User akses via browser
# Tidak perlu install apapun
```

### Opsi 2: Docker Container
```bash
# Build Docker image
docker build -t kejaksaan-app .

# Run container
docker run -p 5000:5000 kejaksaan-app

# User akses via browser di network lokal
```

### Opsi 3: Heroku/Railway
```bash
# Deploy ke cloud platform
# User akses via URL
```

---

## 📊 Comparison

| Method | Pros | Cons |
|--------|------|------|
| **Windows .exe** | ✅ Native app<br>✅ No browser<br>✅ Offline UI | ❌ Need Windows to build<br>❌ Large file size (~50MB) |
| **Linux executable** | ✅ Native app<br>✅ Easy to build | ❌ Only for Linux users<br>❌ Not common in offices |
| **Web App** | ✅ Cross-platform<br>✅ Easy deploy<br>✅ Auto-update | ❌ Need browser<br>❌ Need server |
| **Docker** | ✅ Consistent environment<br>✅ Easy deploy | ❌ Need Docker installed<br>❌ More complex |

---

## 💡 Recommendation

### Untuk Kantor Kejaksaan (Windows Users)

**Best Solution:**
1. Cari 1 PC Windows (bisa pinjam teman/kantor)
2. Build `.exe` sekali saja
3. Distribusi `.exe` ke semua user
4. Update: Build ulang di Windows jika ada perubahan

**Alternative:**
- Deploy sebagai web app (Vercel/Heroku)
- User akses via browser
- Tidak perlu build .exe

---

## 🛠️ Build di Windows (Step by Step)

### 1. Persiapan
```bash
# Install Python 3.8+ dari python.org
# Download: https://www.python.org/downloads/

# Cek instalasi
python --version
```

### 2. Clone Project
```bash
# Clone dari GitHub
git clone https://github.com/ghofur135/kejaksaan-tracking.git
cd kejaksaan-tracking
```

### 3. Setup Environment
```bash
# Buat virtual environment
python -m venv venv

# Activate venv
venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 4. Copy .env File
```bash
# Copy .env dari Linux atau buat baru
# Isi dengan DATABASE_URL dan SECRET_KEY
```

### 5. Build
```bash
# Build .exe
python build_exe.py

# Hasil: dist/E-Kejaksaan.exe
```

### 6. Test
```bash
# Test .exe
cd dist
E-Kejaksaan.exe
```

### 7. Distribusi
```bash
# Copy E-Kejaksaan.exe ke user
# User tinggal double-click
```

---

## 🐛 Troubleshooting

### Error: "pyinstaller not found" (Windows)
```bash
pip install pyinstaller
```

### Error: "pywebview not found" (Windows)
```bash
pip install pywebview
```

### Error: Build di Linux menghasilkan file tanpa .exe
```
Normal! Di Linux tidak ada .exe
File executable: dist/E-Kejaksaan (tanpa extension)
Untuk .exe, build di Windows
```

### Error: .exe tidak jalan di Windows
```bash
# Install Visual C++ Redistributable
# Download: https://aka.ms/vs/17/release/vc_redist.x64.exe
```

---

## 📞 Support

Jika kesulitan build di Windows:
1. Cek dokumentasi: `docs/CARA_BUILD_EXE.txt`
2. Test setup: `python test_build_setup.py`
3. Atau deploy sebagai web app (lebih mudah)

---

## 🎯 Quick Decision Guide

**Punya akses Windows?**
- ✅ Yes → Build .exe di Windows
- ❌ No → Deploy sebagai web app

**User butuh offline app?**
- ✅ Yes → Harus build .exe (butuh Windows)
- ❌ No → Web app sudah cukup

**Butuh update sering?**
- ✅ Yes → Web app lebih praktis
- ❌ No → .exe lebih nyaman untuk user
