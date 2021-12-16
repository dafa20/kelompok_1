# Praktikum Modul 3

### Sistem Administrasi Server

##### Kelompok 1:

- ##### Novandy Prakoso (1202190057)

- ##### Dafa Septiandri Dwinanda P. (1202192033)

###### Persoalan 

1. ###### Buat subdomain dev.vm.local dengan menggunakan ansible dengan beberapa aturan:

   - Menggunakan Ansible
   - Menggunakan lxc yang sma dengan yang digunakan dengan vm.local
   - folder code harus berbeda dengan yang digunakan vm.local, menggunakan /
   - var/www/html/dev/{nama_app}

2. ######  Mendaftarkan subdomain vm.local ke DNS

###### Pemecahan Masalah

- Langkah pertama buat file direktori pada ansible untuk instalasi bind9 dan dnsutils

  ```markdown
  cd ansible/laravel/
  nano sublaravel.yml 
  ```

  ![1](C:\Users\Novandy\Downloads\SS SAS 2\modul 3\1.png)

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

  ![2](C:\Users\Novandy\Downloads\SS SAS 2\modul 3\2.png)

- Langkah selanjutnya buat file baru lagi untuk konfigurasi (disini kita menggunakan file *config1.yml*)

  ![12](C:\Users\Novandy\Downloads\SS SAS 2\modul 3\12.png)

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

  ![3](C:\Users\Novandy\Downloads\SS SAS 2\modul 3\3.png)

  

- Selanjutnya tambahkan subdomain di file *hosts* dan *lxc_landing.dev*

  ![4](C:\Users\Novandy\Downloads\SS SAS 2\modul 3\4.png)

- Lalu buka file vm.local dan edit seperti gambar berikut

  ![5](C:\Users\Novandy\Downloads\SS SAS 2\modul 3\5.png)

  ![6](C:\Users\Novandy\Downloads\SS SAS 2\modul 3\6.png)

- buka dan edit *vm.local* pada direktori */etc/nginx/sites-enabled/*

  ![7](C:\Users\Novandy\Downloads\SS SAS 2\modul 3\7.png)

  

- buka dan edit *vm.local* pada direktori */etc/bind/vm/*

  ![8](C:\Users\Novandy\Downloads\SS SAS 2\modul 3\8.png)

- lalu restart semua *packages*

  ![9](C:\Users\Novandy\Downloads\SS SAS 2\modul 3\9.png)

- Kemudian buka control panel, network & setting, lalu setting manual dns server sesuai dengan IP VM kita pada menu IPv4

  ![10](C:\Users\Novandy\Downloads\SS SAS 2\modul 3\10.png)

- Kemudian buka dev.vm.local pada browser dan selesai

  ![11](C:\Users\Novandy\Downloads\SS SAS 2\modul 3\11.png)
