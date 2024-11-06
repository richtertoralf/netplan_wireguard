# netplan_wireguard
schnelle Variante einer Wireguard-Installation mit netplan unter Ubuntu 24.04 Server

## Installation
```
sudo apt install wireguard
```
## netplan Konfiguration
Tunnel (tunnels) einfügen.
```
network:
  version: 2
  ethernets:
    eno1:
      dhcp4: true
  tunnels:
    client16:
      mode: wireguard
      port: 51821
      key: xxxxxxxxxxxxxxxxxxxxxx=
      addresses:
        - 172.16.90.16/32
      peers:
        - allowed-ips: [172.16.90.0/24]
          endpoint: xxx.xxx.xxx.xxx:51820
          keepalive: 20
          keys:
            public: zzzzzzzzzzzzzzzzzzzzzzzzzzz=
      routes:
        - to: 172.16.90.0/24
          from: 172.16.90.16
          scope: link
```
```
netplan aply
```
