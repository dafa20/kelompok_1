# LAPORAN MODUL 4

NOVANDY PRAKOSO 1202190057 || DAFA SEPTIANDRI 1202192033

- Buat 2 salinan dari setiap container, lalu klik start untuk masing masing container

  

  ![1](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\1.png)

  

- Masuk ke 'ubuntu_php7.4_2', lalu ubah IP address menjadi '10.0.3.111' agar berbeda dengan 'ubuntu_php7.4'. Sama seperti 'ubuntu_php7.4_3' ubah alamat IP menjadi '10.0.3.123' 

  

  ![2](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\2.png)

  

  - Go to etc/hosts to register 'lxc_php7_2.dev

  ![3](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\3.png)

  

- Ganti Nama Server 

   ![4](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\4.png)

  

- restart nginx lalu curl lxc_php7_2.dev  

  ![5](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\5.png)

  - ulangi step yang sama pada ubuntu_php7.4_3

- Sama seperti ubuntu_php7.4 kita harus memulai semua container 

  ![6](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\6.png)

  

-   Buka 'debian_php5.6_2' dan ubah alamat IP menjadi '10.0.3.112'. Hal yang sama untuk 'debian_php5.6_3' ubah alamat IP menjadi '10.0.3.122

  ![7](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\7.png)

  

-  Register 'lxc_php5_2.dev' at /etc/hosts

  ![8](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\8.png)

  

-  ubah nama server, lalu ulangi langkah yang sama untuk 'debian_php5.6_3'. jangan lupa restart containernya

  ![9](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\9.png)

  

-  Daftarkan semua kontainer di /etc/hosts (di vm

  ![15](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\15.png)

  

- Jalankan jmeter. Ubah jumlah utas dari akses pengguna dari 50, 100, 150

  ![16](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\16.png)

  ![17](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\17.png)

  ![18](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\18.png)

  ![19](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\19.png)

   ![20](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\20.png)

  ![21](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\21.png)

  ![22](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\22.png)

  ![23](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\23.png)

  ![24](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\24.png)

  ![25](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\25.png)

  ![26](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\26.png)

  ![27](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\27.png)

   

  ##### Kemudian kami kembali ke VM daripada pergi ke 

- Lalu kita Tambahkan upstream landing  , php5, dan php7

  ![28](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\28.png)

  

-  ubah proxy_pass

  ![29](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\29.png)

   

-  Lalu kita kembali ke jmeter dan mengulangi lagi

  ![30](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\30.png)

  ![31](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\31.png)

  ![32](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\32.png)

  ![33](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\33.png)

  ![34](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\34.png)

  ![35](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\35.png)

  ![36](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\36.png)

  ![37](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\37.png)

  ![38](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\38.png)

  ![39](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\39.png)

  ![40](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\40.png)

  ![41](C:\Users\owner\Downloads\Modul 4 SAS\Modul 4 SAS\41.png)

 

#####  ANALISI

-  Di bawah ini adalah hasil dari saat kita menggunakan load balancer dan tidak menggunakan load balancer

  

-  Ketika ada 50 pengguna yang mengakses web kami, jika kami tidak menggunakan penyeimbang beban rata-rata waktu pengguna mengakses web kami adalah

  - landing : 2444 ms / 2.4 s
  - blog : 2347 ms / 2.3 s
  - app : 19 ms / 0.019 s

-   Saat kita menggunakan penyeimbang beban, maka

  - landing : 1841 ms / 1.8 s
  - blog : 1379 ms / 1.3 s
  - app : 12 ms / 0.012

  

- Disini kita dapat mengetahui bahwa rata-rata waktu user mengakses web kita lebih cepat dibandingkan jika kita tidak menggunakan load balancer. Untuk throughput atau jumlah pengguna yang mengakses web kami adalah

  

-  Ketika ada 50 pengguna yang mengakses web kami, jika kami tidak menggunakan penyeimbang beban, jumlah pengguna yang mengakses web kami adalah

  - landing : 16 user / second
  - blog : 12 user / second
  - app : 22 user / second

-  Saat kita menggunakan penyeimbang beban, maka

  - landing : 42 user / second

  - blog : 29 user / second

  - app : 30 user / second

    

- Di sini kita dapat mengetahui bahwa rata-rata waktu pengguna mengakses web kita dalam 1 detik lebih cepat daripada jika kita tidak menggunakan load balancer.

  Kesimpulannya, jika kita menggunakan load balancer, maka waktunya lebih cepat dan jumlah user yang mengakses web kita jauh lebih banyak daripada jika kita tidak menggunakan load balancer.