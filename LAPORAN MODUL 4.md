# LAPORAN MODUL 4

NOVANDY PRAKOSO 1202190057 || DAFA SEPTIANDRI 1202192033

- Buat 2 salinan dari setiap container, lalu klik start untuk masing masing container

  

  ![1](https://user-images.githubusercontent.com/93079538/148350925-fc4c1e97-968f-4001-8692-c5b321c98465.png)

  

- Masuk ke 'ubuntu_php7.4_2', lalu ubah IP address menjadi '10.0.3.111' agar berbeda dengan 'ubuntu_php7.4'. Sama seperti 'ubuntu_php7.4_3' ubah alamat IP menjadi '10.0.3.123' 

  

  ![2](https://user-images.githubusercontent.com/93079538/148350958-b5357439-cc08-4be6-a318-21e3ce84c0f3.png)

  

  - Go to etc/hosts to register 'lxc_php7_2.dev

  ![3](https://user-images.githubusercontent.com/93079538/148351005-d11faae5-f3f3-4d28-8bfe-de0f3d3f1d91.png)

  

- Ganti Nama Server 

   ![4](https://user-images.githubusercontent.com/93079538/148351021-252b64bf-ebc3-453f-978b-69a74529ad47.png)

  

- restart nginx lalu curl lxc_php7_2.dev  

  ![5](https://user-images.githubusercontent.com/93079538/148351044-7d5315a8-32cd-4b6e-bbf2-9df4fcec3cd5.png)



-  ulangi step yang sama pada ubuntu_php7.4_3

- Sama seperti ubuntu_php7.4 kita harus memulai semua container 

  ![6](https://user-images.githubusercontent.com/93079538/148351597-3236a928-779c-4a77-8233-ee67112c64e6.png)

  

-   Buka 'debian_php5.6_2' dan ubah alamat IP menjadi '10.0.3.112'. Hal yang sama untuk 'debian_php5.6_3' ubah alamat IP menjadi '10.0.3.122

  ![7](https://user-images.githubusercontent.com/93079538/148351621-ea5cb0e7-33e4-4515-ab7c-25d125619e2e.png)

  

-  Register 'lxc_php5_2.dev' at /etc/hosts

  ![8](https://user-images.githubusercontent.com/93079538/148351651-a62f1b47-b806-47eb-8eb5-cb96e28eb2ca.png)

  

-  ubah nama server, lalu ulangi langkah yang sama untuk 'debian_php5.6_3'. jangan lupa restart containernya

  ![9](https://user-images.githubusercontent.com/93079538/148351679-cb1b8ab2-d3d2-4dd3-aecb-f107e1cdb9f3.png)

  

-  Daftarkan semua kontainer di /etc/hosts (di vm

  ![15](https://user-images.githubusercontent.com/93079538/148351765-1a9ef34e-141e-4de5-901b-ce3b9438829f.png)

  

- Jalankan jmeter ubah number of theards dari 50, 100, 150

  ![16](https://user-images.githubusercontent.com/93079538/148351807-8a3b9b2c-a14b-40a2-9ec2-421879807679.png)

  ![17](https://user-images.githubusercontent.com/93079538/148351831-4d5b9208-e104-49b1-9f4f-4de9727db57b.png)

  ![18](https://user-images.githubusercontent.com/93079538/148351857-ac3dd9b9-33a2-4eb6-a973-aa926c29d408.png)

  ![19](https://user-images.githubusercontent.com/93079538/148351871-b12e3ddb-30a4-4ced-ba1d-4ab04d95b30c.png)

   ![20](https://user-images.githubusercontent.com/93079538/148351926-a18d73e0-2666-493c-92b7-00ed5598685c.png)

  ![21](https://user-images.githubusercontent.com/93079538/148351937-7083dcdc-e257-467e-9065-77d1c04452de.png)

  ![22](https://user-images.githubusercontent.com/93079538/148351952-8a173967-a62e-45b3-9a84-eece4e881761.png)

  ![23](https://user-images.githubusercontent.com/93079538/148351970-2aee2c68-174d-4fd6-9ba6-4e4b953418da.png)

  ![24](https://user-images.githubusercontent.com/93079538/148351990-c3cd4bfc-d6aa-4453-add2-245aa89cef5e.png)

  ![25](https://user-images.githubusercontent.com/93079538/148352009-c527264a-3226-4bc2-a5b8-436303d5c54b.png)

  ![26](https://user-images.githubusercontent.com/93079538/148352035-a141fdb4-a013-44e7-9da3-8fa0b1fc8ed2.png)

  ![27](https://user-images.githubusercontent.com/93079538/148352064-a7cb78ae-4a36-463a-9f3d-68b493d1efc4.png)

   

  ##### Kemudian kami kembali ke VM daripada pergi ke 

- Lalu kita Tambahkan upstream landing  , php5, dan php7

  ![28](https://user-images.githubusercontent.com/93079538/148352084-06572486-1bb6-43d5-b576-df0319c3ffec.png)

  

-  ubah proxy_pass

  ![29](https://user-images.githubusercontent.com/93079538/148352101-ef33001a-2eee-4ef3-a67c-e575efd7829f.png)

   

-  Lalu kita kembali ke jmeter dan mengulangi lagi

  ![29](https://user-images.githubusercontent.com/93079538/148352124-44adb5f9-5fab-47b7-bb8a-eae9d918fcb7.png)

  ![31](https://user-images.githubusercontent.com/93079538/148352148-712a2ca4-2533-4057-95a1-bb8872f61c39.png)

  ![32](https://user-images.githubusercontent.com/93079538/148352198-13d53dab-e92e-4b69-8d17-6748783bf44c.png)

  ![33](https://user-images.githubusercontent.com/93079538/148352211-4b65d73b-ab7c-45b1-8837-87677559a909.png)

  ![34](https://user-images.githubusercontent.com/93079538/148352236-9808b2e1-9dfd-4560-bde7-73100fabe033.png)

  ![35](https://user-images.githubusercontent.com/93079538/148352254-cde16b5c-52b4-494e-bd4a-472cca8ee5de.png)

  ![36](https://user-images.githubusercontent.com/93079538/148352270-94532614-ae2d-4e3e-9843-6b09c80ed062.png)

  ![37](https://user-images.githubusercontent.com/93079538/148352278-05a1fff1-02c6-4840-adf5-6804d31114b0.png)

  ![38](https://user-images.githubusercontent.com/93079538/148352289-61740cf7-ef32-4f14-9b36-513cf250c224.png)

  ![39](https://user-images.githubusercontent.com/93079538/148352302-aade1fee-c88e-47e8-b81b-eb51f58b2b10.png)

  ![40](https://user-images.githubusercontent.com/93079538/148352318-d4fb4b46-a155-4e38-93d3-60eead1d8d5a.png)

  ![41](https://user-images.githubusercontent.com/93079538/148352332-b9b73802-9339-47d5-8c0e-06ac5dc41f08.png)

 

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
