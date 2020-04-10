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
end
exit
wr

conf t
#### router ospf 1
network 192.168.4.1 0.0.0.0 area 0
network 192.168.5.1 0.0.0.0 area 0
end


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
end
wr

conf t
#### router ospf 1
network 192.168.6.1 0.0.0.0 area 0
network 192.168.7.1 0.0.0.0 area 0
end

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


#### router ospf 1
network 192.168.4.2 0.0.0.0 area 0
network 192.168.8.1 0.0.0.0 area 0
end


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

#### router ospf 1
network 192.168.8.2 0.0.0.0 area 0
network 192.168.5.2 0.0.0.0 area 0
end
exit
wr


