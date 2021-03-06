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
neighbor 192.168.1.2 default-originate
neighbor 192.168.2.2 default-originate
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
ip ospf network point-to-point
ip ospf 1 area 0
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
redistribute ospf 1
bgp redistribute-internal
end
wr

conf t
#### router ospf 1
network 192.168.4.1 0.0.0.0 area 0
network 192.168.5.1 0.0.0.0 area 0
redistribute connected subnets
redistribute bgp 65100 subnets
default-information originate always
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
ip ospf network point-to-point
ip ospf 1 area 0
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
redistribute ospf 1
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
default-information originate always
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
network 192.168.10.1 0.0.0.0 area 10
network 192.168.11.1 0.0.0.0 area 11
network 192.168.12.1 0.0.0.0 area 12
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
network 192.168.13.1 0.0.0.0 area 10
network 192.168.14.1 0.0.0.0 area 11
network 192.168.15.1 0.0.0.0 area 12
end
wr
exit

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
network 192.168.16.1 0.0.0.0 area 16
network 192.168.17.1 0.0.0.0 area 17
network 192.168.18.1 0.0.0.0 area 18
network 192.168.19.1 0.0.0.0 area 19
network 192.168.20.1 0.0.0.0 area 20
end
wr
exit

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
ip addr 192.168.24.1 255.255.255.252
no shut
exit

#### int e1/2
ip addr 192.168.25.1 255.255.255.252
no shut
exit

#### router ospf 1
network 192.168.9.2 0.0.0.0 area 0
network 192.168.7.2 0.0.0.0 area 0
network 192.168.21.1 0.0.0.0 area 16
network 192.168.22.1 0.0.0.0 area 17
network 192.168.23.1 0.0.0.0 area 18
network 192.168.24.1 0.0.0.0 area 19
network 192.168.25.1 0.0.0.0 area 20
end
wr
exit

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

#### router ospf 1
network 192.168.10.2 0.0.0.0 area 10
network 192.168.13.2 0.0.0.0 area 10
end
wr
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

#### router ospf 1
network 192.168.11.2 0.0.0.0 area 11
network 192.168.14.2 0.0.0.0 area 11
end
wr
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

#### router ospf 1

network 192.168.12.2 0.0.0.0 area 12  
network 192.168.15.2 0.0.0.0 area 12  
end  
wr
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

#### router ospf 1

network 192.168.16.2 0.0.0.0 area 16 
network 192.168.21.2 0.0.0.0 area 16  
end  
wr
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

#### router ospf 1

network 192.168.17.2 0.0.0.0 area 17
network 192.168.22.2 0.0.0.0 area 17  
end  
wr
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

#### router ospf 1

network 192.168.18.2 0.0.0.0 area 18
network 192.168.23.2 0.0.0.0 area 18  
end  
wr
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
ip addr 192.168.24.2 255.255.255.252
no shut
exit

#### router ospf 1

network 192.168.19.2 0.0.0.0 area 19
network 192.168.24.2 0.0.0.0 area 19
end  
wr
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
ip addr 192.168.25.2 255.255.255.252
no shut
exit

#### router ospf 1

network 192.168.20.2 0.0.0.0 area 20
network 192.168.25.2 0.0.0.0 area 20  
end  
wr
exit

### PFSense
1. Subir appliance dentro do lab.
2. Configurar interface LAN para `vtnet0`.
3. Conectar a network `Management` em e0/0.
4. Configurar o IP da interface `vtnet0` dentro do range da VM do Eve.
5. Fazer login na VM do Eve.
6. Tunelar a conexão entre a VM do Eve e o host pelo comando `ssh -L ip_maquina_eve:3000:ip_maquina_pfsense:80 root@ip_maquina_eve`. 
7. Testar o acesso. É necessário obter um erro relativo a verificação do cabeçalho `Referer` do HTTP.
8. Acesse o shell da máquina do PFSense selecionando a opção 8 via console.
9. Execute o comando para desabilitar a verficação do cabeçalho HTTP: `pfSsh.php playback disablereferercheck`
10. Acesse a interface web e configure o firewall
