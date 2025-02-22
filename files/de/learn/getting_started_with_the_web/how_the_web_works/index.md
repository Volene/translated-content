---
title: Wie das Internet funktioniert
slug: Learn/Getting_started_with_the_web/How_the_Web_works
tags:
  - Anfänger
  - Client
  - DNS
  - HTTP
  - IP
  - Infrastruktur
  - Internet
  - Lernen
  - Server
  - TCP
  - Web
translation_of: Learn/Getting_started_with_the_web/How_the_Web_works
original_slug: Learn/Getting_started_with_the_web/Wie_das_Internet_funktioniert
---
{{LearnSidebar}}{{PreviousMenu("Learn/Getting_started_with_the_web/Publishing_your_website", "Learn/Getting_started_with_the_web")}}

_Wie das Internet funktioniert_ gibt eine vereinfachte Übersicht darüber, was passiert, wenn Sie eine Webseite in einem Webbrowser auf Ihrem Computer oder auf Ihrem Smartphone aufrufen.

Dieser Artikel ist sehr theoretisch und ist für den Anfang nicht essentiell um Code für Webseiten zu schreiben, aber nach einiger Zeit werden Sie feststellen, das es von Vorteil ist zu wissen, was im Hintergrund geschieht.

## Client und Server

Computer welche über das Internet verbunden sind werden als Client oder als Server bezeichnet. Dieses Diagramm veranschaulicht, vereinacht, wie diese beiden Computer miteinander interagieren:

![](simple-client-server.png)

- Als Client (engl.: Nutzer oder Kunde) werden die Computer bezeichnet, welche mit dem Internet verbunden sind und typischerweise von einem Benutzer genutzt werden. Zum Beispiel Ihr Computer der via Wi-Fi mit dem Netzwerk verbunden ist, oder ihr Smartphone das über ein mobiles Netzwerk verbunden ist. Auch die Software, welche auf Benutzerseite das Internet veranschaulicht, normalerweise Webbrowser wie Firefox oder Chome, wird als Client bezeichnet.
- Server sind Computer, welche Webseiten, Dateien oder Apps speichern. Wenn ein clientseitiger Computer auf eine Webseite zugreifen möchte, wird eine Kopie dieser Webseite von dem Server heruntergeladen, um dann in dem Browser des Benutzers angezeigt zu werden.

## Die anderen Teile der Werkzeugkiste

Der Client und der Server, wie wir sie oben beschrieben haben sind nicht alles. Es gibt weitere Dinge, die involviert sind, um eine Webseite anzuzeigen und wir werden diese hier erläutern.

Versuchen Sie sich vorzustellen, das Internet wäre eine Straße. An einem Ende der Straße ist der Client, was wie Ihr Haus sein könnte. An dem anderen Ende der Straße ist der Server, der wie ein Einkaufsladen ist, bei dem Sie etwas kaufen möchten.

![](road.jpg)

Auf dem Weg von Ihrem Haus zum Shop müssen Sie an einigen anderen Stellen vorbei und "Hallo" sagen:

- **Ihre Internetverbindung**: Erlaubt Ihnen Daten über das Internet zu senden und zu empfangen. Dies ist wie die eigentliche Straße auf der Sie entlang gehen, um von Ihrem Haus zum Laden zu gelangen.
- **TCP/IP**: Transmission Control Protocol und Internet Protocol sind Kommunikationsprotokolle, welche bestimmen wie Daten über das Internet übertragen werden. Dies ist vergleichbar mit dem Transportvehikel, mit dem Sie zu dem Laden kommen, welches ein Auto oder ein Fahrad oder ein anderes Fahrzeug sein könnte.
- **DNS**: Domain Name Servers sind wie ein Adressbuch für Internetseiten. Wenn Sie nach einer Internetadresse suchen, dann schaut der Browser auf dem DNS nach, um die wirkliche Adresse dieser Webseite zu finden. Der Browser muss herausfinden, auf welchem Server die Webseite liegt, damit er eine HTTP Anfrage an die richtige Stelle senden kann. Dies ist vergleichbar mit dem heraussuchen der Adresse des Geschäftes, in dem Sie einkaufen gehen wollen, damit Sie dieses auch finden.
- **HTTP**: Hypertext Transfer Protocol ist ein Applikations {{Glossary("Protocol" , "protocol")}} welches eine Sprache definiert mit welcher Client und Server miteinander kommunizieren können. Dies ist wie die Sprache, mit der Sie im Laden Ihre Bestellung machen.
- **Zusätzliche Dateien**: Eine Webseite wir aus verschiedenen Dateien zusammengesetzt, ähnlich wie sie aus verschiedenen Teilen aus dem Laden etwas sinnvolles bauen können. Diese Dateien kommen in zwei Haupttypen:

  - **Code Dateien**: Webseiten sind hauptsächlich aus HTML, CSS, und JavaScript, aber es gibt noch weitere Möglichkeiten.
  - **Inhalte**: Dies ist alles andere, was auf einer Webeite zu finden ist, wie Bilder, Musik, Videos, Word-Dokumente oder PDFs.

