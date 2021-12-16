# Praktikum Modul 3

### Sistem Administrasi Server

##### Kelompok 1:

- ##### Novandy Prakoso (1202190057)

- ##### Dafa Septiandri Dwinanda P. (1202192033)

### Persoalan 

1. ##### Buat subdomain dev.vm.local dengan menggunakan ansible dengan beberapa aturan:

   - Menggunakan Ansible
   - Menggunakan lxc yang sma dengan yang digunakan dengan vm.local
   - folder code harus berbeda dengan yang digunakan vm.local, menggunakan /
   - var/www/html/dev/{nama_app}

2. #####  Mendaftarkan subdomain vm.local ke DNS

### Pemecahan Masalah

- Langkah pertama buat file direktori pada ansible untuk instalasi bind9 dan dnsutils

  ```markdown
  cd ansible/laravel/
  nano sublaravel.yml 
  ```

  ![1](https://user-images.githubusercontent.com/93079538/146402547-d7263a9c-647a-48e3-a949-79002689e7e0.png)

  ```markdown
  ---
  - hosts: all
    become : yes
    tasks:
      - name: install bind9 dan dnsutils
        apt:
         pkg:
           - bind9
           - dnsutils
  ```

- lakukan instalasi

  ![2](https://user-images.githubusercontent.com/93079538/146402592-3c559b74-d982-404c-ac0d-adbfa4b53b0a.png)

- Langkah selanjutnya buat file baru lagi untuk konfigurasi (disini kita menggunakan file *config1.yml*)

  ![12](https://user-images.githubusercontent.com/93079538/146402633-c66e5546-9b84-469e-9d61-43533da65963.png)

  ```markdown
  ---
  - hosts: all
    become : yes
    tasks:
     - name: membuat direktori
       file:
        path: /var/www/html/dev/landing
        state: directory
     - name: copy file vm.local
       copy:
        src: /etc/bind/vm/vm.local
        dest: /var/www/html/dev/landing
     - name: mengganti konfigurasi
       replace:
        path: /var/www/html/dev/landing/vm.local
        regexp: 'www'
        replace: 'dev'
     - name: copy file named.conf.local
       copy:
        src: /etc/bind/named.conf.local
        dest: /etc/bind/named.conf.local
     - name: mengganti konfigurasi conf local
       replace:
        path: /etc/bind/named.conf.local
        regexp: '/etc/bind/vm/vm.local'
        replace: '/var/www/html/dev/landing/vm.local'
     - name: mengganti konfigurasi conf local part2
       replace:
        path: /etc/bind/named.conf.local
        regexp: '/etc/bind/vm/115.168.192.in-addr.arpa'
        replace: '/var/www/html/dev/landing/115.168.192.in-addr.arpa'
     - name: copy file 115.168.192.in-addr.arpa
       copy:
        src: /etc/bind/vm/115.168.192.in-addr.arpa
        dest: /var/www/html/dev/landing
     - name: copy file resolv.conf
       copy:
        src: /etc/resolv.conf
        dest: /etc/resolv.conf
     - name: copy file named.conf.options
       copy:
        src: /etc/bind/named.conf.options
        dest: /etc/bind/named.conf.options
     - name: restart nginx
       service:
        name: nginx
        state: restarted
     - name: restart bind9
       action: service name=bind9 state=restarted
  ```

- Lakukan instalasi

  ![3](https://user-images.githubusercontent.com/93079538/146402698-ced67432-5642-4fba-adf4-b27299e6b506.png)

  

- Selanjutnya tambahkan subdomain di file *hosts* dan *lxc_landing.dev*

  ![4](https://user-images.githubusercontent.com/93079538/146402730-b9c5001b-c763-489c-98a6-874484afbfa9.png)

- Lalu buka file vm.local dan edit seperti gambar berikut

  ![5](https://user-images.githubusercontent.com/93079538/146402794-7f207cbf-da56-4dbe-972f-3735a796745f.png)

  ![6](https://user-images.githubusercontent.com/93079538/146402822-7e6fec4f-28e6-41c5-bba0-d77c61c58631.png)

- buka dan edit *vm.local* pada direktori */etc/nginx/sites-enabled/*

  ![7](https://user-images.githubusercontent.com/93079538/146402866-d365c3e3-4e13-44e9-be30-88eef4427625.png)

  

- buka dan edit *vm.local* pada direktori */etc/bind/vm/*

  ![8](https://user-images.githubusercontent.com/93079538/146402906-b8d737a2-7ab8-45ea-99ac-1a68b5462e86.png)

- lalu restart semua *packages*

  ![9](https://user-images.githubusercontent.com/93079538/146402938-86974247-5358-4c89-b653-4189b3840b73.png)

- Kemudian buka control panel, network & setting, lalu setting manual dns server sesuai dengan IP VM kita pada menu IPv4

  ![10](https://user-images.githubusercontent.com/93079538/146402956-869c4064-4482-4aaf-85e2-4e76f24e0429.png)

- Kemudian buka dev.vm.local pada browser dan selesai

  ![11](https://user-images.githubusercontent.com/93079538/146402988-22bb3018-766e-4dfc-9009-20d6cd026061.png)
