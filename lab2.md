## Lab 2

### Lab 2.1 IPS

#### 2.1.3 Topologien einstellen

> ![image](https://user-images.githubusercontent.com/173962/118303243-83ff7700-b4e5-11eb-9738-a4945f31f45f.png)
>
> Topology von eth0 auf "external" stellen.

> ![image](https://user-images.githubusercontent.com/173962/118303483-cb860300-b4e5-11eb-968e-8d70cd016689.png)
>
> Topology von eth1 auf "internal" stellen.

#### 2.1.4 IPS Blade aktivieren

> ![image](https://user-images.githubusercontent.com/173962/118304190-a5ad2e00-b4e6-11eb-8787-24d5e11f7c53.png)
>
> IPS blade aktiviert

> ![003](https://user-images.githubusercontent.com/173962/116441883-29fa8280-a852-11eb-8233-b5ce5fd76ff8.PNG)
> 
> IPS First Time Activation Einstellung

#### 2.1.6 Protected Scope für die Linux Instanz

> ![image](https://user-images.githubusercontent.com/173962/116443098-87430380-a853-11eb-93a8-dd37cb9475ed.png)
> 
> Linux Instanz

> ![image](https://user-images.githubusercontent.com/173962/116443346-d8eb8e00-a853-11eb-9725-46d41451d307.png)
>
> Protected Scope

#### 2.1.7 Profil "Strict" editieren

> ![image](https://user-images.githubusercontent.com/173962/116444319-e6554800-a854-11eb-95ac-c66604399bbe.png)
> 
> "Strict" Profile

> ![image](https://user-images.githubusercontent.com/173962/118305074-ca55d580-b4e7-11eb-875e-30cb60485282.png)
> 
> Nur IPS Blade aktivieren, alles auf "Prevent"

> ![image](https://user-images.githubusercontent.com/173962/116444786-6380bd00-a855-11eb-9815-dac316e523fa.png)
> 
> Publish & Install

> ![image](https://user-images.githubusercontent.com/173962/116445471-35e84380-a856-11eb-910a-df0847e93d46.png)
> 
> Neues Profil

#### 2.1.9 Update

![image](https://user-images.githubusercontent.com/173962/116446047-dc344900-a856-11eb-9c49-0a6e22d7781e.png)

![image](https://user-images.githubusercontent.com/173962/116446180-fc640800-a856-11eb-9845-fa1426b3747c.png)

Nach 10% abgebrochen (da ging scheinbar nichts weiter). Zuerst das Management Server Update machen.

![image](https://user-images.githubusercontent.com/173962/116447220-076b6800-a858-11eb-94e6-e242ad288cb0.png)

Das hängt auch.

![image](https://user-images.githubusercontent.com/173962/116449247-426e9b00-a85a-11eb-8ec2-7650a48b98ac.png)

![image](https://user-images.githubusercontent.com/173962/116450678-dd1ba980-a85b-11eb-9fb1-561fd58be2e3.png)

#### 2.1.10 Traffic generieren und Logs prüfen

> ![image](https://user-images.githubusercontent.com/173962/118308457-3fc3a500-b4ec-11eb-80bd-f06c9ca7a006.png)
> Start eines Nmap-Script-Scans

> ![image](https://user-images.githubusercontent.com/173962/118308166-ee1b1a80-b4eb-11eb-8192-1467f8783fc0.png)
> 
> Erkannter Nmap-Script-Scan: `sudo nmap -sC google.com`


### Lab 2.2 Anti-Virus

### Lab 2.3 HTTPS Inspection
