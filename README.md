# Tutorial-11
---
#### Nama: Abbilhaidar Farras Zulfikar
#### NPM: 2206026012
#### Kelas: Adpro A
---
### Reflection on Hello Minikube
1. **Compare the application logs before and after you exposed it as a Service.** <br>
**Sebelum**
![image](https://github.com/Abbilville/tutorial-11-adpro/assets/119837732/b313bedc-b533-46bb-aaa5-bc4df915d3f2) <br>
**Sesudah**
![](https://github.com/Abbilville/tutorial-11-adpro/assets/119837732/1611c948-45b7-49d8-8b0c-23e617bd2f13) <br>
Sebelum service diexposed, tidak ada log yang ditampilkan ketika ada browser yang dibuka. Setelah service diexposed, service mulai mendapatkan request GET. Request-request tersebut dapat dilihat dalam log seperti yang ditunjukkan pada gambar di atas.

2. **Notice that there are two versions of `kubectl get` invocation during this tutorial section. The first does not have any option, while the latter has `-n` option with value set to `kube-system`. What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created?** <br>
Perbedaan antara kedua sintaks tersebut adalah dengan menggunakan <code>-n</code>. <code>-n</code> adalah singkatan dari namespace. Ini diperlukan jika ada banyak service berbeda yang memiliki nama yang sama dan tersebar di berbagai namespace. Dengan menggunakan <code>-n</code>, kita memfokuskan perintah GET pada namespace yang kita berikan setelah query <code>-n</code>.

### Reflection on Rolling Update & Kubernetes Manifest File
1. **What is the difference between Rolling Update and Recreate deployment strategy?** <br>
Perbedaan utama antara rolling update strategy dan recreate deployment adalah bahwa dalam recreate deployment akan ada downtime antara pembaruan aplikasi karena strategi ini memerlukan penghapusan aplikasi sebelumnya terlebih dahulu dan kemudian mendistribusikan ulang aplikasi yang baru. Oleh karena itu, akan ada downtime setelah penghapusan dan penyelesaian deployment. Dibandingkan dengan rolling updates yang mengubah aplikasi secara perlahan ke versi terbarunya.

2. **Try deploying the Spring Petclinic REST using Recreate deployment strategy and document your attempt.** <br>
Melakukan recreate pada springboot-petclinic-rest yang telah discaled ke versi 3.0.2
![image](https://github.com/Abbilville/tutorial-11-adpro/assets/119837732/6d6cc8c7-ffda-4555-9cab-1896d02c942c) <br> <br>
Setelah itu kita akan memanfaatkan replikaset yang akan menggantikan pod yang dihapus dengan template-nya, ubah versi menjadi 3.2.1 dengan menjalankan perintah berikut <br>
![image](https://github.com/Abbilville/tutorial-11-adpro/assets/119837732/ddcb3232-a889-4105-bcd9-053378626859) <br> <br>
Untuk memeriksa keberhasilan perubahan, lakukan perintah berikut yang akan menghasilkan output seperti yang ditunjukkan pada gambar <br>
![image](https://github.com/Abbilville/tutorial-11-adpro/assets/119837732/9867658c-ad87-4fcb-a4bb-7a7dd6ff2253) <br> <br>
Selanjutnya delete pod yang kita miliki <br>
![image](https://github.com/Abbilville/tutorial-11-adpro/assets/119837732/3f98a648-a7c7-40a3-9ee5-81e09356f7a9) <br> <br>
Dapat dilihat bahwa pod-pod baru sedang dibuat untuk menggatikan pod yang dihapus sebelumnya <br>
![image](https://github.com/Abbilville/tutorial-11-adpro/assets/119837732/79951e2a-558b-47cd-b08a-8001c81b3dcc) <br> <br>
Saat program di-run akan muncul output seperti ini <br>
![image](https://github.com/Abbilville/tutorial-11-adpro/assets/119837732/9952ef67-1d5c-448f-b2b7-995e48151b93) <br>
![image](https://github.com/Abbilville/tutorial-11-adpro/assets/119837732/a36eab73-3460-458a-ab52-ba5e0ba892b0) <br> <br>

3. **Prepare different manifest files for executing Recreate deployment strategy.**
Buat sebuah file baru seperti yang dilampirkan di dalam github dengan nama deployment2.yaml. Isi dari file tersebut sama seperti file hasil export pada tutorial bagian sebelumnya tapi ada tambahan yaitu <br>
```yaml
 selector:
        matchLabels:
        app: spring-petclinic-rest
    strategy:
        type: Recreate
```
File tersebut dapat diimport ke Kubernetes seperti file manifes lainnya, kemudian setelah itu untuk membuktikan bahwa file manifes ini berguna, kita dapat mengubah gambar yang ada di file tersebut ke versi yang kita inginkan dimana itu akan menghapus pod di set replika lama kita dan kemudian menyebarkan pod baru di replika baru seperti yang ditunjukkan di bawah ini. <br>
![image](https://github.com/Abbilville/tutorial-11-adpro/assets/119837732/fd068e8e-54c1-420f-895f-2e017aeb35a6) <br>
![image](https://github.com/Abbilville/tutorial-11-adpro/assets/119837732/60e8247f-3878-4da4-b5f4-e2ddd3b4aafa) <br>
![image](https://github.com/Abbilville/tutorial-11-adpro/assets/119837732/17b858cf-da49-49c0-b820-991b409a6626) <br>
Sehingga terbukti update dilakukan secara recreate strategy dan bukan rolling. <br>

4. **What do you think are the benefits of using Kubernetes manifest files?** <br>
Manfaat utama menggunakan file manifest adalah efisiensi. Dengan manifest file, kita tidak perlu lagi mengingat prosedur dan sintaks yang diperlukan untuk melakukan pembaruan atau deployment awal. Ini mirip dengan mengimpor file ke dalam dokumen; kita tidak perlu tahu bagaimana dokumen tersebut terbentuk, yang penting kita sudah memiliki dokumen yang siap pakai. Selain itu, penggunaan file manifest juga mengurangi kemungkinan kesalahan manusia, karena layanan yang dibuat pasti sesuai dengan isi file tersebut, menghindari kesalahan ketik yang mungkin dilakukan oleh programmer jika mengetik sintaks satu per satu.




