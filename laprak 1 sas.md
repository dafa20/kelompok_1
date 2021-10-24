# <u>Laporan Praktikum Modul 1</u>

## **Sistem Administrasi Server**

###### Nama Kelompok :

- <u>Novandy Prakoso (1202190057)</u>
- <u>Dafa Septiandri Dwinanda Prabowo (1202192033)</u>



###### 1. Rename ubuntu_php5.6 menjadi ubuntu_landing, serta rubah IP mengikuti skema baru
- Mengecek LXC, lalu rename ubuntu_php5.6 menjadi ubuntu_landing 

```markdown
sudo lxc -ls -f
sudo lxc-copy -R ubuntu_php5.6 -N ubuntu_landing
```

![1](https://user-images.githubusercontent.com/93079538/138592515-0fe059ae-6bb1-4ff3-97e7-5629d6f263dd.PNG)
- Start ubuntu_landing

![1 1](https://user-images.githubusercontent.com/93079538/138592512-b7525368-8b39-4d94-be48-e9eb4eac0139.PNG)
- Set up static IP pada ubuntu_landing

```markdown
sudo nano /etc/network/interfaces
```

![1 2](https://user-images.githubusercontent.com/93079538/138592513-d2a85a9e-f08b-4a47-b701-e95918c39b7b.PNG)

```markdown
reboot
ifconfig
```

![1 3](https://user-images.githubusercontent.com/93079538/138592514-291442d0-0e91-4b52-9ddb-9bb5a57bfa37.PNG)

###### 2. Menginstall lxc debian 9 dengan nama debian_php5.6
- Install LXC debian 9

```markdown
sudo lxc-create -n debian_php5.6 -t download -- -- dist debian --release stretch --arch amd64 --force-chace --no-validate --server images.linuxcontainers.org
```

![2](https://user-images.githubusercontent.com/93079538/138592516-1eb2dfe4-f321-45a0-b781-41546967033b.PNG)

###### 3. Setup nginx pada debian_php5.6 untuk domain http://lxc_php5.dev ,buat halaman index.html yang menerangkan informasi nama lxc

- Start debian_php5.6
```

```markdown
sudo lcx-start debian_php5.6
sudo lxc-attach debian_php5.6
apt install nano net-tools curl
```

![3](https://user-images.githubusercontent.com/93079538/138592527-823a8bec-d892-4129-9f62-f4f981a20f8b.PNG)

- Set up static IP 
```

```markdown
nano /etc/network/interfaces
```

![3 3](https://user-images.githubusercontent.com/93079538/138592522-c6b4486d-5e64-48cb-9207-80614faa6052.PNG)

```markdown
reboot
ifconfig
```

![3 4](https://user-images.githubusercontent.com/93079538/138592523-46aa615e-58b4-4e5e-a378-432c348173db.PNG)

- Setting nginx 
```

```markdown
sudo apt install nginx nginx-extras
```

![3 5](https://user-images.githubusercontent.com/93079538/138592524-2687de79-a862-410d-bbb1-d7ae0569c8ca.PNG)

```markdown
cd /etc/nginx/sites-available
touch lxc_php5.6.dev
nano lxc_php5.6.dev
```

![3 6](https://user-images.githubusercontent.com/93079538/138592525-74fa9c52-7675-46fb-9b33-483786fa7562.PNG)

```markdown
cd ../sites-enable
ln -s /etc/nginx/sites-available/lxc_php5.6.dev .
nginx -t
nginx -s reload
nano /etc/hosts
```

![3 2](https://user-images.githubusercontent.com/93079538/138592520-f6ccb50e-e2d7-4dd8-8802-a33382da32e5.PNG)

```markdown
cd /var/www/html
mkdir lxc_php5.6
cp index.nginx-debian.html lxc_php5.6/index.html
cd lxc_php5.6
nano index.html
```

![3 1](https://user-images.githubusercontent.com/93079538/138592519-fd1e398c-734e-4f61-8bc2-0afb507adea9.PNG)

```markdown
curl -i http://lxc_php5.dev 
```

###### 4. Setup nginx pada ubuntu_landing untuk domain http://lxc_landing.dev ,buat halaman index.html yang menerangkan informasi nama
- Setting nginx ubuntu_landing

```markdown
cd /etc/nginx/sites-available
touch lxc_php5.6.dev
nano lxc_php5.6.dev
```

![4](https://user-images.githubusercontent.com/93079538/138592533-9b9c4526-e7b4-4d3f-8af2-ecf845a21064.PNG)

```markdown
cd ../sites-enable
ln -s /etc/nginx/sites-available/lxc_php5.6.dev .
nginx -t
nginx -s reload
nano /etc/hosts
```

![4 1](https://user-images.githubusercontent.com/93079538/138592529-17f48f09-864d-47fe-84d1-f57e6dfb233b.PNG)

```markdown
cd /var/www/html
nano index.html
```

![4 3](https://user-images.githubusercontent.com/93079538/138592531-46b1d0f5-b255-41d8-a453-6b34adb88bec.PNG)

```
curl -i http://lxc_php5.dev 
```

###### 5. LXC ubuntu_landing harus auto start ketika vm dinyalakan,hal ini digunakan untuk menjaga agar website company profile tidak mengalami *downtime*
- Auto start ubuntu_landing

```markdown
sudo su 
echo "lxc.start.auto = 1" >> /var/lib/lxc/ubuntu_landing/config
lxc-stop ubuntu_landing
lxc-ls -f
```

![5 1](https://user-images.githubusercontent.com/93079538/138592536-71252014-7332-46ed-abcf-802d582f0729.PNG)

###### 6. Setup nginx pada vm.local untuk mengatur *proxy_pass* dimana:

  - mengakses http://vm.local akan diarahkan ke http://lxc_landing.dev

  - mengakses http://vm.local/blog akan diarahkan ke http://Lxc_php7.dev

  - mengakese http://vm.local/app akan diarahkan  ke http://lxc_php5.dev

    

- Setting hosts vm

    ```markdown
    sudo nano /etc/hosts
    ```

![6](https://user-images.githubusercontent.com/93079538/138592542-64c94571-79c3-4000-ae45-94dd1e549f3d.PNG)
- Setting nginx vm

    ```markdown
    cd /etc/nginx/sites-available
    sudo nano vm.local
    ```
    

![6 1](https://user-images.githubusercontent.com/93079538/138592538-4afe01ad-341c-4150-8f19-5e46605aca9c.PNG)

```markdown
sudo ln -s /etc/nginx/sites-available/vm.local .
sudo nginx -t
sudo nginx -s reload
curl -i http://vm.local
```

![6 3](https://user-images.githubusercontent.com/93079538/138592541-742a8c6c-9691-44d4-a56a-f28add2e66f2.PNG)

###### 7. untuk kebutuhan presentasi mereka,broswer di laptop mereka harus dapat mengakses ketiga url tersebut

```markdown
- mengakses http://vm.local
```

![browser 1](https://user-images.githubusercontent.com/93079538/138592545-28c8ceb9-d170-45ef-90ee-cea5e0421c6b.PNG)

```markdown
- mengakses http://vm.local/blog
```

![blog](https://user-images.githubusercontent.com/93079538/138592544-9b7796f8-dfbf-43cf-8ca0-2dec39622a1d.PNG)

```markdown
- mengakses http://vm.local/app
```
![app](https://user-images.githubusercontent.com/93079538/138592543-303cfdc5-f897-4b62-9f08-b762097ee44e.PNG)

8. Menyiapkan analisa untuk diserahkan ke CTO

- mengapa untuk kebutuhan php5.6 tidak bisa menggunakan ubuntu 16.04, sehingga perlu diganti os ke debian 9?
 karena ubuntu 16.04 hanya tersedia untuk opsi yang berbayar dan hanya dapat diakses ubuntu estended securiti maintanance yang berarti ubuntu 16.04 akan dihapus karena adanya pembaruan fitur yang bernama Trusty EOL yang tidak support pada ubuntu 16.04

- kenapa harus menggunakan virtualisasi LXC pada skema website yang akan didevelop?
 karena virtualisasi lxc dapat menghemat ruang, menghemat biaya, meningkatkan waktu UPTIME, penyediaan server yang cepat, dan backup yang mudah

- apa yang dimaksud dengan proxy server? kenapa vm.local bisa kita anggap sebagai proxy server?
 Proxy server (peladen proxy) adalah sebuah komputer server atau program komputer yang dapat bertindak sebagai komputer lainnya untuk melakukan request terhadap content dari Internet atau intranet.
