# Lab 4

**Author: Benjamin Medicke**<br>
**Topics: IPSec VPN**

[lab1](lab1.md) | [lab2](lab2.md) | [lab3](lab3.md) | **lab4**

---

<!-- vim-markdown-toc GFM -->

* [Lab 4.1 IPSec VPN](#lab-41-ipsec-vpn)
  * [4.1.1 Aktivieren von IPSec VPN](#411-aktivieren-von-ipsec-vpn)
  * [4.1.2 Erstellen eines neuen Interoprable Devices](#412-erstellen-eines-neuen-interoprable-devices)
  * [4.1.3 Erstellen einer neuen Meshed VPN Community](#413-erstellen-einer-neuen-meshed-vpn-community)
  * [4.1.4 Neue Firewall Regel](#414-neue-firewall-regel)
  * [4.1.5 Gateway Objekt Eigentschaften anpassen](#415-gateway-objekt-eigentschaften-anpassen)
  * [4.1.7 Testen der Erreichbarkeit via VPN Tunnel](#417-testen-der-erreichbarkeit-via-vpn-tunnel)
  * [4.1.8 Erlauben von SSH Traffic](#418-erlauben-von-ssh-traffic)
  * [4.1.9 Log des Blades: VPN](#419-log-des-blades-vpn)
  * [4.1.10 Verbinden mit der Firewall via SSH](#4110-verbinden-mit-der-firewall-via-ssh)
  * [Aufgetretene Probleme](#aufgetretene-probleme)

<!-- vim-markdown-toc -->

## Lab 4.1 IPSec VPN

### 4.1.1 Aktivieren von IPSec VPN

> ![image](https://user-images.githubusercontent.com/173962/118393849-84ad2000-b641-11eb-80ec-2da58442c6ea.png)
>
> "IPSec VPN" Blade aktiviert

> ![image](https://user-images.githubusercontent.com/173962/118395165-25eba480-b649-11eb-8cba-9a4058a030ac.png)
>
> IPSec VPN Einstellungen

### 4.1.2 Erstellen eines neuen Interoperable Devices

> ![image](https://user-images.githubusercontent.com/173962/118395513-13726a80-b64b-11eb-8732-0ec9ff9e744a.png)
>
> Anlegen eines neuen Interoperable Devices: 2 Interfaces

> ![image](https://user-images.githubusercontent.com/173962/118395772-70baeb80-b64c-11eb-84be-835f1a38b72d.png)
>
> Objekt zur Abbildung des internen Partnersubnetzwerkes

> ![image](https://user-images.githubusercontent.com/173962/118395797-934d0480-b64c-11eb-9478-c29d98990271.png)
>
> Auswahl der VPN Domain

### 4.1.3 Erstellen einer neuen Meshed VPN Community

> ![image](https://user-images.githubusercontent.com/173962/118395850-df984480-b64c-11eb-87a0-5534185cf663.png)
>
> Neues Meshed VPN Community Objekt

> ![image](https://user-images.githubusercontent.com/173962/118395904-356cec80-b64d-11eb-9953-e115e2740070.png)
>
> Festelegen eines Shared Secrets (PSK)

> ![image](https://user-images.githubusercontent.com/173962/118395922-49b0e980-b64d-11eb-805a-b8d177ebdc44.png)
>
> Deaktivieren von NAT innerhalb der VPN Community

### 4.1.4 Neue Firewall Regel

Diese neue Regel erlaubt den Traffic von der eigenen Linux Instanz auf die des Kollegen.

> ![image](https://user-images.githubusercontent.com/173962/118396162-7a455300-b64e-11eb-8daa-3b2741fa328a.png)
>
> Bidirektionale Kommunikation zwischen den VPN Teilnehmern erlauben

### 4.1.5 Gateway Objekt Eigentschaften anpassen

> ![image](https://user-images.githubusercontent.com/173962/118396212-c2647580-b64e-11eb-8c19-6f4b18f7e735.png)
>
> Die Einstellungen waren bereits OK

### 4.1.7 Testen der Erreichbarkeit via VPN Tunnel

> ![image](https://user-images.githubusercontent.com/173962/118396309-356dec00-b64f-11eb-9035-7c6186eeff81.png)
>
> VPN Tunnel wird automatisch aufgebaut und funktioniert

### 4.1.8 Erlauben von SSH Traffic

> ![image](https://user-images.githubusercontent.com/173962/118396425-c80e8b00-b64f-11eb-8401-a182be5900b4.png)
>
> Der Tunnel ist funktionsfähig (SSH Verbindung scheitert nur an nicht vorhandenem Public Key)

> ![image](https://user-images.githubusercontent.com/173962/118396624-a3ff7980-b650-11eb-8e03-7855a6c3ff8a.png)
>
> `curl` auf Python Webserver, der bei meinem Kollegen läuft (`python3 -m http.server 1234`) funktioniert

### 4.1.9 Log des Blades: VPN

>![image](https://user-images.githubusercontent.com/173962/118396912-f725fc00-b651-11eb-8785-510ca482fb42.png)
>
>

### 4.1.10 Verbinden mit der Firewall via SSH

<!-- Suchen Sie sich aus dem Log die Einträge für den Verbindungsaufbau (IPSec Phase 1 und Phase 2) heraus und legen Sie diese der Dokumentation bei. -->

> ![image](https://user-images.githubusercontent.com/173962/118397115-c5f9fb80-b652-11eb-9185-20c0950da7ba.png)
>
> IKE Security Associations via `vpn tu`

> ![image](https://user-images.githubusercontent.com/173962/118397154-ee81f580-b652-11eb-99dc-0bdc1091bceb.png)
>
> IPSec Security Associations via `vpn tu`


> ![image](https://user-images.githubusercontent.com/173962/118397367-db235a00-b653-11eb-88af-e2657af6bc31.png)
>
> Neustart des Tunnels durch Löschen der Associations

#### a. Verbindungsaufbau

> ![image](https://user-images.githubusercontent.com/173962/118398370-89c99980-b658-11eb-8312-3448a232170f.png)
>
> Sequence Number 1: IKE Phase 1 (AES-256 + Group 2, PSK)

> ![image](https://user-images.githubusercontent.com/173962/118398287-348d8800-b658-11eb-9e3a-eb75372dbc6a.png)
>
> Sequence Number 2: IKE Phase 2 (AES-128 + SHA1)

#### b. IPSec Parameterwahl

*Welche IPSec Parameter haben Sie verwendet bzw. sind empfehlenswert?*



### Aufgetretene Probleme
