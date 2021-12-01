# Praktikum Modul 2

## SIstem Administrasi Server

#### Novandy Prakoso (1202190057)
#### Dafa Septiandri Dwinanda P (1202190057)



1. ##### Rubah LXC landing dengan ubuntu focal (destroy n create, same ip, same name)

   - Mengganti lxc_landing lxc_php7 dari ubuntu 18 ke ubuntu 20 yaitu ubuntu focal

      ![2](https://user-images.githubusercontent.com/93079538/144323046-c867cbbe-e76b-47ac-920f-3266d15ce19c.png)
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

      ![4](https://user-images.githubusercontent.com/93079538/144323084-0b0f1d36-a65e-4c27-a916-4d848425c2bc.png)
     ```
     netplan apply
     ```

   - install dan setting open-ssh

     ```
     apt install openssh-server -y
     ```

      ![7](https://user-images.githubusercontent.com/93079538/144323164-4ee2d205-9a37-4da1-9b2b-df046145f953.png)
     

     ```
     nano /etc/ssh/sshd_config
     ```

      ![8](https://user-images.githubusercontent.com/93079538/144323182-1ed3e7f9-b392-4dee-890f-d25786e4067b.png)
     ```
     service sshd restart
     ```

   

   - cek ssh apakah sudah berjalan

     ```
     ssh root@10.0.3.103
     ```

      ![10](https://user-images.githubusercontent.com/93079538/144323191-80ad2900-2a72-4761-b12e-2300d26c6fe5.png)
     

2. ##### Rubah LXC php7 dengan ubuntu focal (destroy n create, same ip, same name)

   - Mengganti lxc_php7 dengan ubuntu focal

     ```
     sudo lxc-destroy ubuntu_landing
     
     sudo lxc-create -n ubuntu_php7.4 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
     ```

      ![12](https://user-images.githubusercontent.com/93079538/144323250-030c9dbf-97be-447f-8a3b-a5fa29eb7556.png)
      
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

     ![2021-11-30_3](https://user-images.githubusercontent.com/93079538/144323537-ced18727-129c-4900-ab11-b795d09f30bc.png)
     
   - membuat file nginxphp.yml lalu setting

     ```
     nano nginxphp.yml
     ```

       ![2021-11-30_3_1](https://user-images.githubusercontent.com/93079538/144323547-fe73e37d-a299-45e7-8eaa-3d724f9e2b13.png)
       
     - melakukan instalasi nginxphp.yml

      ```
      ansible-playbook -i hosts nginxphp.yml -k
      ```
      
      ![instalasi nginxphp](https://user-images.githubusercontent.com/93079538/144323307-7392a618-0001-4f27-87bf-2e05dc373594.png)
      
   - membuat file installcomposer.yml

     ```
     nano installcomposer.yml
     ```
     
      ![23](https://user-images.githubusercontent.com/93079538/144323354-fee7cef9-f7a8-45b9-9a57-6de95512a6c7.png)
     
     - melakukan instalasi

      ```
      ansible-playbook -i hosts installcomposer.yml -k
      ```

      ![instalasi composer](https://user-images.githubusercontent.com/93079538/144323400-287b8cdd-09f1-4c4a-bbec-799643dcda98.png)
      
   - membuat file config.yml dan setting

     ```
     nano config.yml
     ```

      ![2021-11-30_7](https://user-images.githubusercontent.com/93079538/144323910-6229d261-3e82-4223-b004-360407b35c18.png)
      
     - melakukan instalasi

      ```
      ansible-playbook -i hosts config.yml -k
      ```

      ![instalasi configyml](https://user-images.githubusercontent.com/93079538/144323435-9fdec0ca-acdf-481f-a09e-82fd52b8e28c.png)
      
   - mengatur lxc_landing.dev

     ```
     nano lxc_landing.dev
     ```

      ![2021-11-30_6_1](https://user-images.githubusercontent.com/93079538/144323978-2979077b-b801-43f9-8c4f-a0fce7863e36.png)
     
     - buka vm.local/ pada browser dan laravel sukses dijalankan

      ![laravel](https://user-images.githubusercontent.com/93079538/144323469-9dde9eb0-4c3e-4bbc-ae0e-b61b227c9b8b.png)

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

      ![2021-12-01_2](https://user-images.githubusercontent.com/93079538/144324062-42370730-58ef-40a0-8b5c-5aff7b614191.png)
      
     - melakukan instalasi

      ```
      ansible-playbook -i hosts installwordpress.yml -k
      ```

      ![instalasi wordpress](https://user-images.githubusercontent.com/93079538/144324100-b3b23d80-7b2c-4131-9b57-5c6c298c9f22.png)
      
   - membuat file wp.conf

     ```
     nano wp,conf
     ```

      ![2021-12-01_2_1](https://user-images.githubusercontent.com/93079538/144324338-8ca373d4-064e-4fb9-b5c9-6684ef9e0887.png)
     

   - membuat file wordpress.conf

      ![2021-12-01_3](https://user-images.githubusercontent.com/93079538/144324309-fa39eeda-8dd0-46d6-bab1-90abdeebf40d.png)
      
   - cek browser dengan membuka vm.local/blog

      ![akhir](https://user-images.githubusercontent.com/93079538/144324200-7db2c26f-fde0-4be0-b896-78b37e3ed736.png)
      
      ![akhir1](https://user-images.githubusercontent.com/93079538/144324213-cbc05d3d-7ba0-4823-b774-2c708e81ec7d.png)
      
      ![akhir2](https://user-images.githubusercontent.com/93079538/144324226-5a351c6a-b9f6-4f86-a14e-ab49062440af.png)
   - wordpress sudah dapat dijalankan
