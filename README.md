# Setup Instalasi Kong API Gateway

## Instalasi Kong dan Komponen Tambahan

Pertama-tama, Anda perlu menginstal Kong dan komponen tambahan yang diperlukan. Berikut langkah-langkahnya:

1. **Install Kong:**

   - Ikuti petunjuk instalasi yang tersedia di [dokumentasi resmi Kong](https://docs.konghq.com/gateway/latest/install/).

2. **Buat Plugin dan Jaringan:**

   - Setelah menginstal Kong, Anda dapat membuat plugin dan jaringan sesuai kebutuhan dengan menggunakan perintah-perintah seperti `kong plugin`, `kong network`, dll.

## Install Layanan Contoh Echo

Setelah menginstal Kong, Anda dapat menguji layanan dengan menginstal layanan contoh Echo. Langkah-langkahnya adalah sebagai berikut:

1. **Install layanan contoh Echo:**

   - Ikuti panduan yang tersedia di [dokumentasi Echo](https://github.com/labstack/echo) atau pilih alternatif lain yang sesuai dengan kebutuhan Anda.

## Membuat Rate Limit dan Anotasi ke Layanan Echo

Setelah menginstal layanan Echo, Anda dapat menerapkan pembatasan kecepatan (rate limit) dan anotasi ke layanan tersebut dengan langkah-langkah berikut:

1. **Terapkan rate limit dan anotasi ke layanan Echo:**

   ```bash
   kubectl annotate service echo konghq.com/plugins=rate-limit-5-min --overwrite
2. **Uji rate limit ke layanan Echo:**

   ```bash
   $env:PROXY_IP = "localhost:80"
   ```
   ```bash
   foreach ($i in 1..6) {
       Invoke-WebRequest -Uri "http://$env:PROXY_IP/echo" -UseBasicParsing -Method Get | Select-Object -ExpandProperty Headers
   }
   ```
3. **Tambahkan key-auth ke layanan Echo:**
   ```bash
   kubectl annotate service echo konghq.com/plugins=rate-limit-5-min,key-auth --overwrite
   ```
   ```bash
   Invoke-WebRequest -Uri "http://$env:PROXY_IP/echo" -Headers @{ "apikey" = "hello_world" }
   ```

## Berikut beberapa perintah Kubernetes (K8s) yang mungkin berguna:

**list panggilan pada k8s**
 - kubectl get pods
 - kubectl get deployment -A
 - kubectl get httproute
 - kubectl get svc

## Jika Anda mengalami kesalahan saat melakukan pull dari repository:

```bash
kubectl rollout restart deployment nama-deployment
```
## Untuk melihat semua objek Kong yang ada di namespace kong:

```bash
kubectl get all -n kong
```
