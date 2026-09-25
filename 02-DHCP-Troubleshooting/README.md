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

- DHCP Enabled
- DHCP Server
- IPv4 Address
- Subnet Mask
- Default Gateway
- DNS Servers
- Lease Obtained
- Lease Expires

---

# Dzierżawa DHCP

- Przykład:
- Lease Obtained: 21.09 23:35
- Lease Expires:  22.09 23:35

Adres z DHCP jest przydzielany na określony czas.
Windows może próbować odnowić dzierżawę zanim całkowicie wygaśnie.

---

# `ipconfig /release`

Powoduje zwolnienie aktualnej dzierżawy DHCP.

Po wykonaniu komendy komputer może stracić:

prawidłowy adres IPv4
bramę IPv4
dostęp do innych sieci

Podczas laba Windows otrzymał adres APIPA.