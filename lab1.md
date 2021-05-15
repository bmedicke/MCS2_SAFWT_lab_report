# Lab 1


<!-- vim-markdown-toc GFM -->

* [Lab 1.1 Connecting to Management](#lab-11-connecting-to-management)
* [Lab 1.2 SSH Connection to Linux Instance](#lab-12-ssh-connection-to-linux-instance)
  * [1.2.1 Subnet hinter NAT](#121-subnet-hinter-nat)
  * [1.2.2 Neue Policies](#122-neue-policies)
  * [1.2.3 Management Traffic & Stealth-Rule](#123-management-traffic--stealth-rule)
  * [1.2.4 Logging](#124-logging)
  * [1.2.5 Install Policy](#125-install-policy)
  * [1.2.6 Testen der SSH Keys](#126-testen-der-ssh-keys)
  * [Aufgetretene Probleme](#aufgetretene-probleme)
* [Lab 1.3 VNCServer & NAT Rules](#lab-13-vncserver--nat-rules)
  * [1.3.1 Regel erstellen: Internetzugriff für die Linux Instanz](#131-regel-erstellen-internetzugriff-für-die-linux-instanz)
  * [1.3.2 Login und Internet-Test](#132-login-und-internet-test)
  * [1.3.3 apt Installationen](#133-apt-installationen)
  * [1.3.4 VNC server starten](#134-vnc-server-starten)
  * [1.3.5 Erstellen von Security Policies](#135-erstellen-von-security-policies)
  * [1.3.6 Testen der VNC Verbindung](#136-testen-der-vnc-verbindung)
  * [1.3.7 Aufgetretene Probleme](#137-aufgetretene-probleme)

<!-- vim-markdown-toc -->

## Lab 1.1 Connecting to Management

Der Fingerprint des Servers, der bei der ersten Verbindung angezeigt wird ist:

`REAR NECK KICK TIP HOE DUET DALE GASH ECHO OW SHED TONE`

Er stimmt mit dem im Gaia Web Interface überein.

> ![image](https://user-images.githubusercontent.com/173962/116440505-dfc4d180-a850-11eb-9774-08411186ece4.PNG)
>
> Fingerprint im Gaia Web Interface

---

_Beantworten Sie die Frage: Welche Aufgaben hat der Fingerprint und welche Bedrohungen werden damit verhindert?_

Der Fingerprint garantiert die Authentizität des Servers. Falls der Server 'ausgetauscht' wird, können Man-In-The-Middle Angriffe erkannt werden. Wenn sich der Fingerprint geändert hat, deutet das auf eine Änderung des Private Keys des Servers hin. Dies kann darauf hinweisen, dass sich ein Angreifer als der Zielserver ausgiebt. Es sollte sichergestellt werden, dass der Server integer ist.

## Lab 1.2 SSH Connection to Linux Instance

### 1.2.1 Subnet hinter NAT

Anlegen eines neuen Netzwerkobjektes (Subnetz 192.168.20.0/24), welches mit NAT hinter der Firewall versteckt wird.

> ![image](https://user-images.githubusercontent.com/173962/116457764-19530800-a864-11eb-8acc-00c64e2c3783.png)
>
> Neues Netzwerkobjekt, Reiter: General

> ![image](https://user-images.githubusercontent.com/173962/116457797-24a63380-a864-11eb-8b16-17e8f28af12e.png)
>
> Neues Netzwerkobjekt, Reiter: NAT.<br>
> Aktivieren von "Add automatic address translation rule", "Hide" und "Hide behind the gateway".

Ebenso wurde ein Host-Objekt angelegt, welches die Linux Instanz (IP: `192.168.20.50`) abbildet.

> ![image](https://user-images.githubusercontent.com/173962/118277689-54427600-b4c9-11eb-821a-b2399cdb10d4.png)
>
> Neues Netzwerkobjekt: Linux Instance

### 1.2.2 Neue Policies

Anlegen neuer Policies um SSH Zugriff auf Linux Instanz zu ermöglichen. Beachte: Auf Port `22` läuft bereits der SSH Server der CloudGuard Instanz, daher wird hier `2222` Die folgenden Regeln wurden erstellt:

1. eine Firewallregel, die Port `2222` (für SSH) auf die CloudGuard Instanz erlaubt
2. eine NAT-Regel, die Port `2222` der CloudGuard Instanz auf `22` der Linux Instanz mappt 

> ![image](https://user-images.githubusercontent.com/173962/116458672-320fed80-a865-11eb-8964-93ca2058e15d.png)
>
> Neues TCP-Service-Object: SSH-access

> ![image](https://user-images.githubusercontent.com/173962/116462870-460a1e00-a86a-11eb-91e4-4a898ec0e51f.png)
>
> Firewallregel, die Port 2222 erlaubt.

> ![image](https://user-images.githubusercontent.com/173962/116461224-4bfeff80-a868-11eb-8dbc-87ca3f20934a.png)
>
> NAT Regel.

### 1.2.3 Management Traffic & Stealth-Rule

Hier werden zwei weitere Regeln erstellt:

1. Erlauben von Management-Traffic
2. Stealth Regel (restlichen Traffic droppen)

> ![image](https://user-images.githubusercontent.com/173962/118280320-6376f300-b4cc-11eb-98d2-ae16f2c2e0ae.png)
>
> Neue Management und Stealth Regeln

### 1.2.4 Logging

Jetzt wurde Logging für alle Regeln aktiviert (siehe vorherigen Screenshot).

### 1.2.5 Install Policy

Die Policies wurden mit "Install Policy" installiert.

>![image](https://user-images.githubusercontent.com/173962/118281344-658d8180-b4cd-11eb-9c90-0cce74d98c8c.png)
>
> Install Policy Button

### 1.2.6 Testen der SSH Keys

>![image](https://user-images.githubusercontent.com/173962/116460772-b82d3380-a867-11eb-914c-251b079ddaf4.png)
>
> Bei der initialen Verbindung wird der SSH key angezeigt. Dieser sollte verglichen und akzeptiert werden.


>![image](https://user-images.githubusercontent.com/173962/116462086-5a99e680-a869-11eb-8c1e-d9d56f243200.png)
>
> Erfolgreicher Login via SSH Key auf die Linux Instanz

>![image](https://user-images.githubusercontent.com/173962/116464247-08a69000-a86c-11eb-883b-5481d05206fc.png)
>
> Erfolgreicher Login via SSH Key auf die CloudGuard Instanz

### Aufgetretene Probleme

Es sind keine Probleme aufgetreten.

## Lab 1.3 VNCServer & NAT Rules

### 1.3.1 Regel erstellen: Internetzugriff für die Linux Instanz

>![image](https://user-images.githubusercontent.com/173962/118291355-cd48ca00-b4d7-11eb-9123-5c54ac9ad201.png)
>
> Policy, die Internetzugriff für die Linux Instanz erlaubt

>![image](https://user-images.githubusercontent.com/173962/118291408-dd60a980-b4d7-11eb-9d50-fce75bab26f3.png)
>
> Publish & Install

### 1.3.2 Login und Internet-Test

> ![image](https://user-images.githubusercontent.com/173962/118291914-64158680-b4d8-11eb-9e75-4f89c73b9a53.png)
>
> Der Ping geht durch!

### 1.3.3 apt Installationen

> ![image](https://user-images.githubusercontent.com/173962/118292217-b060c680-b4d8-11eb-84e5-b345d6a55627.png)
>
> `sudo apt update`

> ![image](https://user-images.githubusercontent.com/173962/118292526-02a1e780-b4d9-11eb-8959-95c6d234bbab.png)
>
> `sudo apt install xfce4 xfce4-goodies`

>![image](https://user-images.githubusercontent.com/173962/118292823-53194500-b4d9-11eb-967c-2c7571bb2338.png)
>
> Was eine Weile dauert.

> ![image](https://user-images.githubusercontent.com/173962/118292958-73e19a80-b4d9-11eb-83fb-509486069f89.png)
>
> `sudo apt install tightvncserver`


### 1.3.4 VNC Server starten

> ![image](https://user-images.githubusercontent.com/173962/118293263-c327cb00-b4d9-11eb-83d5-7d7f126e8941.png)
>
> Passwortvergabe für den VNC Service

> ![image](https://user-images.githubusercontent.com/173962/118293930-798bb000-b4da-11eb-8d1f-f358cb2f69c8.png)
>
> Gekürzte Passwörter sind nicht sehr vertrauenserweckend...

> ![image](https://user-images.githubusercontent.com/173962/118294464-0898c800-b4db-11eb-8e9b-2f4ba395b421.png)
>
> Desktop-Umgebung (xfce4) Eintrag

> ![image](https://user-images.githubusercontent.com/173962/118294764-5ad9e900-b4db-11eb-9c0c-3fdab2a211f0.png)
>
> Ausführbar machen des Scripts.

> ![image](https://user-images.githubusercontent.com/173962/118294941-8fe63b80-b4db-11eb-9252-ec59a880dcf8.png)
>
> Neuen Service anlegen

> ![image](https://user-images.githubusercontent.com/173962/118295666-6da0ed80-b4dc-11eb-906e-8c0269d18ee1.png)
>
> Editiertes Service Script

> ![image](https://user-images.githubusercontent.com/173962/118295867-a04ae600-b4dc-11eb-8bc5-7585ef8ed0ab.png)
>
> Regenerieren des Dependy-Trees, VNC Service Autostart aktivieren und starten

> ![image](https://user-images.githubusercontent.com/173962/118296300-1a7b6a80-b4dd-11eb-8098-f27ae0ef6765.png)
>
> Der Service läuft!


### 1.3.5 Erstellen von Security Policies

> ![image](https://user-images.githubusercontent.com/173962/118298315-9bd3fc80-b4df-11eb-83a7-2c804f96840b.png)
>
> Neues VNC Service Objekt auf Port `5901`

> ![image](https://user-images.githubusercontent.com/173962/118298535-dd64a780-b4df-11eb-8a06-f0fe782a0032.png)
>
> NAT für den VNC Service (von CloudGuard auf Linux Instanz, jeweils Port `5901`)

> ![image](https://user-images.githubusercontent.com/173962/118298780-33394f80-b4e0-11eb-9b1c-b7b189eb7ba1.png)
>
> Installieren der Policy

### 1.3.6 Testen der VNC Verbindung

> ![image](https://user-images.githubusercontent.com/173962/118299065-94f9b980-b4e0-11eb-958e-66c9221d173f.png)
>
> Der VNC Verbindungsaufbau funktioniert

> ![image](https://user-images.githubusercontent.com/173962/118299273-d68a6480-b4e0-11eb-882b-f39fb3cfe021.png)
>
> Der VNC Login war erfolgreich

### 1.3.7 Aufgetretene Probleme

* Der automatische Vollbildmodus hatte leiche Grafikfehler
 * gelöst durch `Strg-Alt-Shift-F` um den Modus zu verlassen 
