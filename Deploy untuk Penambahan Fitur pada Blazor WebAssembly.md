Berikut adalah versi yang telah dirapikan dan diberi deskripsi dari proses **deploy untuk penambahan fitur pada proyek Blazor WebAssembly**:  

---

# **Deploy untuk Penambahan Fitur pada Blazor WebAssembly**  

## **1. Buka Proyek di VS Code**  
```sh
cd D:\code-c\TodoList
code .
```
- **`cd D:\code-c\TodoList`** → Masuk ke folder proyek.  
- **`code .`** → Membuka proyek di **VS Code**.  

---

## **2. Tambahkan atau Edit Fitur**  
- Lakukan perubahan pada file yang diperlukan di dalam proyek.  
- Simpan semua perubahan sebelum melanjutkan ke langkah berikutnya.  

---

## **3. Membersihkan Cache Build Lama**  
```sh
dotnet clean
```
- Menghapus hasil build sebelumnya untuk menghindari konflik saat **publish ulang**.  

---

## **4. Build dan Publish Proyek**  
```sh
dotnet publish TodoList.csproj -c Release -o output
```
- **`-c Release`** → Menggunakan mode **Release** untuk optimasi.  
- **`-o output`** → Menyimpan hasil build ke dalam folder **output**.  

---

## **5. Mengatasi Error Jika Build Gagal**  
Jika terjadi error, periksa apakah ada **instance Blazor WebAssembly** yang masih berjalan:  

```sh
tasklist | findstr dotnet
```
Jika ada proses **`dotnet.exe`**, hentikan dengan:  

```sh
taskkill /F /IM dotnet.exe
```
Kemudian, jalankan ulang perintah publish:  

```sh
dotnet publish TodoList.csproj -c Release -o output
```

---

## **6. Menyiapkan Folder Deploy**  
Karena sebelumnya sudah ada file di dalam `deploy-blazor`, kita perlu membersihkannya:  

```sh
Remove-Item -Recurse -Force deploy-blazor/*
```
Kemudian, salin hasil build terbaru ke dalam folder **deploy-blazor**:  

```sh
cp -r output/wwwroot/* deploy-blazor/
```

---

## **7. Commit dan Push ke Repository Git**  
Setelah semua file terbaru disalin, lakukan **commit dan push ke GitHub**:  

```sh
cd deploy-blazor
git add .
git commit -m "Deploy Blazor WebAssembly"
git push origin main
```
- **`git add .`** → Menambahkan semua perubahan.  
- **`git commit -m`** → Menyimpan perubahan dengan pesan **"Deploy Blazor WebAssembly"**.  
- **`git push origin main`** → Mengirim perubahan ke **GitHub**.  

---

## **8. Deploy ke Cloudflare Pages (Jika Perlu)**  
1. **Buka [Cloudflare Pages](https://pages.cloudflare.com/)**.  
2. Klik **"Create a project"** (jika belum dibuat).  
3. Pilih repository **deploy-blazor**.  
4. **Atur konfigurasi build**:  
   - **Framework Preset** → Pilih **None**.  
   - **Build Command** → **(Kosongkan, karena sudah di-build secara lokal)**.  
   - **Build Output Directory** → Isi dengan **`.`** (root directory).  
5. Klik **"Save and Deploy"**.  

Setelah ini, aplikasi Blazor WebAssembly terbaru akan **online** dengan fitur yang telah diperbarui. 🚀  

---

Semoga panduan ini membantu! Jika ada tambahan atau kendala, silakan tanyakan. 😊
