# Junior Network Administrator - LSP BNSP

- [ ] J.611000.004.01 | Merancang pengalamatan jaringan
- [ ] J.611000.010.02 | Memasang jaringan nirkabel
- [ ] J.611000.012.02 | Mengkonfigurasi switch pada jaringan
- [ ] J.611000.013.02 | Mengkonfigurasi routing pada perangkat jaringan dalam satu autonomous system
- [ ] J.611000.014.02 | Mengkonfigurasi routing pada perangkat jaringan antar autonomous system

# Practice Test

## Topologi

![Topologi](https://user-images.githubusercontent.com/104877293/168695145-0b7ee189-2957-425d-a9d6-58c0c728b11a.png)

# Step 1: Konfigurasi ip address pada setiap interface

## Router RM1
Konfigurasi mengalamatan ip address pada router RM1
```sh
   Router>en
   Router#conf t
   Router(config)#hostname RM1
   RM1(config)#int gig0/2
   RM1(config-if)#ip add 192.168.20.1 255.255.255.224
   RM1(config-if)#no sh
   RM1(config-if)#ex
   RM1(config)#service dhcp
   RM1(config)#ip dhcp pool RMarea
   RM1(dhcp-config)#default-router 192.168.20.1
   RM1(dhcp-config)#dns-server 8.8.8.8
   RM1(dhcp-config)#ex
   RM1(config)#int gig 0/1
   RM1(config-if)#ip add 12.10.10.1 255.255.255.252
   RM1(config-if)#no sh
   RM1(config-if)#ex
   RM1(config)#int gig 0/0
   RM1(config-if)#ip add 20.2.2.1 255.255.255.252
   RM1(config-if)#no sh
   RM1(config-if)#ex
   ```
## Router RM2
Konfigurasi mengalamatan ip address pada router RM2
```sh
   Router>en
   Router#conf t
   Router(config)#hostname RM2
   RM2(config)#int gig0/0
   RM2(config-if)#ip add 12.10.10.2 255.255.255.252
   RM2(config-if)#no sh
   RM2(config-if)#ex
   RM2(config)#int gig0/1
   RM2(config-if)#ip add 13.10.10.1 255.255.255.252
   RM2(config-if)#no sh
   RM2(config-if)#ex
   ```
## Router RM3
Konfigurasi mengalamatan ip address pada router RM3
```sh
   Router>en
   Router#conf t
   Router(config)#hostname RM3
   RM3(config)#int gig0/0
   RM3(config-if)#ip add 20.2.2.2 255.255.255.252
   RM3(config-if)#no sh
   RM3(config-if)#ex
   RM3(config)#int gig0/1
   RM3(config-if)#ip add 10.1.1.1 255.255.255.252
   RM3(config-if)#no sh
   RM3(config-if)#ex
   ```
## Router RS
Konfigurasi mengalamatan ip address pada router RS
```sh
   Router>en
   Router#conf t
   Router(config)#hostname RS
   RS(config)#int gig0/0
   RS(config-if)#ip add 10.1.1.2 255.255.255.252
   RS(config-if)#no sh
   RS(config-if)#ex
   RS(config)#int gig0/1
   RS(config-if)#ip add 192.168.10.1 255.255.255.128
   RS(config-if)#no sh
   RS(config-if)#ex
   RS(config)#service dhcp
   RS(config)#ip dhcp pool RSarea
   RS(dhcp-config)#net 192.168.10.0 255.255.255.128
   RS(dhcp-config)#default-router 192.168.10.1
   RS(dhcp-config)#dns-server 8.8.8.8
   RS(dhcp-config)#ex
   ```
## Router RK2
Konfigurasi mengalamatan ip address pada router RK2
```sh
   Router>en
   Router#conf t
   Router(config)#hostname RK2
   RK2(config)#int gig0/0
   RK2(config-if)#ip add 13.10.10.2 255.255.255.252
   RK2(config-if)#no sh
   RK2(config-if)#ex
   RK2(config)#int gig0/1
   RK2(config-if)#ip add 30.3.3.1 255.255.255.248
   RK2(config-if)#no sh
   RK2(config-if)#ex
   ```
## Router RK1
Konfigurasi mengalamatan ip address pada router RK1
```sh
   Router>en
   Router#conf t
   Router(config)#hostname RK1
   RK1(config)#int gig0/0
   RK1(config-if)#ip add 30.3.3.2 255.255.255.248
   RK1(config-if)#no sh
   RK1(config-if)#ex
   RK1(config)#int gig0/1
   RK1(config-if)#ip add 192.168.30.1 255.255.255.0
   RK1(config-if)#no sh
   RK1(config-if)#ex
   R1(config)#service dhcp
   R1(config)#ip dhcp pool RKarea
   R1(dhcp-config)#net 192.168.30.0 255.255.255.0
   R1(dhcp-config)#default-router 192.168.30.1
   R1(dhcp-config)#dns-server 8.8.8.8
   R1(dhcp-config)#ex
   R1(config)#
   ```
 
# Step 2: Konfigurasi Routing pada masing-masing Router
  
## Area RM menggunakan Routing Static

Konfigurasi Routing Static pad RM1

```sh
   RM1(config)#ip route 13.10.10.0 255.255.255.252 12.10.10.2
   RM1(config)#ip route 30.3.3.0 255.255.255.248 12.10.10.2
   RM1(config)#ip route 192.168.30.0 255.255.255.0 12.10.10.2
   RM1(config)#ip route 192.168.10.0 255.255.255.128 20.2.2.2
   RM1(config)#ip route 10.1.1.0 255.255.255.252 20.2.2.2
   ```
   
Konfigurasi Routing Static pad RM2
```sh
   RM2(config)#ip route 192.168.20.0 255.255.255.224 12.10.10.1
   RM2(config)#ip route 20.2.2.0 255.255.255.252 12.10.10.1
   RM2(config)#ip route 10.1.1.0 255.255.255.252 12.10.10.1
   RM2(config)#ip route 192.168.10.0 255.255.255.128 12.10.10.1
   ```

Konfigurasi Routing Static pad RM3
```sh
   RM3(config)#ip route 192.168.20.0 255.255.255.224 20.2.2.1
   RM3(config)#ip route 12.10.10.0 255.255.255.252 20.2.2.1
   RM3(config)#ip route 13.10.10.0 255.255.255.252 20.2.2.1
   RM3(config)#ip route 30.3.3.0 255.255.255.248 20.2.2.1
   RM3(config)#ip route 192.168.30.0 255.255.255.252 20.2.2.1
   ```
   
## Area RS menggunakan Routing RIP

Konfigurasi Routing RIP pad RM3

```sh
RM3(config)#router rip
RM3(config-router)#net 10.1.1.0
RM3(config-router)#no auto-summary 
RM3(config-router)#ex
   ```
   
Konfigurasi Routing RIP pad RS
```sh
RS(config)#router rip
RS(config-router)#net 192.168.10.0
RS(config-router)#net 10.1.1.0
RS(config-router)#no auto-summary 
RS(config-router)#ex
   ```
## Area RM2 -> RK2 menggunakan Routing BGP

Konfigurasi Routing BGP pad RM2

```sh
RM2(config)#router bgp 100
RM2(config-router)#neighbor 13.10.10.2 remote-as 200
RM2(config-router)#ex
   ```
   
Konfigurasi Routing BGP pad RK2

```sh
RK2(config)#router bgp 200
RK2(config-router)#neighbor 13.10.10.1 remote-as 100
RK2(config-router)#ex
   ```
   
## Area RK menggunakan Routing OSPF

Konfigurasi Routing OSPF pad RK1
```sh
   RK1(config)#router ospf 20
   RK1(config-router)#net 192.168.30.0 0.0.0.255 area 0
   RK1(config-router)#net 30.3.3.0 0.0.0.7 area 0
   RK1(config-router)#ex
   ```

Konfigurasi Routing OSPF pad RK2
```sh
   RK2(config)#router ospf 20
   RK2(config-router)#network 30.3.3.0 0.0.0.7 area 0
   RK2(config-router)#ex
   ```
   
# Step 3: Konfigurasi Redistribute pada Router RM2, RM3, RK2

## RM2
Konfigurasi RM2 Redistribute pada routing BGP
```sh
   RM2(config)#router bgp 100
   RM2(config-router)#redistribute static
   RM2(config-router)#redistribute connected
   RM2(config-router)#ex
   ```
## RK2
Konfigurasi RK2 Redistribute OSPF pada routing BGP
```sh
   RK2(config)#router bgp 200
   RK2(config-router)#redistribute ospf 20
   RK2(config-router)#ex
   ```
Konfigurasi RK2 Redistribute BGP pada routing OSPF
```sh
   RK2(config)#router ospf 20
   RK2(config-router)#redistribute ospf 20
   RK2(config-router)#redistribute bgp 200 subnets
   RK2(config-router)#ex
   ```

## RM3
Konfigurasi RM3 Redistribute Static pada Routing RIP
```sh
   RM3(config)#router rip
   RM2(config-router)#redistribute static
   RM2(config-router)#redistribute connected
   RM2(config-router)#ex
   ```
   
   
