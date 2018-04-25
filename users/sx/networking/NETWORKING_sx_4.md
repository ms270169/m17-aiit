# Netzwerke und Internet (4)

## Schritt 3: Request und Response

Nachdem die TCP/IP Verbindung aufgebaut ist, sendet der Client von seinem Socket eine HTTP Anfrage an den Server-Socket, und erwartet zeitnah eine Antwort (Response) vom Server.

### Request (Anfrage)

Der HTTP-Request selbst ist eine Textnachricht, die am Ende mit einer leeren Zeile abgeschlossen ist. Die Textnachricht besteht aus dem HTTP-Kommando *GET* und dem Request-Header (alle Zeilen unter GET).

Der Header besteht aus Attributen, zum Beispiel dem Attribut *Connection* hat den Wert *keep-alive*, das dem Server mitteilt, er möge die Netzwerverbindung nach der Beantwortung geöffnet lassen.

```
GET /1ahme/text HTTP/1.1
host: htl-mechatronik.at
Connection: keep-alive
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) ppleWebKit/537.36 (KHTML, like Gecko) Ubuntu Chromium/64.0.3282.167 Chrome/64.0.3282.167 afari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: de-DE,de;q=0.9,en-US;q=0.8,en;q=0.7

```
Dieser ASCII codierte Text (467 Zeichen) wird über das Netzwerk an den Server-Socket `htl-mechatronik.at:80` (das Web-Server Programm am Server-Host) gesendet.

-------------------------------------

### Response (Antwort)

Der Server empfängt den Request und bearbeitet ihn. Er sucht die gewünschte Resource `/1ahme/text` und sendet die Antwort in Form einer Textnachricht wieder zurück.

```
HTTP/1.1 200 OK
Date: Mon, 23 Apr 2018 04:30:13 GMT
Server: Apache/2.4.7 (Ubuntu)
Last-Modified: Mon, 23 Apr 2018 04:29:18 GMT
ETag: "fa0-56a7c7b2d43f3"
Accept-Ranges: bytes
Content-Length: 4000
Keep-Alive: timeout=10, max=100
Connection: Keep-Alive

Lorem ipsum ... est. Pha
```

Auch hier wird dem gleichen Prinzip wie beim Request gefolgt. Zu Beginn eine Zeile die angibt, ob der Request erfolgreich bearbeitet werden konnte. Der HTTP Status-Code 200 steht für einer erfolgreiche Bearbeitung. Danach kommt der Response-Header, gefolgt von einer Leerzeile. Im Header gibt es das Attribut `Content-Length` mit dem Wert 4000. Es besagt, dass nach dem Header der **Body** mit 4000 Zeichen folgt. Danach ist die Response zu Ende. Die letzte Zeile mit `...` symbolisiert die 4000 Zeichen der angeforderten Resource, also den angeforderten Text.

-------------------------------------

### Das HTTP Protokoll

Das **Hypertext Transfer Protocol** (HTTP) ist ein zustandsloses Protokoll, dass heisst, Anfragen werden unabhängig von Anfragen der Vergangenheit beantwortet.

Die "Kommunikationseinheiten" werden als **Nachricht** (*message*) bezeichnet. Es gibt zwei Arten von Nachrichten, **Anfragen** (*request*) und **Antworten** (*response*) .

Jede Nachricht besteht aus zwei Teilen, dem **Nachrichtenkopf** (***header***) und dem **Nachrichtenrumpf** (***body***). Der body enthält die Nutzdaten und kann auch gänzlich fehlen wenn keine Nutzdaten transportiert werden sollen.

In der Anfrage ist die Anfragemethode enthalten. Die wichtigsten Methoden sind:

* **GET**  
  Die gewünschte Resource holen.
* **POST**  
  Die mitgesendeten Daten verarbeiten, zB für die Daten eine neue Resource am Server anlegen.
* **HEAD**  
  Nur den Header der gewünschten Resource holen.
* **PUT**  
  Eine Resource am Server neu anlegen oder bereits existierende Daten aktualisieren.
* **DELETE**  
  Die Resource am Server löschen.

Jede Anfrage wird in der Response mit einem HTTP Statuscode beantwortet. Die erste Ziffer kennzeichnet den Typ:

* 1xx - Informationen
* 2xx - Erfolgreiche Operation
* 3xx - Umleitung
* 4xx - Client Fehler
* 5xx - Server Fehler

Sehr häufige Status-Codes sind:
* **200 OK**
* 304 Not Modified
* 400 Bad Request
* 401 Unauthorized
* 403 Forbidden
* 404 Not Found
* 500 Internal Server Error

In der Antwort können auch Daten im Body mitgesendet werden, zum Beispiel um bei einem POST dem Client mitteilen zu können mit welcher URL die neu erstellte Resource in Zukunft abgefragt werden kann.

Stellt der Server fest, dass die Resource nur für bestimmte "Anfrager" verfügbar ist, erfolgt die Antwort mit Status-Code 401 (*Unauthorized*). In diesem Fall muss der Client zusätzliche Informationen im Header mitsenden (ID/Password, Cookie, JSON-Webtoken, ...), die eine Authentifizierung erlauben. Fehlen diese Informationen, so kann sich der Client diese Informationen in der Regel über spezielle Login-Seiten beschaffen. Üblicherweise erfolgt eine automatische Weiterleitung zum Login URL.

---------------------------
***Weiterführende Informationen in Wikipedia:***

* [Hypertext Transfer Protocol](https://de.wikipedia.org/wiki/Hypertext_Transfer_Protocol)
* [HTTP-Statuscode](https://de.wikipedia.org/wiki/HTTP-Statuscode)
-------------------------