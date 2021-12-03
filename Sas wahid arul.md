Sas wahid arul

 

1 Ubah LXC landing dengan ubuntu focal ( destroy n create, same ip, same name) destroy

rm /var/lib/lxc/ubuntu_php7.4/lxc_snapshots

lxc-destroy ubuntu_landing

![1](https://user-images.githubusercontent.com/95128942/144636754-fd9c8e5a-0914-4528-8dbb-eff75a604e35.jpg)
 

Create

sudo lxc-create -n ubuntu_landing -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org

root@sas02:~# lxc-start ubuntu_landing

root@sas02:~# lxc-attach ubuntu_landing

![2](https://user-images.githubusercontent.com/95128942/144636766-f69efae6-69fe-4eb1-b4cd-2b7b96b03299.jpg)
 

root@ubuntulanding:~# apt install nano net-tools curl

![3](https://user-images.githubusercontent.com/95128942/144636775-0b54d2a9-0096-4b21-ba90-6dbe2f774874.jpg)
Atur ip

root@ubuntulanding:~# nano /etc/netplan/10-lxc.yaml

![4](https://user-images.githubusercontent.com/95128942/144636784-24faa00e-3114-456b-8250-7fb30a666656.jpg)
 

Ip ganti

root@ubuntulanding:~# netplan apply

root@ubuntulanding:~# ip r

![5](https://user-images.githubusercontent.com/95128942/144636900-bc4f332b-80ef-46e5-8a88-507857cde1a5.jpg)
 

Install ssh

\# apt install openssh-server -y

![6](https://user-images.githubusercontent.com/95128942/144636926-a2d81059-967c-4735-be88-c34b6ed96d97.jpg)
nano sshd_config

![7](https://user-images.githubusercontent.com/95128942/144636940-04765941-ef90-4380-b786-db8bc7f0c44d.jpg)
root@ubuntulanding:/etc/ssh# passwd

New password:

Retype new password:

passwd: password updated successfully

root@ubuntulanding:/etc/ssh# exit

![8](https://user-images.githubusercontent.com/95128942/144636950-9130b7e1-3440-47e8-bdc3-020dc9038798.jpg)

ssh root@10.0.3.103

![9](https://user-images.githubusercontent.com/95128942/144636959-c6dc3727-4f71-40b6-9391-208aba53513e.jpg)
\2.  rm /var/lib/lxc/ubuntu_php7.4/lxc_snapshots

lxc-destroy ubuntu_landing

![10](https://user-images.githubusercontent.com/95128942/144636982-4f90e968-3968-4316-bf6b-68e1eb271b42.jpg)
 

Create

sudo lxc-create -n ubuntu_landing -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org

root@sas02:~# lxc-start ubuntu_landing

root@sas02:~# lxc-attach ubuntu_landing

![11](https://user-images.githubusercontent.com/95128942/144637005-d9a34eec-c4cd-43c2-b94e-20f8eb7c80d5.jpg)
 

root@ubuntulanding:~# apt install nano net-tools curl

![12](https://user-images.githubusercontent.com/95128942/144637062-af66102f-34b0-4df9-989c-c28d74747340.jpg)
Atur ip

root@ubuntulanding:~# nano /etc/netplan/10-lxc.yaml

![13](https://user-images.githubusercontent.com/95128942/144637114-4f0360e3-7b3f-40d0-bb3e-3449e27e6be8.jpg)
 

Ip ganti

root@ubuntulanding:~# netplan apply

root@ubuntulanding:~# ip r

![14](https://user-images.githubusercontent.com/95128942/144637137-1bb68ee6-b32f-4482-81a1-87ef23c95ba9.jpg)
 

Install ssh

\# apt install openssh-server -y

![15](https://user-images.githubusercontent.com/95128942/144637149-694fc40e-ce63-4de2-98f6-72357b2e6bde.jpg)
nano sshd_config

![16](https://user-images.githubusercontent.com/95128942/144637169-a2f5d3a6-cae6-4102-a60e-9095876d7e46.jpg)
root@ubuntulanding:/etc/ssh# passwd

New password:

Retype new password:

passwd: password updated successfully

root@ubuntulanding:/etc/ssh# exit

![17](https://user-images.githubusercontent.com/95128942/144637190-9a749f09-0571-4d0e-ab52-1f235c551783.jpg)
ssh root@10.0.3.103

![18](https://user-images.githubusercontent.com/95128942/144638761-3b302cbb-3aa9-4f67-99af-9fda1ee4f7ab.jpg)
\3. install Laravel

cd -/ansible/

mksdir Laravel/

cd Laravel/

![19](https://user-images.githubusercontent.com/95128942/144637233-0cc47149-9b27-46b4-8906-767579b62adb.jpg)
78c66f97.jpg)
Membuat hosts

Hosts

ubuntu_landing ansible_host=lxc_landing.dev ansible_ssh_user=root ansible_become_pass=1234

 

![20](https://user-images.githubusercontent.com/95128942/144639612-d993b5cc-c59f-4069-bed1-03391b71e2ef.jpg)
 

buat direktori yang akan dijalankan pada folder php dam install di nginxphp.yml

\---

\- hosts: all

 become : yes

 tasks:

  \- name: install nginx nginx extras

   apt:

​    pkg:

​     \- nginx

​     \- nginx-extras

​    state: latest

  \- name: start nginx

   service:

​    name: nginx

​    state: started

  \- name: menginstall tools

   apt:

​    pkg:

​     \- curl

​     \- software-properties-common

​     \- unzip

​    state: latest

​     \- name: "Repo PHP 7.4"

​    apt_repository:

​     repo="ppa:ondrej/php"

  \- name: "Updating the repo"

   apt: update_cache=yes

  \- name: Installation PHP 7.4

   apt: name=php7.4 state=present

  \- name: install php untuk laravel

   apt:

​    pkg:

​     \- php7.4-fpm

​       \- php7.4-mysql

​       \- php7.4-mbstring

​       \- php7.4-xml

​       \- php7.4-bcmath

​       \- php7.4-json

​       \- php7.4-zip

​       \- php7.4-common

​          state: present

![21](https://user-images.githubusercontent.com/95128942/144637282-ed402335-2947-4297-9150-d90a2d859704.jpg)
 

 

Installasi

 

ansible-playbook -y hosts nginxphp.yml -k

 

![22](https://user-images.githubusercontent.com/95128942/144637337-311b4600-4d16-4660-a3c4-21a7395d6fba.jpg)
 

Installcomposer

Installcomposer.yml
![23](https://user-images.githubusercontent.com/95128942/144637370-9683c663-a4a6-4281-b9f2-8b00ec917f12.jpg) 

![24](https://user-images.githubusercontent.com/95128942/144637395-e302c167-4513-4d3e-b988-a4973f69e656.jpg)
 

lxc_landing.dev

![25](https://user-images.githubusercontent.com/95128942/144637443-d0c0b66e-f269-43e4-85c8-1621687c139c.jpg)

![26](https://user-images.githubusercontent.com/95128942/144637463-265a76b7-d769-4d06-9564-2e945fe10e54.jpg)

![27](https://user-images.githubusercontent.com/95128942/144637474-f477bc40-09c4-4766-a73e-7c860f0632e9.jpg)

![28](https://user-images.githubusercontent.com/95128942/144637494-cf9e0018-43be-4025-b7fe-ba5f28d3d113.jpg)

 

 

 

\4. wordpress

root@sas02:~/ansible# mkdir wordpress

root@sas02:~/ansible# cd wordpress/

root@sas02:~/ansible/wordpress#

 
![29](https://user-images.githubusercontent.com/95128942/144637510-b8df036c-cd32-4d11-9335-07220f0809ed.jpg)

![30](https://user-images.githubusercontent.com/95128942/144637519-063f1fdf-3278-4034-9509-8ea76b298b8d.jpg)


 

Buat direktori

![31](https://user-images.githubusercontent.com/95128942/144637540-68bcb060-5d65-454f-84d7-283b6baf03d6.jpg)
 

Direktori wp

![32](https://user-images.githubusercontent.com/95128942/144637615-88b5ea1d-6983-43b1-bbcd-7d1cf352d76c.jpg)
 

Direktori wordpress.conf

![33](https://user-images.githubusercontent.com/95128942/144637629-7836b62e-938a-4696-ba6b-57eda162ad90.jpg)
 

Install

Ansible-playbook -I hosts installwordpress.yml -k

![34](https://user-images.githubusercontent.com/95128942/144637651-37d61b96-44df-4a16-88db-368149ea759f.jpg)
 

![35](https://user-images.githubusercontent.com/95128942/144637680-77be710e-1d2a-4996-a329-77f4af8ba5d8.jpg)
 

![36](https://user-images.githubusercontent.com/95128942/144637687-8f7ee002-2688-4edc-b7f6-64c02dd2857d.jpg)
 

 

Soal tambahan

Mengubah di bagian fastcgi_pass menjadi 127.0.0.1:9001;

![37](https://user-images.githubusercontent.com/95128942/144637732-56119dc6-e353-440d-8fda-22d96f214ac2.jpg)

![38](https://user-images.githubusercontent.com/95128942/144637750-fefa12f0-3fc5-4b2e-82fa-c10169012d1d.jpg)

![39](https://user-images.githubusercontent.com/95128942/144637772-661497ed-8800-4d94-ad4f-a09edf06872e.jpg)

![40](https://user-images.githubusercontent.com/95128942/144637792-c61592ff-8742-4f3c-b4e4-3d9346ef152f.jpg)

 

Wordpress

Sama seperti laravel

![41](https://user-images.githubusercontent.com/95128942/144637803-421cf473-608a-4485-88e4-24198706a2a3.jpg)

![42](https://user-images.githubusercontent.com/95128942/144637819-8d9d909f-9060-4f88-958a-982ab6aed17c.jpg)

![43](https://user-images.githubusercontent.com/95128942/144637837-a2b28af0-7cae-4989-b838-f4359d78060e.jpg)
