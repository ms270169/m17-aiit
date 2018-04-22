# Netzwerke und Internet (2)

## 1.Schritt: Eingabe der URI im Web-Browser

Der Benutzer gibt einen **Uniform Resource Locator** (*URL*) im Browser ein. Dieser beinhaltet im authority-Teil den Domain-Namen oder die IP-Adresse des Rechners, auf dem der Server (ein Programm) läuft.

## 2.Schritt: Auflösung des Domain-Namen (Hostname, Rechnername)

Falls im URI ein Domainname verwendet wurde (zum Beispiel *htl-mechatronik.at*), muss im ersten Schritt die IP-Adresse dieser Domain gefunden werden. Dazu gibt es mehrere Möglichkeiten:

1) Der Name ist in der Datei *hosts* vermerkt  
Windows: *C:/Windows/System32/Drivers/etc/hosts*  
Linux und macOS: */etc/hosts*  

2) Ein **Domain Name System** - Server (**DNS-Server** oder **Nameserver**) wird über das Netzwerk kontaktiert.

Damit ein **Nameserver** überhaupt kontaktiert werden kann, muss dem Betriebssystem dessen IP-Adresse bekannt sein. Diese Adresse kommt in der Regel vom DHCP-Server, der bei der Netzwerkanmeldung auch die IP-Adresse des Rechners vergibt. Die Adresse des DNS-Server kann aber auch fest vergeben werden.

Beispiel: **8.8.8.8** (Google DNS Server) oder **1.1.1.1** (von Cloudfare)

Den Google DNS Server sollte man aber nur zu Testzwecken und nicht im regulären Betrieb verwenden, da Google sonst das komplette Surfprofil bequem aufzeichnen kann. Meist wird der DNS-Server des Internet Provider verwendet. Systeme wie Ubuntu betreiben im eigenen System einen DNS-Server. Anfragen die selbst nicht beantwortet (aufgelöst) werden können, werden an den vom DHCP Server genannten DNS-Server weitergereicht.

Da der Nameserver für die Funktion des Netzwerks eine zentrale Bedeutung hat, können im Betriebssystem mehrere Nameserver eingetragen werden (*Primary DNS*, *Secondary DNS*, ...).

Weiterführende Informationen in Wikipedia:  
* [Domain Name System](https://de.wikipedia.org/wiki/Domain_Name_System)
* [Domain-Namesraum](https://de.wikipedia.org/wiki/Domain_Name_System#Domain-Namensraum)

## TCP/IP, IP-Adressen

Die meisten Netzwerke (so auch das Internet) verwenden heute die Protokolle **TCP** (*Transmission Control Protocol*) und **IP** (*Internet Protocol*) als Basistechnologie. Man spricht dann von einem **TCP/IP-Netzwerk**.

In einem solchen Netzwerk ist jeder Rechner (Host) über seine IP-Adresse eindeutig erreichbar.

Zwei Arten von IP-Adressen sind heute in Verwendung:

1) **IPv4-Adresse (IP Version 4)**  
Diese ist 32 Bit lang, und wird mit 4 Zahlen dezimalen Zahlen im Bereich 0 bis 255 angeschrieben. Zwischen den Dezimalzahlen wird ein Punkt gesetzt.  
Beispiel: IP-Adresse der HTL in Arnfels  
**`188.20.185.182`** = Binär `10111100 00010100 10111001 10110110`

2) **IPv6-Adresse (IP Version 6)**  
Diese ist 128 Bit lang, und wird mit acht vierziffrigen Hex-Zahlen (0000 bis FFFF) angeschrieben. Zwischen den Hexzahlen wird ein Doppelpunkt gesetzt.  
Beispiel:  
**`fe80:0000:0000:0000:020f:feff:fe94:0040`** = Binär `11111110 10000000 00000000 ... `  
Um die Länge der Adresse auch kürzer schreiben zu können, dürfen führende 0er weggelassen werden. Weiters darf **einmal (!)** ein 0er-Block durch zwei Doppelpunkte ersetzt werden. Das obere Beispiel kann daher auch so angeschriebenw werden:  
**`fe80::20f:feff:fe94:40`**

Derzeit werden im asiatischen Raum (China) fast ausschließlich IPv6-Adressen verwendet, während in Europa und den USA meist IPv4-Adressen verwendet werden. Vermutlich wird das noch 10 bis 20 Jahre so bleiben.

