# Jarkom-Modul-5-E29-2023
## Anggota
Kelompok E29
| Nama | NRP |
| --- | --- |
| Sony Hermawan | 5025211226 |
| Sekar Ambar Arum | 5025211041 |

# Laporan Resmi

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
```
IPETH0="$(ip -br a | grep eth0 | awk '{print $NF}' | cut -d'/' -f1)"
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source "$IPETH0" -s 10.51.0.0/20
```
