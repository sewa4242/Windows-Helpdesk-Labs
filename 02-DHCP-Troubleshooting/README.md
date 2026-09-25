# 02 - DHCP Troubleshooting


## Cel laboratorium: 

Przećwiczenie diagnostyki problemów z DHCP w Windows 11. 

Środowisko:
- Windows 11 VM
- VirtualBox
- NAT / Internal Network

## Co udało mi się przećwiczyć:

- sprawdzanie konfiguracji DHCP przez `ipconfig /all`
- analizę dzierżawy DHCP
- `ipconfig /release`
- `ipconfig /renew`
- rozpoznawanie adresu APIPA
- diagnostykę braku adresu z DHCP
- sprawdzanie kabla, portu i karty sieciowej
- sprawdzanie usługi DHCP Client
- końcową weryfikację po naprawie

---

# DHCP w Windows 

DHCP może automatycznie dostarczyć komputerowi m.in.:

- adres IPv4
- maskę podsieci 
- bramę domyślną
- serwer DNS

W `ipconfig /all` warto sprawdzić:

DHCP Enabled
DHCP Server
IPv4 Address
Subnet Mask
Default Gateway
DNS Servers
Lease Obtained
Lease Expires