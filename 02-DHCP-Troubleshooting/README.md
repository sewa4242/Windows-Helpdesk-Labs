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

- prawidłowy adres IPv4
- bramę IPv4
- dostęp do innych sieci

Podczas laba Windows otrzymał adres APIPA.

# `ipconfig /renew`

Klient próbuje ponownie uzyskać konfigurację z serwera DHCP.
Po poprawnym odnowieniu powinny wrócić m.in.:

- IPv4
- Subnet Mask
- Default Gateway
- DNS
- DHCP Server
- Lease Obtained
- Lease Expires

Nie ma gwarancji, że komputer zawsze otrzyma dokładnie ten sam adres IPv4.

# Sprawdzanie sprzętu

`devmgmt.msc` = Menadżer urządzeń

Sprawdzam:
- czy karta sieciowa jest widoczna
- czy jest włączona
- czy sterownik działa poprawnie
- czy nie występują błędy urządzenia

Brak błędów w Menedżerze urządzeń nie daje 100% pewności, że sprzęt jest sprawny.

# Sprawdzanie usługi DHCP Client

`services.msc` = Menadżer usług 

Warto sprawdzić usługę:
- Klient DHCP

Przykładowy problem:
- Status: Stopped
- Startup type: Disabled

Jeżeli polityka firmy na to pozwala, należy przywrócić prawidłową konfigurację usługi i ponownie spróbować: `ipconfig /renew`

# Praktyczny troubleshooting

Przy problemie z jednym komputerem warto sprawdzić: Czy problem idzie za komputerem. 

Można:
- podłączyć komputer do innego działającego portu
- użyć sprawdzonego kabla
- podłączyć komputer do kabla/portu działającego stanowiska

problem znika po zmianie kabla
-> podejrzenie kabla

problem znika po zmianie portu
-> podejrzenie portu / switcha / VLAN-u

problem nadal występuje na sprawdzonym kablu i porcie
-> podejrzenie samego komputera

# Końcowa weryfikacja 

Po uzyskaniu poprawnego adresu z DHCP nie zamykam od razu zgłoszenia.

Sprawdzam: 
- `ping Gateway`
- `ping 8.8.8.8`
- `nslookup google.com`

# Wnioski

- DHCP Enabled: Yes nie oznacza, że DHCP faktycznie zadziałało.
- 169.254.x.x to bardzo mocny sygnał problemu z uzyskaniem konfiguracji DHCP.
- ipconfig /release zwalnia dzierżawę.
- ipconfig /renew próbuje pobrać konfigurację ponownie.
- przy problemie jednego użytkownika najpierw warto wykluczyć kabel, port, kartę i konfigurację klienta.
- przy problemie wielu użytkowników bardziej podejrzana jest infrastruktura.
- po naprawie trzeba jeszcze potwierdzić działanie sieci i aplikacji użytkownika.
