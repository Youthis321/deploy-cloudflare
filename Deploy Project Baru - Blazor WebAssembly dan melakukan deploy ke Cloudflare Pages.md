Berikut adalah langkah-langkah yang lebih rapi dan disertai dengan penjelasan untuk membuat aplikasi To-Do List menggunakan **Blazor WebAssembly** dan melakukan **deploy ke Cloudflare Pages**.

---

## **1. Membuat Proyek Blazor WebAssembly**
Blazor WebAssembly memungkinkan kita membuat aplikasi web interaktif dengan .NET yang berjalan di browser menggunakan WebAssembly.

```sh
dotnet new blazorwasm -o TodoList
```
- **`dotnet new blazorwasm`** → Membuat proyek Blazor WebAssembly.
- **`-o TodoList`** → Menentukan nama folder proyek sebagai **TodoList**.

Setelah perintah dijalankan, masuk ke folder proyek:
```sh
cd TodoList
```

---

## **2. Menambahkan Komponen Todo**
Komponen ini akan menangani daftar tugas (To-Do List).

```sh
dotnet new razorcomponent -n Todo -o Pages
```
- **`dotnet new razorcomponent`** → Membuat komponen **Razor**.
- **`-n Todo`** → Menentukan nama komponen sebagai **Todo**.
- **`-o Pages`** → Menyimpan komponen di folder **Pages**.

---

## **3. Menjalankan Aplikasi di Lokal**
Setelah proyek dibuat dan komponen ditambahkan, jalankan aplikasi dengan:

```sh
dotnet run
```
- **Blazor WebAssembly** akan dikompilasi dan dijalankan secara lokal.
- Akses aplikasi di **http://localhost:5000** atau port lain yang ditentukan.

---

## **4. Build dan Deploy ke Cloudflare Pages**
### **A. Build Proyek**
Blazor WebAssembly adalah aplikasi **statik**, sehingga perlu di-build sebelum di-deploy.

```sh
dotnet publish -c Release -o output
```
- **`dotnet publish`** → Membangun aplikasi untuk deployment.
- **`-c Release`** → Menggunakan konfigurasi **Release** untuk optimalisasi.
- **`-o output`** → Menyimpan hasil build ke dalam folder **output**.

---

### **B. Menyiapkan Repository untuk Deploy**
Setelah aplikasi di-build, buat repository **deploy-blazor** untuk menyimpan file statis.

```sh
mkdir deploy-blazor
cd deploy-blazor
git init
```
- **`mkdir deploy-blazor`** → Membuat folder baru untuk deployment.
- **`cd deploy-blazor`** → Masuk ke folder tersebut.
- **`git init`** → Menginisialisasi repository Git.

Salin hasil build dari **wwwroot** ke folder ini:
```sh
cp -r ../output/wwwroot/* .
```

Tambahkan file ke repository Git:
```sh
git add .
git commit -m "Deploy Blazor WebAssembly"
```

Hubungkan ke GitHub dan push ke repository:
```sh
git branch -M main
git remote add origin https://github.com/USERNAME/NAMA-REPO.git
git push -u origin main
```
- **Ganti `USERNAME` dan `NAMA-REPO`** dengan nama akun dan repository GitHub.

---

### **C. Deploy ke Cloudflare Pages**
1. **Buka [Cloudflare Pages](https://pages.cloudflare.com/)**.
2. Klik **"Create a project"**.
3. Pilih repository **deploy-blazor** yang baru saja dibuat.
4. **Atur konfigurasi build**:
   - **Framework Preset** → Pilih **None**.
   - **Build Command** → **(Kosongkan, karena sudah di-build secara lokal)**.
   - **Build Output Directory** → Isi dengan **`.`** (root directory).
5. Klik **"Save and Deploy"**.

Cloudflare Pages akan meng-host aplikasi Blazor WebAssembly sebagai **static site**.

---

Sekarang aplikasi To-Do List dengan **Blazor WebAssembly** sudah ter-deploy di Cloudflare Pages! 🚀
