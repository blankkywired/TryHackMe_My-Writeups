---
tags:
  - "#THM-Path-Notes"
  - Cybersecurity-101
  - Network
---
Room link: [https://tryhackme.com/room/nmap](https://tryhackme.com/room/nmap)


---


# Table of Contents

- [[#Host Discovery: Who is online]]
- [[#Port Scanning: Who is listening]]
- [[#Version Detection: Extract More Information]]
- [[#Timing: How Fast is Fast]]


## Host Discovery: Who is online

1 ==**Question**==: **What is the last IP address that will be scanned when your scan target is `192.168.0.1/27`?**

R: Usando uma calculadora de CIDR IP, podemos encontrar o range do IP e quantos hosts o IP (192.168.0.1/27) suporta, sendo a notação [/ < n >] que determina quantos bits são da rede e quantos bits são do host, exemplo: 192.168.0.1/27 significa que 27 bits servem para identificar a rede, sobrando apenas 5 bits disponiveis para identificar os hosts
	
R: O ultimo IP Address é 192.168.0.31

![[image-3.png]]
## Port Scanning: Who is listening

1 ==**Question**==: **How many TCP ports are open on the target system at `10.64.163.223`?**

R: Usando o comando: nmap -sS <MACHINE_IP> achamos todos os serviços com portas abertas da maquina, totalizando 6 portas tcp abertas
 
![[image_1_.png]]

 2 ==**Question**==: **Find the listening web server on `10.64.163.223` and access it with your browser. What is the flag that appears on its main page?**

Para acessar a flag, eu coloco o endereço ip do alvo junto com a porta em que está rodando o serviço(server http na porta 8008) como url no navegador
 
![[image_2_.png]]
## Version Detection: Extract More Information
1 ==**Question**==**:** **What is the name and detected version of the web server running on `10.64.163.223`?**

Usando o comando nmap -sV <MACHINE_IP> encontramos tambem as versões possiveis dos serviços que estão rodando, o servidor http ta rodando um software chamado lighttpd 1.4.74
	
![[image_3_-2.png]]

## Timing: How Fast is Fast
