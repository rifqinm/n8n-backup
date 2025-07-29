# 🧠 n8n Backup & Restore (Windows Edition)

Backup & restore workflow sederhana untuk `n8n` self-hosted yang dijalankan via Docker Compose di Windows.

---

## 📁 Struktur Direktori

n8n/
├── docker-compose.yml
├── backup_n8n/ # Folder untuk menyimpan hasil backup
├── n8n_data/ (optional) # Jika pakai bind mount lokal
└── README.md

yaml

---

## 🔄 Backup (Volume → Folder)

Backup data dari volume Docker `n8n_n8n_data` ke folder `backup_n8n`:

```powershell
docker run --rm `
  -v n8n_n8n_data:/data `
  -v "C:/Users/WIN10/OneDrive/Documents/App/App - n8n/n8n/backup_n8n:/backup" `
  alpine sh -c "cp -r /data/* /backup"
```
📦 Hasil backup akan disimpan di folder backup_n8n.

♻️ Restore (Folder → Volume)
Restore data ke dalam volume Docker dari folder backup:
```
docker run --rm `
  -v n8n_n8n_data:/data `
  -v "${PWD}/backup_n8n:/backup" `
  alpine sh -c "cp -r /backup/* /data"
```
Restart Docker Compose agar n8n memuat ulang data:
```
docker compose down
docker compose up -d
```
🔐 Fix Permission (WAJIB setelah restore)
Jika muncul error seperti EACCES: permission denied, lakukan perbaikan permission:
```
docker run --rm -it -v n8n_n8n_data:/data alpine sh
```
Di dalam container:
```
chown -R 1000:1000 /data
chmod -R u+rwX /data
```
```
exit
```
Kemudian jalankan ulang:
```
docker compose up -d