Vergeben werden IP-Adressen von der **Internet Assigned Numbers Authority** (**IANA**). Diese vergibt Adresspakete an untergeordnete Organisationen, die ihrerseits Pakete wieder an die einzelenen Internet-Provider vergeben. Über ihren Internet-Provider können dann private Personen oder Organisationen IP-Adressen bekommen. Diese sind in der Regel kostenpflichtig.

Siehe auch: [https://www.iana.org/numbers](https://www.iana.org/numbers)

Weiterführende Informationen in Wikipedia:  
* [https://de.wikipedia.org/wiki/IP-Adresse](https://de.wikipedia.org/wiki/IP-Adresse)

## IPv4 Adressen im IPv6 Netzwerk

Um die Umstellung von klassischen IPv4 Netzen zu IPv6 Netzen zu erleichtern, können IPv4-Adressen auch als IPv6-Adresse gebildet werden.

Es stehen vier Varianten zur Verfügung:

 Typ | IPv4 | IPv6 | Kurzschreibweise
  :-- | :-- | :-- | :--
 compatible  | `188.20.185.182` | `0:0:0:0:0:0:BC78:B9B6`
 mapped | `188.20.185.182` | `0:0:0:0:0:FFFF:BC78:B9B6` | `::ffff:188.20.185.182`
 translated | `188.20.185.182` | `0:0:0:0:FFFF:0:BC78:B9B6` | `::ffff:0:188.20.185.182`
 6to4 | `188.20.185.182` | `2002:BC78:B9B6::` 

Weiterführende Informationen in Wikipedia:
* [6to4](https://en.wikipedia.org/wiki/6to4)


## Private IP-Adressen

Damit im internen Heim- und Firmenbereich TCP/IP Netze errichtet werden können, sind bestimmte Adressbereiche als **private Adressen** definiert. Diese werden im öffentlichen Netz (Internet) nicht verwendet.

* **IPv4**: 

   Erste Adresse | Letzte Adresse | CIDR-Notation | Anzahl
   :----------- | :------------ | :----------- | -----: 
    `192.168.0.0` | `192.168.255.255` | `192.168.0.0/16` |     65.536
    `172.16.0.0`  | `172.31.255.255`  | `172.16.0.0./12` |  1.048.576
    `10.0.0.0`    | `10.255.255.255`  | `10.0.0.0./8`    | 16.777.216

* **IPv6**  
Alle Adressen die mit `fd00` beginnen.

Weiterführende Informationen in Wikipedia:
* [Private IP-Adresse](https://de.wikipedia.org/wiki/Private_IP-Adresse)

## CIDR, Netzwerk- und Geräteteil

Eine IP-Adresse besteht eigentlich aus zwei Teilen, einem Netzwerk- und Geräteteil. Zu Beginn des Internets wurde mit Hilfe von Netzklassen diese Unterscheidung getroffen. Seit 1993 wird das **Classless Inter-Domain Routing** (**CIDR**) Verfahren verwendet.

Bei diesem Verfahren wird die binäre IP-Adresse mit Hilfe einer Netzmaske (nur IPv4) oder Präfixlänge (IPv4 und IPv6) in die beiden Teile Netzwerk- und Geräteteil unterteilt.

Beispiel: IPv4-Adresse der HTL in Arnfels

Bezeichnung | Wert
 :-- | :--
IPv4 Adresse         | **`188.20.185.182`**
IPv4 (hexadezimal)   | `BC 14 B9 B6`
Mit Netzmaske        | `188.20.185.182/255.255.255.252`
Mit Präfixlänge      | `188.20.185.182/30`
Netzmaske (binär)    | `1111 1111   1111 1111   1111 1111   1111 1100`
IPv4 (binär)         | `1011 1100   0001 0100   1011 1001   1011 0110`
Netzwerkteil (binär) | `1011 1100   0001 0100   1011 1001   1011 01  `
Geräteteil (binär)   | `                                           10`

Weiterführende Informationen in Wikipedia:
* [IPv4 Netzwerkteil und Geräteteil](https://de.wikipedia.org/wiki/IP-Adresse#Netzwerkteil_und_Ger%C3%A4teteil)
* [Classless Inter-Domain Routing](https://de.wikipedia.org/wiki/Classless_Inter-Domain_Routing)
