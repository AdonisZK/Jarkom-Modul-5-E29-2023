# Jarkom-Modul-5-E29-2023

### (A) Tugas pertama, buatlah peta wilayah sesuai berikut ini:
### (B) Untuk menghitung rute-rute yang diperlukan, gunakan perhitungan dengan metode VLSM. Buat juga pohonnya, dan lingkari subnet yang dilewati.
#### Topologi
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
