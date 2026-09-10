# Lab 01 - Diagnostyka sieci w Windows



## Cel Laboratorium 



Celem tego laba było przećwiczenie podstawowej diagnostyki sieciowej na Windows 11 z perspektywy osoby pracującej na Helpdesk.

Środowisko:
- Windows 11 VM
- NAT

## Co przećwiczyłem 

- sprawdzanie informacji aktualnej sieci przez `ipconfig /all`
- testy połączenia za pomocą `ping`
- diagnostykę DNS przy użyciu komendy `nslookup`
- czyszczenie cache DNS `ipconfig /flushdns`
- sprawdzenie trasy przez `tracert`
- symulację błędnego DNS
- symulację braku bramy IPv4
- diagnozę zgłoszenia "brak internetu"

# `ipconfig /all`

IPv4:        10.0.2.15
Maska:       255.255.255.0
Gateway:     10.0.2.2
DHCP:        Yes
DNS:         192.168.50.1

# APIPA

Adres typu 169.254.x.x mogą zostać automatycznie przypisane przez windows, gdy komputer nie otrzyma adresu ip od DHCP

Może to oznaczać że problem występuje z:
- DHCP
- kartą sieciową 
- Wi-Fi/kablem
- switchem
- VLAN-em  (?)
- serwerem DHCP

Prywatne zakresy IPv4:
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16

APIPA nie należy do standardowych zakresów prywatnych prywatnych RFC1918 (?)

# PING

Podstawowa kolejność testów
ping 127.0.0.1
ping <własne_IP>
ping <gateway>
ping 8.8.8.8
ping google.com

ping Gateway -> działa = Komunikacja z lokalną bramą działa. 
ping 8.8.8.8 -> działa = Komputer posiada komunikację poza siecią lokalną.
ping google.com -> nie działa = Komputer nie potrafi rozwiązać nazwy domenowej 
Brak odpowiedzi na `ping` nie zawsze oznacza awarię. ICMP (?) może być blokowany przez firewall.
