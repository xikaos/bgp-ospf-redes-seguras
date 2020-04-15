# Redes Seguras - Roteamento
## ISP
### AS65300-B0
enable
conf t
hostname AS65300-B0
no ip domain-lookup
exit
wr

conf t
#### int e0/0
ip addr 192.168.1.1 255.255.255.252
no shut
exit

#### int e0/1
ip addr 192.168.2.1 255.255.255.252
no shut
exit
exit 
wr

conf t
#### router bgp 65300
neighbor 192.168.1.2 remote-as 65100
neighbor 192.168.2.2 remote-as 65100
redistribute connected
end
wr
exit

### PAE-BORDER01
enable
conf t
hostname PAE-BORDER01
no ip domain-lookup
exit
wr

conf t
#### int e0/0
ip addr 192.168.4.1 255.255.255.252
no shut
exit

#### int e0/1
ip addr 192.168.5.1 255.255.255.252
no shut
exit

#### int e0/2
ip addr 192.168.3.1 255.255.255.252
no shut
exit

#### int e0/3
ip addr 192.168.1.2 255.255.255.252
no shut
exit
exit
wr

conf t
#### router bgp 65100
neighbor 192.168.1.1 remote-as 65300
neighbor 192.168.3.2 remote-as 65100
redistribute connected
bgp redistribute-internal
end
wr

conf t
#### router ospf 1
network 192.168.4.1 0.0.0.0 area 0
network 192.168.5.1 0.0.0.0 area 0
redistribute connected subnets
redistribute bgp 65100 subnets
end
wr

### FNL-BORDER01
enable
conf t
hostname FNL-BORDER0
no ip domain-lookup
exit
wr

conf t
#### int e0/0
ip addr 192.168.6.1 255.255.255.252
no shut 
exit

#### int e0/1
ip addr 192.168.7.1 255.255.255.252
no shut
exit

#### int e0/2
ip addr 192.168.3.2 255.255.255.252
no shut
exit


#### int e0/3
ip addr 192.168.2.2 255.255.255.252
no shut
exit
exit
wr

conf t
#### router bgp 65100
neighbor 192.168.2.1 remote-as 65300
neighbor 192.168.3.1 remote-as 65100
redistribute connected
bgp redistribute-internal
end
wr

conf t
#### router ospf 1
network 192.168.6.1 0.0.0.0 area 0
network 192.168.7.1 0.0.0.0 area 0
redistribute bgp 65100 subnets
redistribute connected subnets
end
wr


### PAE-DIST01
enable
conf t
hostname PAE-DIST01
no ip domain-lookup
exit
wr

conf t
#### int e1/0
ip addr 192.168.4.2 255.255.255.252
no shut
exit

#### int e0/3
ip addr 192.168.8.1 255.255.255.252
no shut
exit

#### int e0/0
ip addr 192.168.10.1 255.255.255.252
no shut
exit

#### int e0/1
ip addr 192.168.11.1 255.255.255.252
no shut
exit

#### int e0/2
ip addr 192.168.12.1 255.255.255.252
no shut
exit

#### router ospf 1
network 192.168.4.2 0.0.0.0 area 0
network 192.168.8.1 0.0.0.0 area 0
end

wr


### PAE-DIST02
enable
conf t
hostname PAE-DIST02
no ip domain-lookup
exit
wr

conf t
#### int e1/0
ip addr 192.168.5.2 255.255.255.252
no shut
exit

#### int e0/3
ip addr 192.168.8.2 255.255.255.252
no shut
exit

#### int e0/0
ip addr 192.168.13.1 255.255.255.252
no shut
exit

#### int e0/1
ip addr 192.168.14.1 255.255.255.252
no shut
exit

#### int e0/2
ip addr 192.168.15.1 255.255.255.252
no shut
exit

#### router ospf 1
network 192.168.8.2 0.0.0.0 area 0
network 192.168.5.2 0.0.0.0 area 0
end
exit
wr

### FNL-DIST01
enable
conf t
hostname FNL-DIST01
no ip domain-lookup
exit
wr

conf t
#### int e1/0
ip addr 192.168.9.1 255.255.255.252
no shut
exit

