# Jarkom-Modul-5-E29-2023
## Anggota
Kelompok E29
| Nama | NRP |
| --- | --- |
| Sony Hermawan | 5025211226 |
| Sekar Ambar Arum | 5025211041 |

# Laporan Resmi
* [(A)](#(A))
  * [Topologi GNS3](#Topologi-GNS3)
* [(B)](#(B))
  * [Topologi VLSM](#Topologi-VLSM)
  * [VLSM Tree](#VLSM-Tree)
* [(C)](#(C))
  * [Rute](#Rute)
  * [Pembagian IP](#Pembagian-IP)
  * [Subnetting](#Subnetting)
  * [Routing](#Routing)
* [(D)](#(D))
  * [DHCP Relay](#DHCP-Relay)
  * [Testing-CPT](#Testing-CPT)

### (A) Tugas pertama, buatlah peta wilayah sesuai berikut ini:
#### Topologi GNS3
![image](https://github.com/AdonisZK/Jarkom-Modul-5-E29-2023/assets/48209612/b1f20194-f178-4bc9-9b12-ae74d7edcf21)
### (B) Untuk menghitung rute-rute yang diperlukan, gunakan perhitungan dengan metode VLSM. Buat juga pohonnya, dan lingkari subnet yang dilewati.
#### Topologi VLSM
![image](https://github.com/AdonisZK/Jarkom-Modul-5-E29-2023/assets/48209612/40e01283-4248-4ec9-b5c0-f96177d8bd61)
#### VLSM Tree
![image](https://github.com/AdonisZK/Jarkom-Modul-5-E29-2023/assets/48209612/da32c2f4-f53d-46d4-bae5-ff369e3a2ba5)
### (C) Kemudian buatlah rute sesuai dengan pembagian IP yang kalian lakukan. 
#### Rute
| Nama Subnet                          | Rute                                           | Jumlah IP | Netmask |
|--------------------------------------|------------------------------------------------|-----------|---------|
| A1                                   | Heiter-TurkRegion                              | 1023      | /21     |
| A2                                   | Heiter-Switch3-Sein-Switch3-GrobeForest       | 514       | /22     |
| A3                                   | Himmel-LaubHills                               | 256       | /23     |
| A4                                   | Himmel-Switch1-SchwerMountain-Switch1-Fern    | 66        | /25     |
| A5                                   | Fern-Switch2-Revolte                           | 2         | /30     |
| A6                                   | Fern-Richter                                   | 2         | /30     |
| A7                                   | Frieren-Stark                                  | 2         | /30     |
| A8                                   | Himmel-Frieren                                 | 2         | /30     |
| A9                                   | Aura-Frieren                                   | 2         | /30     |
| A10                                  | Aura-Heiter                                   | 2         | /30     |
| **Total**                            |                                                | **1871**  | **/21** |
#### Pembagian IP
| Subnet | Network ID   | Netmask           | Broadcast      |
|--------|--------------|-------------------|----------------|
| A1     | 10.51.0.0    | 255.255.248.0     | 10.51.7.255    |
| A2     | 10.51.8.0    | 255.255.252.0     | 10.51.11.255   |
| A3     | 10.51.12.0   | 255.255.254.0     | 10.51.13.255   |
| A4     | 10.51.14.0   | 255.255.255.128   | 10.51.14.127   |
| A5     | 10.51.14.128 | 255.255.255.252   | 10.51.14.131   |
| A6     | 10.51.14.132 | 255.255.255.252   | 10.51.14.135   |
| A7     | 10.51.14.136 | 255.255.255.252   | 10.51.14.139   |
| A8     | 10.51.14.140 | 255.255.255.252   | 10.51.14.143   |
| A9     | 10.51.14.144 | 255.255.255.252   | 10.51.14.147   |
| A10    | 10.51.14.148 | 255.255.255.252   | 10.51.14.151   |

#### Subnetting
##### Aura
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp

#A10
auto eth1
iface eth1 inet static
address 10.51.14.149
netmask 255.255.255.252

#A9
auto eth2
iface eth2 inet static
address 10.51.14.145
netmask 255.255.255.252
```
##### Heiter
```
auto lo
iface lo inet loopback

#A10
auto eth0
iface eth0 inet static
address 10.51.14.150
netmask 255.255.255.252
gateway 10.51.14.149

#A1
auto eth1
iface eth1 inet static
address 10.51.0.1
netmask 255.255.248.0

#A2
auto eth2
iface eth2 inet static
address 10.51.8.1
netmask 255.255.252.0
```
##### Frieren
```
auto lo
iface lo inet loopback

#A9
auto eth0
iface eth0 inet static
address 10.51.14.146
netmask 255.255.255.252
gateway 10.51.14.145

#A7
auto eth1
iface eth1 inet static
address 10.51.14.137
netmask 255.255.255.252

#A8
auto eth2
iface eth2 inet static
address 10.51.14.141
netmask 255.255.255.252
```
##### Himmel
```
auto lo
iface lo inet loopback

#A8
auto eth0
iface eth0 inet static
address 10.51.14.142
netmask 255.255.255.252
gateway 10.51.14.141

#A3
auto eth1
iface eth1 inet static
address 10.51.12.1
netmask 255.255.254.0

#A4
auto eth2
iface eth2 inet static
address 10.51.14.1
netmask 255.255.255.128
```
##### Fern
```
auto lo
iface lo inet loopback

#A4
auto eth0
iface eth0 inet static
address 10.51.14.2
netmask 255.255.255.128
gateway 10.51.14.1

#A6
auto eth1
iface eth1 inet static
address 10.51.14.133
netmask 255.255.255.252

#A5
auto eth2
iface eth2 inet static
address 10.51.14.129
netmask 255.255.255.252
```
##### Sein
```
#A2
auto eth0
iface eth0 inet static
address 10.51.8.2
netmask 255.255.252.0
gateway 10.51.8.1
```
##### Stark
```
#A7
auto eth0
iface eth0 inet static
address 10.51.14.138
netmask 255.255.255.252
gateway 10.51.14.137
```
##### Richter
```
#A6
auto eth0
iface eth0 inet static
address 10.51.14.134
netmask 255.255.255.252
gateway 10.51.14.133
```
##### Revolte
```
#A5
auto eth0
iface eth0 inet static
address 10.51.14.130
netmask 255.255.255.252
gateway 10.51.14.129
```
##### GrobeForest, TurkRegion, LaubHills, SchwerMountain - Client
```
auto eth0
iface eth0 inet dhcp
```

#### Routing
##### Aura
```
# Frieren
## A8
route add -net 10.51.14.140 netmask 255.255.255.252 gw 10.51.14.146
## A3
route add -net 10.51.12.0 netmask 255.255.254.0 gw 10.51.14.146
## A4
route add -net 10.51.14.0 netmask 255.255.255.128 gw 10.51.14.146
## A5
route add -net 10.51.14.128 netmask 255.255.255.252 gw 10.51.14.146
## A6
route add -net 10.51.14.132 netmask 255.255.255.252 gw 10.51.14.146
## A7
route add -net 10.51.14.136 netmask 255.255.255.252 gw 10.51.14.146
# Heiter
## A1
route add -net 10.51.0.0 netmask 255.255.248.0 gw 10.51.14.150
## A2
route add -net 10.51.8.0 netmask 255.255.252.0 gw 10.51.14.150
```
##### Heiter
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.51.14.149
```
##### Frieren
```
# Himmel
## A3
route add -net 10.51.12.0 netmask 255.255.254.0 gw 10.51.14.142
## A4
route add -net 10.51.14.0 netmask 255.255.255.128 gw 10.51.14.142
## A5
route add -net 10.51.14.128 netmask 255.255.255.252 gw 10.51.14.142
## A6
route add -net 10.51.14.132 netmask 255.255.255.252 gw 10.51.14.142
```
##### Himmel
```
#Fern
## A5
route add -net 10.51.14.128 netmask 255.255.255.252 gw 10.51.14.2
## A6
route add -net 10.51.14.132 netmask 255.255.255.252 gw 10.51.14.2
```
##### Fern
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.51.14.142
```
### (D) Tugas berikutnya adalah memberikan ip pada subnet SchwerMountain, LaubHills, TurkRegion, dan GrobeForest menggunakan bantuan DHCP.
#### Script
##### Revolte - DHCP Server
```
apt-get update
apt-get install isc-dhcp-server -y
dhcpd --version

echo 'INTERFACES="eth0 eth1 eth2 "' >/etc/default/isc-dhcp-server

echo '
subnet 10.51.14.128 netmask 255.255.255.252 {

}

# TurkRegion
subnet 10.51.0.0 netmask 255.255.248.0 {
    range 10.51.0.2 10.51.0.255;
    option routers 10.51.0.1;
    option broadcast-address 10.51.7.255;
    option domain-name-servers 10.51.14.134;
    default-lease-time 600;
    max-lease-time 7200;
}

# GrobeForest
subnet 10.51.8.0 netmask 255.255.252.0 {
    range 10.51.8.3 10.51.8.255;
    option routers 10.51.8.1;
    option broadcast-address 10.51.11.255; 
    option domain-name-servers 10.51.14.134;
    default-lease-time 600;
    max-lease-time 7200;
}

# LaubHills
subnet 10.51.12.0 netmask 255.255.254.0 {
    range 10.51.12.2 10.51.12.255;
    option routers 10.51.12.1;
    option broadcast-address 10.51.13.255;
    option domain-name-servers 10.51.14.134;
    default-lease-time 600;
    max-lease-time 7200;
}

# SchwerMountain
subnet 10.51.14.0 netmask 255.255.255.128 {
    range 10.51.14.3 10.51.14.126;
    option routers 10.51.14.1;
    option broadcast-address 10.51.14.127;
    option domain-name-servers 10.51.14.134;
    default-lease-time 600;
    max-lease-time 7200;
}
' >/etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

##### Heiter, Himmel - DHCP Relay
```
apt-get update
apt-get install isc-dhcp-relay -y
service isc-dhcp-relay start

echo '
SERVERS="10.51.14.130"
INTERFACES="eth0 eth1 eth2"
OPTIONS=' >/etc/default/isc-dhcp-relay

echo '
net.ipv4.ip_forward=1' >/etc/sysctl.conf

service isc-dhcp-relay restart
```

### 1. Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.
#### Script
##### Aura
```
IPETH0="$(ip -br a | grep eth0 | awk '{print $NF}' | cut -d'/' -f1)"
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source "$IPETH0" -s 10.51.0.0/20
```
- `ip -br a`: Memberikan listing semua network interface dan konfigurasinya
- `grep eth0`: Filter output
- `awk '{print $NF}'`: Mengambil last column yaitu IP addr and subnet
- `cut -d'/' -f1`: Mengambil IP address dengan memisah string dengan /
- `iptables -t nat`: Menggunakan nat
- `- POSTROUTING`: Menambahkan rule POSTROUTING
- `-o eth0`: Outgoing network eth0
- `-j SNAT`: SNAT digunakan untuk memodikasi source address
- `--to-source "$IPETH0"`: Source SNAT eth0
#### Testing
Testing akan dilakukan oleh node lain dengan cara mengakses internet, disini kami akan mengambil contoh 1 router dan 1 client
##### Fern
![image](https://github.com/AdonisZK/Jarkom-Modul-5-E29-2023/assets/48209612/69ae323f-78fc-44c3-819d-365c199961d9)
##### TurkRegion
![image](https://github.com/AdonisZK/Jarkom-Modul-5-E29-2023/assets/48209612/b665d038-af07-4c72-84c3-35df64921e6f)

### 2. Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.
#### Script
Lakukan netcat terlebih dahulu
```
apt-get update
apt-get install netcat
```
##### Schwer
```
iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
iptables -A INPUT -p tcp -j DROP
iptables -A INPUT -p udp -j DROP
nc -l -p 8080
```
- `-A`: Append Rule
- `-p`: Menentukan protokol
- `--dport`: Menentukan port
- `-j ACCEPT`: Jika paket memenuhi kondisi maka paket tersebut diterima
- `-j DROP`: Jika paket memenuhi kondisi maka paket tersebut didrop
- `-l`: Mode listen.
##### Grobe
```
apt-get update
apt-get install netcat
nc <Ip Schwer> 8080 #Success
nc <Ip Schwer> 80   #Fail
```
port 80 akan fail karena port yang diaccept hanya 8080
#### Testing
![image](https://github.com/AdonisZK/Jarkom-Modul-5-E29-2023/assets/48209612/8ec2b1a2-5191-4138-95cd-857b8c12afbd)

### 3. Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.
#### Script
##### Revolte, Revolte - DHCP, DNS Server
```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```
##### Others
```
ping 10.51.14.130 #Revolte
ping 10.51.14.134 #Richter
```
Flag yang sudah dijelaskan di soal-soal atas tidak akan dibahas lagi
- `--connlimit-above 3`: Melimit koneksi hanya 3, akan menolak paket jika lebih dari 3
- `--connlimit-mask 0`: Mask 0 berarti melihat koneksi dari alamat IP sumberdan bukan port
#### Testing
![image](https://github.com/AdonisZK/Jarkom-Modul-5-E29-2023/assets/48209612/59ac272a-8837-45a3-a7cb-f0d709e49860)
Pada saat node ke4 melakukan ping, tidak akan mendapat balasan dari Revolte

### 4. Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.
#### Script
Script langsung untuk soal 4-6, 8
##### Sein, Stark - Web Server
```
# Soal 8
iptables -A INPUT -s 10.51.14.130 -m time --datestart 2024-02-14T00:00:00 --datestop 2024-06-26T23:59:59 -j DROP

# Soal 4
iptables -A INPUT -p tcp --dport 22 -s 10.51.8.0/22 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP

# Soal 6
iptables -A INPUT -m time --timestart 08:00 --timestop 12:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -m time --timestart 08:00 --timestop 11:00 --weekdays Fri -j ACCEPT
iptables -A INPUT -m time --timestart 13:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT

iptables -A INPUT -m time --timestart 12:00 --timestop 13:00 --weekdays Mon,Tue,Wed,Thu -j DROP
iptables -A INPUT -m time --timestart 11:00 --timestop 13:00 --weekdays Fri -j DROP

# Soal 5
iptables -A INPUT -m time --timestart 08:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -j DROP
```
Hanya allow `-s` dari subnet GrobeForest
##### Others
```
date -s "6 DEC 2023 09:00:00" #Dibutuhkan karena soal-soal berikutnya
nmap 10.51.14.138 -p 22
ssh 10.51.14.138
```
#### Testing
##### GrobeForest
![image](https://github.com/AdonisZK/Jarkom-Modul-5-E29-2023/assets/48209612/0e34e8f9-09c7-4029-81a1-c454e2179626)
- `22/tcp closed ssh` closed karena portnya tidak terbuka tetapi, mendapatkan response dari server
- `ssh port 22 connection refused` sama seperti diatas port tidak terbuka tetapi, mendapatkan response dari server
##### TurkRegion
![image](https://github.com/AdonisZK/Jarkom-Modul-5-E29-2023/assets/48209612/f4323816-768b-4021-946a-279c622437fb)
- `22/tcp filtered` ssh karena koneksi didrop
- `ssh` stuck karena tidak mendapat balasan dari server

### 5. Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.
#### Script
##### Stark, Sein - Web Server
```
iptables -A INPUT -m time --timestart 08:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -j DROP
```
- `-m time`: Menetapkan kondisi berdasarkan waktu
- `--timestart 08:00`: Menetapkan waktu awal 08:00
- `--timestop 16:00`: Menetapkan waktu akhir 16:00
- `--weekdays Mon,Tue,Wed,Thu,Fri`: Menetapkan hari dimana aturan ini berlaku, yaitu Senin hingga Jumat
##### GrobeForest
```
date -s "6 DEC 2023 09:00:00" # Success
ping 10.51.14.138 -c 5        #Stark
ping 10.51.8.2 -c 5           #Sein
date -s "6 DEC 2023 06:00:00" # Fail
ping 10.51.14.138 -c 5        #Stark
ping 10.51.8.2 -c 5           #Sein
```

#### Testing
![image](https://github.com/AdonisZK/Jarkom-Modul-5-E29-2023/assets/48209612/b8e8e15a-b3f6-4a57-a1ac-898c682c02c0)
- Percobaan pertama `success` karena pada waktu jam kerja
- Percobaan kedua `failed` karena diluar waktu jam kerja
### 6. Lalu, karena ternyata terdapat beberapa waktu di mana network administrator dari WebServer tidak bisa stand by, sehingga perlu ditambahkan rule bahwa akses pada hari Senin - Kamis pada jam 12.00 - 13.00 dilarang (istirahat maksi cuy) dan akses di hari Jumat pada jam 11.00 - 13.00 juga dilarang (maklum, Jumatan rek).
#### Script
##### Stark, Sein - Web Server
```
iptables -A INPUT -m time --timestart 08:00 --timestop 12:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -m time --timestart 08:00 --timestop 11:00 --weekdays Fri -j ACCEPT
iptables -A INPUT -m time --timestart 13:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT

iptables -A INPUT -m time --timestart 12:00 --timestop 13:00 --weekdays Mon,Tue,Wed,Thu -j DROP
iptables -A INPUT -m time --timestart 11:00 --timestop 13:00 --weekdays Fri -j DROP
```
##### GrobeForest
```
date -s "14 DEC 2023 11:20:00" # Success
ping 10.51.14.138 -c 5         #Stark
ping 10.51.8.2 -c 5            #Sein
date -s "15 DEC 2023 11:20:00" # Fail (Jumat)
ping 10.51.14.138 -c 5         #Stark
ping 10.51.8.2 -c 5            #Sein
date -s "14 DEC 2023 12:20:00" # Fail (Break)
ping 10.51.14.138 -c 5         #Stark
ping 10.51.8.2 -c 5            #Sein
```
#### Testing
##### GrobeForest
![image](https://github.com/AdonisZK/Jarkom-Modul-5-E29-2023/assets/48209612/a3f60be5-5928-4882-a356-ee7997b277ed)
- Test pertama `success` karena pada jam kerja
- Test kedua `failed` karena jumatan
- Test ketiga `failed` karena break
### 7. Karena terdapat 2 WebServer, kalian diminta agar setiap client yang mengakses Sein dengan Port 80 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan dan request dari client yang mengakses Stark dengan port 443 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan.
#### Script
##### Sein
```
apt-get install nginx -y

echo '
    <h1>Sein nih boss</h1>
' >/var/www/html/index.nginx-debian.html

echo 'server {
        listen 80 default_server;
        listen 443 default_server;
        listen [::]:80 default_server;

        root /var/www/html;
        index index.html index.htm index.nginx-debian.html;

        server_name _;

        location / {
            try_files $uri $uri/ =404;
        }
}' >/etc/nginx/sites-available/default

service nginx restart

iptables -A INPUT -p tcp --dport 443 -j ACCEPT
iptables -A INPUT -p tcp --dport 80 -j ACCEPT

iptables -t nat -A PREROUTING -p tcp --dport 80 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 10.51.14.138:80
iptables -t nat -A POSTROUTING -p tcp --dport 80 -j SNAT --to-source 10.51.8.2
```
- `-m statistic --mode nth --every 2 --packet 0`: Menggunakan DNAT setiap dua paket, aturan akan diterapkan pada setiap paket ke-2 yang masuk.
- `-j DNAT --to-destination 10.51.14.138:80`: Menetapkan paket-paket tersebut ke alamat IP tujuan 10.51.14.138 pada port 80.
- `-j SNAT --to-source 10.51.8.2`: Melakukan Source NAT pada paket-paket tersebut mengganti alamat sumber dengan 10.51.8.2.
##### Stark
```
apt-get install nginx -y

echo '
    <h1>Stark nih boss</h1>
' >/var/www/html/index.nginx-debian.html

echo 'server {
        listen 80 default_server;
        listen 443 default_server;
        listen [::]:80 default_server;

        root /var/www/html;
        index index.html index.htm index.nginx-debian.html;

        server_name _;

        location / {
            try_files $uri $uri/ =404;
        }
}' >/etc/nginx/sites-available/default

service nginx restart

iptables -A INPUT -p tcp --dport 443 -j ACCEPT
iptables -A INPUT -p tcp --dport 80 -j ACCEPT

iptables -t nat -A PREROUTING -p tcp --dport 443 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 10.51.8.2:443
iptables -t nat -A POSTROUTING -p tcp --dport 443 -j SNAT --to-source 10.51.14.138
```
##### GrobeForest
```
curl 10.51.14.138:443
curl 10.51.8.2:80
```
#### Testing
![image](https://github.com/AdonisZK/Jarkom-Modul-5-E29-2023/assets/48209612/fc8acf8f-1701-46f1-9fa9-0d57eb32a70b)

### 8. Karena berbeda koalisi politik, maka subnet dengan masyarakat yang berada pada Revolte dilarang keras mengakses WebServer hingga masa pencoblosan pemilu kepala suku 2024 berakhir. Masa pemilu (hingga pemungutan dan penghitungan suara selesai) kepala suku bersamaan dengan masa pemilu Presiden dan Wakil Presiden Indonesia 2024.
#### Script
##### Stark, Sein - Web Server
```
iptables -A INPUT -s 10.51.14.130 -m time --datestart 2024-02-14T00:00:00 --datestop 2024-06-26T23:59:59 -j DROP
```
- `-s 10.51.14.130`: IP Revolte
- `--datestart 2024-02-14T00:00:00`: Menetapkan tanggal dan waktu awal 14 Februari 2024 pukul 00:00:00
- `--datestop 2024-06-26T23:59:59`: Menetapkan tanggal dan waktu akhir 26 Juni 2024 pukul 23:59:59
- Waktu 14 Feb - 26 Jun diambil dari screenshot mba elshe
#### Testing
![image](https://github.com/AdonisZK/Jarkom-Modul-5-E29-2023/assets/48209612/91498d8a-f5d8-42d8-bb15-7b9302661edb)
- Percobaan pertama `success` karena diluar waktu yang dilarang
- Percobaan kedua `failed` karena dalam jangka waktu yang dilarang
### 9. Sadar akan adanya potensial saling serang antar kubu politik, maka WebServer harus dapat secara otomatis memblokir  alamat IP yang melakukan scanning port dalam jumlah banyak (maksimal 20 scan port) di dalam selang waktu 10 menit. 
(clue: test dengan nmap)
#### Script
##### Stark, Sein - Web Server
```
iptables -A INPUT -m recent --name portscan --update --seconds 600 --hitcount 20 -j DROP
iptables -A FORWARD -m recent --name portscan --update --seconds 600 --hitcount 20 -j DROP
```
##### GrobeForest
```
date -s "13 FEB 2024 11:20:00"
ping 10.51.14.138 -c 25
```
#### Testing
![image](https://github.com/AdonisZK/Jarkom-Modul-5-E29-2023/assets/48209612/4433727b-d327-4aff-ad87-7393e0418156)
- Hanya 20 paket yang diterima, dan sisanya akan ditolak
### 10. Karena kepala suku ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level. 
#### Script
#### Testing
