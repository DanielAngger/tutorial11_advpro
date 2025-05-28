# Refleksi Tutorial 11 Adpro

## Reflection on Hello Minikube

### 1. Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?

Sebelum di-expose sebagai Service, log hanya menunjukkan pesan saat aplikasi pertama kali mulai, yaitu sebagai berikut:

I0528 15:49:34.192028       1 log.go:195] Started HTTP server on port 8080  
I0528 15:49:34.192398       1 log.go:195] Started UDP server on port  8081

Tetapi setelah di-expose sebagai Service, ada log baru yang muncul, yaitu sebagai berikut:

I0528 15:54:41.943357       1 log.go:195] GET /  
I0528 15:54:42.298240       1 log.go:195] GET /

Artinya, aplikasi telah menerima dua request HTTP GET ke path / , ini karena saya membuka aplikasi dua kali melalui browser saat proxy aktif.

### 2. Notice that there are two versions of `kubectl get` invocation during this tutorial section. The first does not have any option, while the latter has `-n` option with value set to `kube-system`. What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created?

Opsi -n NAMA_NAMESPACE biasanya digunakan untuk menspesifikkan namespace dalam Kubernetes saat menjalankan perintah seperti kubectl get atau yang lainnya, sementara namespace adalah cara untuk mengorganisasi objek (Pod, Service, Deployment, dll) ke dalam lingkungan virtual yang terpisah di dalam kluster Kubernetes yang sama. Jika kita membuat Pod atau Service tanpa menyebutkan namespace, maka Kubernetes akan membuatnya di namespace default. Namun ketika kita menggunakan -n, maka kita hanya akan melihat Pod-Pod yang dibuat di dalam namespace yang kita ketik, yaitu milik sistem Kubernetes sendiri, bukan milik aplikasi yang kita buat.