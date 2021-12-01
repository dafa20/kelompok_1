# Praktikum Modul 2

## SIstem Administrasi Server

#### Novandy Prakoso (1202190057)

#### Dafa Septiandri Dwinanda P (1202190057)



1. ##### Rubah LXC landing dengan ubuntu focal (destroy n create, same ip, same name)

   - Mengganti lxc_landing lxc_php7 dari ubuntu 18 ke ubuntu 20 yaitu ubuntu focal

     ![2](C:\Users\Novandy\Downloads\SS SAS 2\2.png)

     ```
     sudo lxc-destroy ubuntu_landing
     
     sudo lxc-create -n ubuntu_landing -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
     ```

   - mengatur IP ubuntu_landing 10.0.3.103

     ```
     sudo lxc-start -n ubuntu_landing
     sudo lxc-attach  -n ubuntu_landing
     nano /etc/netplan/10-lxc.yaml
     ```

      ![4](C:\Users\Novandy\Downloads\SS SAS 2\4.png)

     ```
     netplan apply
     ```

   - install dan setting open-ssh

     ```
     apt install openssh-server -y
     ```

     ![7](C:\Users\Novandy\Downloads\SS SAS 2\7.png)

     

     ```
     nano /etc/ssh/sshd_config
     ```

   ![8](C:\Users\Novandy\Downloads\SS SAS 2\8.png)

   ```
   service sshd restart
   ```

   

   - cek ssh apakah sudah berjalan

     ```
     ssh root@10.0.3.103
     ```

     ![10](C:\Users\Novandy\Downloads\SS SAS 2\10.png)

     

2. ##### Rubah LXC php7 dengan ubuntu focal (destroy n create, same ip, same name)

   - Mengganti lxc_php7 dengan ubuntu focal

     ```
     sudo lxc-destroy ubuntu_landing
     
     sudo lxc-create -n ubuntu_php7.4 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
     ```

     ![12](C:\Users\Novandy\Downloads\SS SAS 2\12.png)

   - lakukan seperti lxc_landing

     

3. ##### vm.local/

   - membuat direktori laravel lalu setting hosts

     ```
     cd ~/ansibel
     mkdir laravel
     cd laravel/
     ```

     ```
     nano hosts
     ```

     ![2021-11-30_3](C:\Users\Novandy\Downloads\no 3\2021-11-30_3.png)

   - membuat file nginxphp.yml lalu setting

     ```
     nano nginxphp.yml
     ```

     ![2021-11-30_3_1](C:\Users\Novandy\Downloads\no 3\2021-11-30_3_1.png)

     - melakukan instalasi nginxphp.yml

       ```
       ansible-playbook -i hosts nginxphp.yml -k
       ```

       ![instalasi nginxphp](C:\Users\Novandy\Downloads\SS SAS 2\instalasi nginxphp.png)

   - membuat file installcomposer.yml

     ```
     nano installcomposer.yml
     ```

     ![23](C:\Users\Novandy\Downloads\SS SAS 2\23.png)

     - melakukan instalasi

       ```
       ansible-playbook -i hosts installcomposer.yml -k
       ```

       ![instalasi composer](C:\Users\Novandy\Downloads\SS SAS 2\instalasi composer.png)

   - membuat file config.yml dan setting

     ```
     nano config.yml
     ```

     ![2021-11-30_7](C:\Users\Novandy\Downloads\no 3\2021-11-30_7.png)

     - melakukan instalasi

       ```
       ansible-playbook -i hosts config.yml -k
       ```

       ![instalasi configyml](C:\Users\Novandy\Downloads\SS SAS 2\instalasi configyml.png)

   - mengatur lxc_landing.dev

     ```
     nano lxc_landing.dev
     ```

     ![2021-11-30_6_1](C:\Users\Novandy\Downloads\no 3\2021-11-30_6_1.png)

     

     - buka vm.local/ pada browser dan laravel sukses dijalankan

       ![laravel](C:\Users\Novandy\Downloads\SS SAS 2\laravel.png)

4. ##### vm.local/blog

   - membuat direktori wordpress lalu setting hosts

     ```
     cd ~/ansibel
     mkdir wordpress
     cd wordpress/
     ```

   - membuat file installwordpress.yml

     ```
     nano installwordpress.yml
     ```

     ![2021-12-01_2](C:\Users\Novandy\Downloads\no 4\2021-12-01_2.png)

     - melakukan instalasi

       ```
       ansible-playbook -i hosts installwordpress.yml -k
       ```

       ![instalasi wordpress](C:\Users\Novandy\Downloads\SS SAS 2\instalasi wordpress.png)

   - membuat file wp.conf

     ```
     nano wp,conf
     ```

     ![2021-12-01_2_1](C:\Users\Novandy\Downloads\no 4\2021-12-01_2_1.png)

     

   - membuat file wordpress.conf

     ![2021-12-01_3](C:\Users\Novandy\Downloads\no 4\2021-12-01_3.png)

   - cek browser dengan membuka vm.local/blog

     ![akhir](C:\Users\Novandy\Downloads\SS SAS 2\akhir.png)

     ![akhir1](C:\Users\Novandy\Downloads\SS SAS 2\akhir1.png)

     ![akhir2](C:\Users\Novandy\Downloads\SS SAS 2\akhir2.png)

   - wordpress sudah dapat dijalankan