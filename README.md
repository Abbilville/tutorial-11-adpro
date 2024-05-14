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
