# FreeRTOS-Semaphore-LED-Control
Proyek ini menunjukkan penggunaan FreeRTOS Semaphore untuk sinkronisasi antara beberapa task dalam sistem multitasking. Program ini berfokus pada bagaimana penggunaan semaphore dapat mengatur urutan eksekusi task, khususnya dalam mengendalikan perilaku LED pada STM32F401CCU6.

Diagram Task :

![Screenshot 2024-11-17 120605](https://github.com/user-attachments/assets/8f61436f-ef1f-4106-9fb7-b93c6999653d)

Hardware yang diperlukan :
1. STM32f401CCU6
2. LED

Software yang diperlukan :
1. STM32CubeIDE
2. FreeRTOS

Cara Kerja :
1. Inisialisasi Semaphore dan Task :
   - Program dimulai dengan inisialisasi FreeRTOS dan pembuatan beberapa task serta semaphore.
   - Tugas-tugas ini berinteraksi dengan semaphore untuk mengatur akses ke critical section atau untuk sinkronisasi antar task.
     
2. Deskripsi Task :
   
   a. 'RedTask' :
   - Task ini menunggu semaphore untuk mendapatkan akses ke LED 2.
   - Jika semaphore tersedia, LED 2 akan menyala selama 500ms sebelum menyerahkan kembali semaphore.
   
   b. 'GreenTask' :
   - Task ini juga menggunakan semaphore untuk mengakses LED 1.
   - Jika semaphore tersedia, LED 1 akan menyala selama 500ms.
   
   c. 'BlueTask' :
   - Task ini hanya dapat berjalan setelah semaphore dilepas oleh task lain.
   - Menggunakan semaphore untuk mengakses LED 3, yang menyala selama 500ms.
   
   d. 'OrangeTask' :
   - Task dengan prioritas lebih tinggi yang berjalan terus-menerus tanpa bergantung pada semaphore.
   - LED 4 berkedip dengan delay 50ms.
     
4. Mekanisme Semaphore
   - Binary Semaphore digunakan untuk memastikan bahwa hanya satu task yang dapat mengakses critical section (dalam hal ini, LED) pada satu waktu.
   - Task yang tidak dapat mendapatkan semaphore akan menunggu hingga semaphore dilepas oleh task lain.
     
5. Perilaku Task :
   
   a. Urutan Eksekusi dengan Semaphore :
      - Jika semaphore tersedia, 'RedTask', 'GreenTask', atau 'BlueTask' akan mengaksesnya bergantian.
      - Task yang gagal mendapatkan semaphore akan masuk ke mode blocked state hingga semaphore dilepas.
        
   b. OrangeTask :
      - Selalu berjalan tanpa tergantung pada semaphore.
      - LED Orange berkedip cepat untuk menunjukkan bahwa task ini berjalan normal.
       
7. Siklus Kerja LED :
   - Led 'GreenTask', 'RedTask', dan 'BlueTask' menyala bergantian tanpa konflik.
   - Led 'OrangeTask' berkedip tanpa gangguan.

Ringkasan Perilaku LED :

![Screenshot 2024-11-17 154739](https://github.com/user-attachments/assets/69271358-527a-46f3-8115-62b063c9170e)


Pinout Hardware :

![Pinout Hardware FreeRTOS](https://github.com/user-attachments/assets/8b814f64-fa02-4ee5-a5e5-d6a85f395bb2)

Hasil Hardware :

![8-GIF](https://github.com/user-attachments/assets/0c34bbde-cc0e-4427-92b5-64da70665ac2)


Hasil dari proyek ini sebagai berikut :
- Led 'GreenTask', 'RedTask', dan 'BlueTask' menyala bergantian tanpa konflik.
- Led 'OrangeTask' berkedip tanpa gangguan.
   
Project ini dikerjakan di Politeknik Elektronika Negeri Surabaya dengan dosen pengampu bapak Fernando Ardilla
