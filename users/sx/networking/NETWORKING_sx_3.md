# Netzwerke und Internet (3)

## 2.Schritt: TCP/IP Verbindung zu einem Zielrechner aufbauen

Sobald die URL im Web-Browser eingegeben wird, baut das Client Programm (der Web-Browser) eine Netzwerkverbindung zum Server (einem anderen Programm) auf. Genau genommen wird das vom Betriebssystem erledigt, und dem Web-Client wird nach dem erfolgreichen Verbindungsaufbau vom Betriebssystem ein Kommunikationsendpunkt, ein sogenannter **Socket**, zur Verfügung gestellt.

### Socket

Sockets werden als Kombination von IP-Adresse und Port angeschrieben. Die beiden Teile werden durch einen Doppelpunkt getrennt.

Beispiel: Web-Server der HTL in Arnfels

* `htl-mechatronik.at:80`
* `188.20.185.182:80`
* `172.16.1.11:80`

Wird in der URL ein Domain-Name verwendet, so wird dieser automatisch vom Betriebssystem über eine DNS-Server Abfrage durch die IP-Adresse ersetzt.

Läuft der Server am eigenen Rechner, so kann in der URL ...  
* als Domain-Name **localhost** 
* oder als IPv4-Adresse **127.0.0.1**
* oder als IPv6 Adresse **::1**

... eingegeben werden.


---------------------------
***Weiterführende Informationen in Wikipedia:***

* [Socket](https://de.wikipedia.org/wiki/Socket_(Software))
* [TCP Verbindungsaufbau](https://de.wikipedia.org/wiki/Transmission_Control_Protocol#Verbindungsaufbau)
-------------------------

### TCP (Transmission Control Protocol)

Ein Web-Browser benötigt für den Datenaustausch mit dem Server einen Stream-Socket zum Server. Beim Datenaustausch kommt das **Transmission Control Protocol** (**TCP**) zum Einsatz. 

Dieses Netzwerkprotokoll sorgt dafür, dass Daten ...

* ... gleichzeitig in beide Richtungen - also **bidirektional** -  übertragen werden können.
* ... **richtig** übertragen werden.  
Bei Übertragungsfehlern werden die Daten automatisch nochmals gesendet.
* ... **vollständig** übertragen werden.  
Gehen Daten verloren, so werden diese automatisch nochmals gesendet.
* ... Datenteile in der **richtigen Reihenfolge** beim Empfänger ankommen.

Liegt der Server-Socket auf einem anderen Rechner, so kommen zusätzliche andere Netzwerkprotokolle zum Einsatz, die Daten zum richtigen Rechner transportieren. Das sind im Normallfall:  
* **Internet Protocol (IP)**
* **Ethernet** und/oder **WLAN**

Da es sich im Normalfall um einen Datenaustausch zwischen Programmen auf unterschiedlichen Rechnern handelt, wird oft von einem Datentransfer über eine **TCP/IP Verbindung** gesprochen.

---------------------------
***Weiterführende Informationen in Wikipedia:***  
*  [Transmission Control Protocol](https://de.wikipedia.org/wiki/Transmission_Control_Protocol#Verbindungsaufbau)
-------------------------

### Port

Der Port ist eine 16 Bit große Zahl und Teil des Socket, der "Netzwerkadresse" eines Programmes. Durch ihn kann das Betriebssystem eintreffende Daten dem richtigen Programm zustellen.

Mit 16 Bit lassen sich Werte von 0 bis 65535 bilden. Diese Werte werden in drei Bereiche unterteilt:
1) **System Ports**  (0 bis 1023)  

    Siehe auch: [Wikipedia - Liste der standardisierten Ports](https://de.wikipedia.org/wiki/Liste_der_standardisierten_Ports)

     Beispiele:  
     Port     | Beschreibung 
     --:     | :--
     22      | SSH (Secure Shell)
     **80**  | HTTP (Hypertext Transfer Protocol) / Web-Server
     **443** | HTTPS (Hypertext Transfer Protocol Secure) / Web-Server verschlüsselt
     995     | POPS (Post Office Protocol Secure)

2) **Registrierte Ports** (1024 bis 49151)  
  Auch diese Ports stehen für Server-Programme zur Verfügung. Wird zum Beispiel ein Web-Server Programm gestartet, und möchte dieses unter Port 80 seinen Dienst anbieten, so benötigt das Programm Admin-Rechte. Möchte es seine Dienste hingegen über Port 8080 anbieten, so benötigt es dafür keine Admin-Rechte.

3) **Dynamische Ports** (49152 bis 65535)  
  Eine Portnummer aus diesem Bereich wird beim Aufbau der Verbindung automatisch dem Client-Programm zugeteilt.

---------------------------
***Weiterführende Informationen in Wikipedia:***  
* [Port (Protokoll)](https://de.wikipedia.org/wiki/Port_(Protokoll))
-------------------------
