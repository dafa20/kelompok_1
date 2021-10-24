# <u>Laporan Praktikum Modul 1</u>

## **Sistem Administrasi Server**

###### Nama Kelompok :

- <u>Novandy Prakoso (1202190057)</u>
- <u>Dafa Septiandri Dwinanda Prabowo (1202192033)</u>



###### 1. Rename ubuntu_php5.6 menjadi ubuntu_landing, serta rubah IP mengikuti skema baru

 - Mengecek LXC, lalu rename ubuntu_php5.6 menjadi ubuntu_landing 

```
sudo lxc -ls -f
sudo lxc-copy -R ubuntu_php5.6 -N ubuntu_landing
```

![1](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\1.PNG)

 - Start ubuntu_landing

![1.1](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\1.1.PNG)

 - Set up static IP pada ubuntu_landing

```
sudo nano /etc/network/interfaces
```

![1.2](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\1.2.PNG)

```
reboot
ifconfig
```

![1.3](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\1.3.PNG)

###### 2. Menginstall lxc debian 9 dengan nama debian_php5.6

 - Install LXC debian 9

```
sudo lxc-create -n debian_php5.6 -t download -- -- dist debian --release stretch --arch amd64 --force-chace --no-validate --server images.linuxcontainers.org
```

![2](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\2.PNG)

###### 3. Setup nginx pada debian_php5.6 untuk domain http://lxc_php5.dev ,buat halaman index.html yang menerangkan informasi nama lxc

	- Start debian_php5.6

```
sudo lcx-start debian_php5.6
sudo lxc-attach debian_php5.6
apt install nano net-tools curl
```

![3](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\3.PNG)

	- Set up static IP 

```
nano /etc/network/interfaces
```

![3.3](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\3.3.PNG)

```
reboot
ifconfig
```

![3.4](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\3.4.PNG)

	- Setting nginx 

```
sudo apt install nginx nginx-extras
```

![3.5](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\3.5.PNG)

```
cd /etc/nginx/sites-available
touch lxc_php5.6.dev
nano lxc_php5.6.dev
```

![3.6](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\3.6.PNG)

```
cd ../sites-enable
ln -s /etc/nginx/sites-available/lxc_php5.6.dev .
nginx -t
nginx -s reload
nano /etc/hosts
```

![3.2](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\3.2.PNG)

```
cd /var/www/html
mkdir lxc_php5.6
cp index.nginx-debian.html lxc_php5.6/index.html
cd lxc_php5.6
nano index.html
```

![3.1](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\3.1.PNG)

```
curl -i http://lxc_php5.dev 
```

###### 4. Setup nginx pada ubuntu_landing untuk domain http://lxc_landing.dev ,buat halaman index.html yang menerangkan informasi nama

 - Setting nginx ubuntu_landing

```
cd /etc/nginx/sites-available
touch lxc_php5.6.dev
nano lxc_php5.6.dev
```

![4](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\4.PNG)

```
cd ../sites-enable
ln -s /etc/nginx/sites-available/lxc_php5.6.dev .
nginx -t
nginx -s reload
nano /etc/hosts
```

![4.1](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\4.1.PNG)

```
cd /var/www/html
nano index.html
```

![4.3](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\4.3.PNG)

```
curl -i http://lxc_php5.dev 
```

###### 5. LXC ubuntu_landing harus auto start ketika vm dinyalakan,hal ini digunakan untuk menjaga agar website company profile tidak mengalami *downtime*

 - Auto start ubuntu_landing

```
sudo su 
echo "lxc.start.auto = 1" >> /var/lib/lxc/ubuntu_landing/config
lxc-stop ubuntu_landing
lxc-ls -f
```

![5.1](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\5.1.PNG)

###### 6. Setup nginx pada vm.local untuk mengatur *proxy_pass* dimana:

  - mengakses http://vm.local akan diarahkan ke http://lxc_landing.dev

  - mengakses http://vm.local/blog akan diarahkan ke http://Lxc_php7.dev

  - mengakese http://vm.local/app akan diarahkan  ke http://lxc_php5.dev

    

    - Setting hosts vm

    ```
    sudo nano /etc/hosts
    ```

    ![6](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\6.PNG)

    - Setting nginx vm

    ```
    cd /etc/nginx/sites-available
    sudo nano vm.local
    ```
    
![6.1](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\6.1.PNG)
    
```
    sudo ln -s /etc/nginx/sites-available/vm.local .
    sudo nginx -t
    sudo nginx -s reload
    curl -i http://vm.local
    ```
    
![6.3](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\6.3.PNG)

###### 7.untuk kebutuhan presentasi mereka,broswer di laptop mereka harus dapat mengakses ketiga url tersebut

	- mengakses http://vm.local

![browser 1](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\browser 1.PNG)

	- mengakses http://vm.local/blog

![blog](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\blog.PNG)

	- mengakses http://vm.local/app

![app](C:\Users\owner\Downloads\SAS-20211021T124156Z-001\SAS\app.PNG)

