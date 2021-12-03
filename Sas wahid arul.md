Sas wahid arul

 

1 Ubah LXC landing dengan ubuntu focal ( destroy n create, same ip, same name) destroy

rm /var/lib/lxc/ubuntu_php7.4/lxc_snapshots

lxc-destroy ubuntu_landing

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg)

 

Create

sudo lxc-create -n ubuntu_landing -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org

root@sas02:~# lxc-start ubuntu_landing

root@sas02:~# lxc-attach ubuntu_landing

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image004.jpg)

 

root@ubuntulanding:~# apt install nano net-tools curl

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image006.jpg)

Atur ip

root@ubuntulanding:~# nano /etc/netplan/10-lxc.yaml

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image008.jpg)

 

Ip ganti

root@ubuntulanding:~# netplan apply

root@ubuntulanding:~# ip r

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image010.jpg)

 

Install ssh

\# apt install openssh-server -y

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image012.jpg)

nano sshd_config

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image014.jpg)

root@ubuntulanding:/etc/ssh# passwd

New password:

Retype new password:

passwd: password updated successfully

root@ubuntulanding:/etc/ssh# exit

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image016.jpg)

ssh root@10.0.3.103

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image018.jpg)

\2.  rm /var/lib/lxc/ubuntu_php7.4/lxc_snapshots

lxc-destroy ubuntu_landing

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image019.jpg)

 

Create

sudo lxc-create -n ubuntu_landing -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org

root@sas02:~# lxc-start ubuntu_landing

root@sas02:~# lxc-attach ubuntu_landing

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image020.jpg)

 

root@ubuntulanding:~# apt install nano net-tools curl

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image021.jpg)

Atur ip

root@ubuntulanding:~# nano /etc/netplan/10-lxc.yaml

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image022.jpg)

 

Ip ganti

root@ubuntulanding:~# netplan apply

root@ubuntulanding:~# ip r

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image023.jpg)

 

Install ssh

\# apt install openssh-server -y

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image024.jpg)

nano sshd_config

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image025.jpg)

root@ubuntulanding:/etc/ssh# passwd

New password:

Retype new password:

passwd: password updated successfully

root@ubuntulanding:/etc/ssh# exit

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image026.jpg)

ssh root@10.0.3.103

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image027.jpg)

\3. install Laravel

cd -/ansible/

mksdir Laravel/

cd Laravel/

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image029.png)

Membuat hosts

Hosts

ubuntu_landing ansible_host=lxc_landing.dev ansible_ssh_user=root ansible_become_pass=1234

 

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image031.png)

 

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

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image033.png)

 

 

Installasi

 

ansible-playbook -y hosts nginxphp.yml -k

 

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image035.png)

 

Installcomposer

Installcomposer.yml

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image037.png)
 

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image039.png)

 

lxc_landing.dev

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image041.png)

 

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image043.png)

 

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image045.png)

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image047.png)

 

 

 

\4. wordpress

root@sas02:~/ansible# mkdir wordpress

root@sas02:~/ansible# cd wordpress/

root@sas02:~/ansible/wordpress#

 

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image049.png)

 

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image051.png)

 

Buat direktori

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image053.png)

 

Direktori wp

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image055.png)

 

Direktori wordpress.conf

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image057.png)

 

Install

Ansible-playbook -I hosts installwordpress.yml -k

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image059.png)

 

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image061.png)

 

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image063.png)

 

 

Soal tambahan

Mengubah di bagian fastcgi_pass menjadi 127.0.0.1:9001;

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image065.png)

 

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image067.png)

 

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image069.png)

 

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image071.png)

 

Wordpress

Sama seperti laravel

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image073.png)

 

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image075.png)

 

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image077.png)

 

![img](file:///C:/Users/WAHID/AppData/Local/Temp/msohtmlclip1/01/clip_image079.png)