#### int e1/1
ip addr 192.168.6.2 255.255.255.252
no shut
exit

#### int e0/0
ip addr 192.168.16.1 255.255.255.252
no shut
exit

#### int e0/1
ip addr 192.168.17.1 255.255.255.252
no shut
exit

#### int e0/2
ip addr 192.168.18.1 255.255.255.252
no shut
exit

#### int e0/3
ip addr 192.168.19.1 255.255.255.252
no shut
exit

#### int e1/2
ip addr 192.168.20.1 255.255.255.252
no shut
exit


#### router ospf 1
network 192.168.9.1 0.0.0.0 area 0
network 192.168.6.2 0.0.0.0 area 0
end
exit
wr

### FNL-DIST02
enable
conf t
hostname FNL-DIST02
no ip domain-lookup
exit
wr

conf t
#### int e1/0
ip addr 192.168.9.2 255.255.255.252
no shut
exit

#### int e1/1
ip addr 192.168.7.2 255.255.255.252
no shut
exit

#### int e0/0
ip addr 192.168.21.1 255.255.255.252
no shut
exit

#### int e0/1
ip addr 192.168.22.1 255.255.255.252
no shut
exit

#### int e0/2
ip addr 192.168.23.1 255.255.255.252
no shut
exit

#### int e0/3
ip addr 192.168.23.1 255.255.255.252
no shut
exit

#### int e1/2
ip addr 192.168.24.1 255.255.255.252
no shut
exit

#### router ospf 1
network 192.168.9.2 0.0.0.0 area 0
network 192.168.7.2 0.0.0.0 area 0
end
exit
wr

### CSL-ACESSO01
enable
conf t
hostname CSL-ACCESSO01
no ip domain-lookup
exit
wr

conf t
#### int e0/0
ip addr 192.168.10.2 255.255.255.252
no shut
exit

#### int e0/1
ip addr 192.168.13.2 255.255.255.252
no shut
exit


### SMA-ACESSO01
enable
conf t
hostname SMA-ACCESSO01
no ip domain-lookup
exit
wr

conf t
#### int e0/0
ip addr 192.168.11.2 255.255.255.252
no shut
exit

#### int e0/1
ip addr 192.168.14.2 255.255.255.252
no shut
exit

### PAE-ACESSO01
enable
conf t
hostname PAE-ACCESSO01
no ip domain-lookup
exit
wr

conf t
#### int e0/0
ip addr 192.168.12.2 255.255.255.252
no shut
exit

#### int e0/1
ip addr 192.168.15.2 255.255.255.252
no shut
exit

### FNL-ACESSO01
enable
conf t
hostname FNL-ACCESSO01
no ip domain-lookup
exit
wr

conf t
#### int e0/0
ip addr 192.168.16.2 255.255.255.252
no shut
exit

#### int e0/1
ip addr 192.168.21.2 255.255.255.252
no shut
exit

### BNU-ACESSO01
enable
conf t
hostname BNU-ACCESSO01
no ip domain-lookup
exit
wr

conf t
#### int e0/0
ip addr 192.168.17.2 255.255.255.252
no shut
exit

#### int e0/1
ip addr 192.168.22.2 255.255.255.252
no shut
exit


### XAP-ACESSO01
enable
conf t
hostname XAP-ACCESSO01
no ip domain-lookup
exit
wr

conf t
#### int e0/0
ip addr 192.168.18.2 255.255.255.252
no shut
exit

#### int e0/1
ip addr 192.168.23.2 255.255.255.252
no shut
exit

### CCM-ACESSO01
enable
conf t
hostname CCM-ACCESSO01
no ip domain-lookup
exit
wr

conf t
#### int e0/0
ip addr 192.168.19.2 255.255.255.252
no shut
exit

#### int e0/1
ip addr 192.168.23.2 255.255.255.252
no shut
exit

### JOI-ACESSO01
enable
conf t
hostname JOI-ACCESSO01
no ip domain-lookup
exit
wr

conf t
#### int e0/0
ip addr 192.168.20.2 255.255.255.252
no shut
exit

#### int e0/1
ip addr 192.168.24.2 255.255.255.252
no shut
exit

