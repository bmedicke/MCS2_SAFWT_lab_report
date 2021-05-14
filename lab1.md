## Lab 1

<!-- vim-markdown-toc GFM -->

* [Lab 1.1 Connecting to Management](#lab-11-connecting-to-management)
* [Lab 1.2 SSH Connection to Linux Instance](#lab-12-ssh-connection-to-linux-instance)
* [Lab 1.3 VNCServer & NAT Rules](#lab-13-vncserver--nat-rules)

<!-- vim-markdown-toc -->

### Lab 1.1 Connecting to Management

Der Fingerprint des Servers, der bei der ersten Verbindung angezeigt wird ist:

`REAR NECK KICK TIP HOE DUET DALE GASH ECHO OW SHED TONE`

Er stimmt mit dem im Gaia Web Interface überein.

> ![002](https://user-images.githubusercontent.com/173962/116440505-dfc4d180-a850-11eb-9774-08411186ece4.PNG)
>
> Fingerprint im Gaia Web Interface

---

_Beantworten Sie die Frage: Welche Aufgaben hat der Fingerprint und welche Bedrohungen werden damit verhindert?_

Der Fingerprint garantiert die Authentizität des Servers. Falls der Server 'ausgetauscht' wird, können Man-In-The-Middle Angriffe erkannt werden.

### Lab 1.2 SSH Connection to Linux Instance

#### 1.2.1

Anlegen eines neuen Netzwerkobjektes (Subnetz 192.168.20.0/24), welches mit NAT hinter der Firewall versteckt wird.

> ![image](https://user-images.githubusercontent.com/173962/116457764-19530800-a864-11eb-8acc-00c64e2c3783.png)
>
> Neues Netzwerkobjekt, Reiter: General

> ![image](https://user-images.githubusercontent.com/173962/116457797-24a63380-a864-11eb-8b16-17e8f28af12e.png)
>
> Neues Netzwerkobjekt, Reiter: NAT

Ebenso wurde ein Host-Objekt angelegt, welches die Linux Instanz (IP: `192.168.20.50`) abbildet.

> ![image](https://user-images.githubusercontent.com/173962/118277689-54427600-b4c9-11eb-821a-b2399cdb10d4.png)
>
> Neues Netzwerkobjekt: Linux Instance

#### 1.2.2

Anlegen neuer Policies um SSH Zugriff auf Linux Instanz zu ermöglichen. Beachte: Auf Port 22 läuft bereits der SSH Server der CloudGuard Instanz. Die folgenden Regeln wurden erstellt:

1. eine Firewallregel, die Port 2222 (für SSH) auf die CloudGuard Instanz erlaubt
2. eine NAT-Regel, die Port 2222 der CloudGuard Instanz auf 22 der Linux Instanz mappt 

> ![image](https://user-images.githubusercontent.com/173962/116458672-320fed80-a865-11eb-8964-93ca2058e15d.png)
>
> Neues TCP-Service-Object: SSH-access

> ![image](https://user-images.githubusercontent.com/173962/116462870-460a1e00-a86a-11eb-91e4-4a898ec0e51f.png)
>
> Firewallregel, die Port 2222 erlaubt.

> ![image](https://user-images.githubusercontent.com/173962/116461224-4bfeff80-a868-11eb-8dbc-87ca3f20934a.png)
> 
> NAT Regel.

#### 1.2.3

Hier werden zwei weitere Regeln erstellt:

1. Erlauben von Management-Traffic
2. Stealth Regel (restlichen Traffic droppen)

> ![image](https://user-images.githubusercontent.com/173962/118280320-6376f300-b4cc-11eb-98d2-ae16f2c2e0ae.png)
> 
> Neue Management und Stealth Regeln

#### 1.2.4

Jetzt wurde Logging für alle Regeln aktiviert (siehe vorherigen Screenshot).

![image](https://user-images.githubusercontent.com/173962/116460772-b82d3380-a867-11eb-914c-251b079ddaf4.png)

![image](https://user-images.githubusercontent.com/173962/116462086-5a99e680-a869-11eb-8c1e-d9d56f243200.png)

![image](https://user-images.githubusercontent.com/173962/116464247-08a69000-a86c-11eb-883b-5481d05206fc.png)

### Lab 1.3 VNCServer & NAT Rules