## Was passiert jetzt also genau?

Wenn Sie eine Internetadresse in Ihren Browser eintippen (wie wenn Sie zu dem Laden gehen):

1.  Der Browser kontaktiert den DNS Server und findet die echte Adresse von derm Server auf dem die Webseite liegt (Sie finden die Adresse des Ladens).
2.  Der Browser sendet eine HTTP-Anfrage an den Server und fragt nach einer Kopie der Webseite für den Client (Sie gehen zu dem Laden und bestellen Ihre Waren). Diese Nachricht und alle anderen Daten, welche zwischen Client und Server gesendet werden, nutzen Ihre Internetverbindung und nutzen TCP/IP für die Übertragung.
3.  Wenn der Server die Anfrage entgegennimmt, sendet dieser an den Client eine "200 OK" Nachricht, welche soviel bedeutet wie "Natürlich können Sie sich die Webseite anschauen! Hier ist sie." Danach sendet der Server die Dateien der Webseite, in kleinen Datenpaketen, an den Browser. (Im Laden bekommen Sie Ihre Waren und bringen diese nach Hause)
4.  Im Browser werden die kleinen Datenpakete zusammengesetzt und zeigt Ihnen die komplette Webseite. (die Waren kommen bei Ihnen daheim an)

## DNS erklärt

Echte Webadressen sind keine schönen, leicht zu merkenden Strings, welche Sie in die Adressleiste Ihres Browsers eingeben, um Ihre Lieblingswebseiten zu finden. Es sind spezielle Nummern, welche so aussehen: 63.245.215.20.

Dies ist eine {{Glossary("IP Address", "IP address")}} und repräsentiert eine einzigartige Adresse im Internet. Diese kann man sich aber nicht so leicht merken. Deswegen wurden Domain Name Server erfunden. Dies sind spezielle Server, welche zu der Adresse die Sie im Browser eintippen(z.B. "mozilla.org"), die richtige (IP) Adresse finden.

Webseiten können direkt über ihre IP Adresse erreicht werden. Versuchen Sie es: Gehen Sie zur Mozilla Webseite, indem sie die folgende IP Adresse in der Adresszeile Ihres Browsers in einem neuen Tab eingeben: `63.245.215.20`

![A domain name is just another form of an IP address](https://mdn.mozillademos.org/files/8405/dns-ip.png)

## Datenpakete erklärt

Vorhin haben wir das Wort "Datenpakete" genutzt, um zu beschreiben in welcher Form die Daten vom Server zum Client gelangen. Was ist damit gemeint? Wenn Daten über das Internet gesendet werden, dann wird es in tausenden von kleinen Stückchen geschickt, damit verschiedene Benutzer einer Webseite, diese zur selbern Zeit herunterladen können. Wenn Webseiten in einem großen Paket gesendet werden würde, dann könnte nur ein Benutzer auf einmal diese herunterladen, was das Internet nicht sehr effizient machen würde.

## Lesen Sie weiter (englisch)

- [How the Internet works](/en-US/Learn/How_the_Internet_works)
- [HTTP — an Application-Level Protocol](https://dev.opera.com/articles/http-basic-introduction/)
- [HTTP: Let’s GET It On!](https://dev.opera.com/articles/http-lets-get-it-on/)
- [HTTP: Response Codes](https://dev.opera.com/articles/http-response-codes/)

## Credit

Street photo: [Street composing](https://www.flickr.com/photos/kdigga/9110990882/in/photolist-cXrKFs-c1j6hQ-mKrPUT-oRTUK4-7jSQQq-eT7daG-cZEZrh-5xT9L6-bUnkip-9jAbvr-5hVkHn-pMfobT-dm8JuZ-gjwYYM-pREaSM-822JRW-5hhMf9-9RVQNn-bnDMSZ-pL2z3y-k7FRM4-pzd8Y7-822upY-8bFN4Y-kedD87-pzaATg-nrF8ft-5anP2x-mpVky9-ceKc9W-dG75mD-pY62sp-gZmXVZ-7vVJL9-h7r9AQ-gagPYh-jvo5aM-J32rC-ibP2zY-a4JBcH-ndxM5Y-iFHsde-dtJ15p-8nYRgp-93uCB1-o6N5Bh-nBPUny-dNJ66P-9XWmVP-efXhxJ), by [Kevin D](https://www.flickr.com/photos/kdigga/).

{{PreviousMenu("Learn/Getting_started_with_the_web/Publishing_your_website", "Learn/Getting_started_with_the_web")}}
