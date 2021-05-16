# Lab 3

**Author: Benjamin Medicke**<br>
**Topics: Application Control, URL Filtering & HTTPS Inspection Bypass**

[lab1](lab1.md) | [lab2](lab2.md) | **lab3** | [lab4](lab4.md)

---

<!-- vim-markdown-toc GFM -->

* [Lab 3.1 Application Control](#lab-31-application-control)
  * [3.1.1 Aktivieren der Blades: Application Control & URL Filtering](#311-aktivieren-der-blades-application-control--url-filtering)
  * [3.1.3 Vorhandene Policy anpassen](#313-vorhandene-policy-anpassen)
  * [3.1.6 Update](#316-update)
  * [3.1.7 Anlegen einer Application Control Policy](#317-anlegen-einer-application-control-policy)
  * [3.1.9 Policy auf Linux Instanz testen](#319-policy-auf-linux-instanz-testen)
  * [3.1.10 Zugriff auf Google Maps verbieten](#3110-zugriff-auf-google-maps-verbieten)
  * [Aufgetretene Probleme](#aufgetretene-probleme)
* [Lab 3.2 URL Filtering](#lab-32-url-filtering)
  * [3.2.1 Neue Applikation erstellen](#321-neue-applikation-erstellen)
  * [3.2.3 Drop Policy für das Technikum erstellen](#323-drop-policy-für-das-technikum-erstellen)
  * [3.2.4 Testen der Drop Policy](#324-testen-der-drop-policy)
* [Lab 3.3 HTTPS Inspection Bypass](#lab-33-https-inspection-bypass)
  * [Aufgetretene Probleme](#aufgetretene-probleme-1)
  * [3.3.2 Erstellen einer Bypass Rule für das Technikum](#332-erstellen-einer-bypass-rule-für-das-technikum)
  * [3.3.3 Testen des Zugriffs und Analyse des Zertifikates](#333-testen-des-zugriffs-und-analyse-des-zertifikates)
  * [3.3.4 Welche Kategorien von Seiten kommen in einem Unternehmen in Frage?](#334-welche-kategorien-von-seiten-kommen-in-einem-unternehmen-in-frage)
  * [Aufgetretene Probleme](#aufgetretene-probleme-2)

<!-- vim-markdown-toc -->

## Lab 3.1 Application Control

Lab 3.1 beschäftigt sich mit Zugriffskontrollen von vordefinierten Webservices (im konkreten Fall Google Maps).

### 3.1.1 Aktivieren der Blades: Application Control & URL Filtering

Zwei weitere Blades ("Application Control" und "URL Filtering") wurden aktiviert.

>![image](https://user-images.githubusercontent.com/173962/118366373-3c89f100-b5a0-11eb-82c3-75b74dc23f65.png)
>
> Aktivieren der "URL Filtering" und "Application Control" Blades 

### 3.1.3 Vorhandene Policy anpassen

Über den Layer Editor wurde die vorhandene Policy angepasst:

> ![image](https://user-images.githubusercontent.com/173962/118367659-61cb2f00-b5a1-11eb-881f-ffc645d7c729.png)
>
> Editierter Access Control Layer

Die angepasste Version wurde installiert:

>![image](https://user-images.githubusercontent.com/173962/118368168-f03fb080-b5a1-11eb-8334-0af5eb660284.png)
>
> Installieren der Policy

### 3.1.6 Update

Da das Blade zum ersten mal gestartet wurde, wurde ein Update durchgeführt:

>![image](https://user-images.githubusercontent.com/173962/118369547-15352300-b5a4-11eb-9f7e-7d6637d75611.png)
>
> Update Application Control & URL Filtering

### 3.1.7 Anlegen einer Application Control Policy

Ich habe mich für Google Maps entschieden:

> ![image](https://user-images.githubusercontent.com/173962/118370280-47944f80-b5a7-11eb-96cf-0bd10a12ea06.png)
>
> Policy um Google Maps zu verbieten

> ![image](https://user-images.githubusercontent.com/173962/118394373-9e039b80-b644-11eb-99de-5da7a1c9eac8.png)
>
> Google Maps benötigt HTTPS Inspection.

Ein wichtiger Punkt hier ist, dass diese Policy nur funktioniert, wenn HTTPS Inspektion aktiviert ist. Das ist nicht bei jeder Applikation so (Google Calendar oder YouTube kann zum Beispiel auch ohne diese Funktion geblockt werden),

### 3.1.9 Policy auf Linux Instanz testen

Vor Installation der Policy wurde die Seite getestet:

> ![image](https://user-images.githubusercontent.com/173962/118370452-0e101400-b5a8-11eb-946c-db46b28f9084.png)
>
> Vor Installation der Policy geht Google Maps einwandfrei

> ![image](https://user-images.githubusercontent.com/173962/118370610-a4443a00-b5a8-11eb-8b56-2511b5fe2d4b.png)
>
> Nach Installation wird die Seite geblockt (bei aktivierter HTTPS Inspektion)

<!-- Erfahrungen? -->

### 3.1.10 Zugriff auf Google Maps verbieten

> ![image](https://user-images.githubusercontent.com/173962/118372496-2f75fd80-b5b2-11eb-9b55-9b59ea701948.png)
>
> **Nach Deaktivieren der HTTPS Inspektion ist die Seite (über HTTPS) wieder erreichbar.
> Dies ist der Fall, weil die Subdomain der Firewall gegenüber nicht offen gelegt wird.**

### Aufgetretene Probleme

Es sind keine Probleme aufgetreten.

## Lab 3.2 URL Filtering

Das Ziel dieses Labs war es eine Custum-URL zu blocken. In diesem Fall war das die Seite des Technikum Wiens.

> ![image](https://user-images.githubusercontent.com/173962/118373003-b5934380-b5b4-11eb-9590-f45f2c309c5d.png)
>
> Neues Application/Site Objekt

### 3.2.1 Neue Applikation erstellen

Vor Installation der Policy wurde die Seite wieder getestet.

> ![image](https://user-images.githubusercontent.com/173962/118373109-51bd4a80-b5b5-11eb-8781-ff0dc3d4bfcd.png)
>
> Zugriff ist noch möglich

### 3.2.3 Drop Policy für das Technikum erstellen

> ![image](https://user-images.githubusercontent.com/173962/118393110-942a6a00-b63d-11eb-93fe-91b653113cd5.png)
>
> Drop Policy: Technikum

> ![image](https://user-images.githubusercontent.com/173962/118373190-cdb79280-b5b5-11eb-914b-c9deacdd274a.png)
>
> Nach Installation: Die Policy funktioniert

### 3.2.4 Testen der Drop Policy

Auch diese Policy funktioniert.

> ![image](https://user-images.githubusercontent.com/173962/118373237-0a838980-b5b6-11eb-9ce3-cf82bfba1ce9.png)
>
> Detailansicht des Blockeintrages

*Welche URL Kategorien von Seiten würden Sie blockieren?*

Persönlich würde ich nur Webseiten blocken, die eine sicherheitstechnische Gefahr darstellen. Aus Produktivitätsgründen kann es je nach Unternehmen gewünscht sein zusätzlich die folgenden Kategorien zu blocken:

* anstößliche Inhalte (Wettseiten, Pornographie)
* Social Media
* Spiele Seiten
* Musik/Video Streaming Seiten
* etc.

Wobei das produktivitätstechnisch vermutlich keinen positiven Einfluss hat. Geblockte Seiten haben negative Auswirkungen auf die Motivation und Moral der Mitarbeiter. Facebook wird sonst einfach am Handy geöffnet. Im Schlimmsten Fall führt es sogar zu einer Schatten-IT.

### Aufgetretene Probleme

Es sind keine Probleme aufgetreten.

## Lab 3.3 HTTPS Inspection Bypass

Dieses Lab behandelt das gezielte ignorieren von Seiten im Bezug auf HTTPS Inspection. Das kann vor allem zur Wahrung der Privatsphäre von Usern praktisch sein.

> ![image](https://user-images.githubusercontent.com/173962/118374045-46b8e900-b5ba-11eb-8311-733591449fdd.png)
>
> Vor Bypass Regel. Man sieht der Issuer ist Google.com (was ich als Wert im self-signed Certificate eingestellt habe)

### 3.3.2 Erstellen einer Bypass Rule für das Technikum

Das Original-Zertifikat nach installieren der Bypass Rule, der HTTPS Traffic wird also nicht aufgebrochen:

> ![image](https://user-images.githubusercontent.com/173962/118374177-f726ed00-b5ba-11eb-9cb1-2308ee995374.png)
>
> Nach Bypass wird das Original Zertifikat verwendet. Vergleiche "Issued By" mit vorherigem Screenshot.

### 3.3.3 Testen des Zugriffs und Analyse des Zertifikates

Siehe die zwei vorherigen Screenshots für die Auswirkungen auf das verwendete Zertifikat.

> ![image](https://user-images.githubusercontent.com/173962/118374319-b24f8600-b5bb-11eb-8e73-ec53c432ed75.png)
>
> HTTPS Inspection Bypass für die Technikum Seite funktioniert

>![image](https://user-images.githubusercontent.com/173962/118394784-110e1180-b647-11eb-8ee4-328a0751c63b.png)
>
> Inspiziert vs. gebypassed

### 3.3.4 Welche Kategorien von Seiten kommen in einem Unternehmen in Frage?

<!-- Privacy concerns! -->

*Welche Seiten oder Kategorien von Seiten würden Sie in der HTTPS Inspection ausnehmen, daher bypassen?*

Jegliche Seiten, die private Daten übermitteln:
* private Kommunikation
* Regierungsseiten
* Medizienische Seiten
* Finanzseiten

### Aufgetretene Probleme

Es sind (glücklicherweise ein weiteres Mal) keine Probleme aufgetreten.

[nächstes Lab](lab4.md)
