---
title: '502'
slug: Web/HTTP/Status/502
tags:
  - '502'
  - Glossar
  - HTTP Fehler
  - HTTP Fehlercodes
  - Infrastruktur
  - Navigation
translation_of: Glossary/502
original_slug: Glossary/502
---
502 ist ein {{Glossary("HTTP")}}-Fehlercode, der "Bad Gateway", _fehlerhaftes Gateway_, bedeutet.

Ein {{Glossary("Server")}} kann als Gateway oder Proxy (Vermittler) zwischen einem Client (wie Ihrem Web-Browser) und einem Upstreamserver fungieren. Wenn Sie eine {{Glossary("URL")}} aufrufen, kann der Gateway-Server Ihre Anfrage an den Upstreamserver weiterleiten. "502" bedeutet, dass der Upstreamserver eine ungültige Antwort ausgegeben hat.

Normalerweise ist der Upstreamserver funktionstüchtig (d.h. er übermittelt keine Antwort an das Gateway/der Proxy), verwendet aber nicht das gleiche Protokoll wie das Gateway/der Proxy. Internetprotokolle sind ({{Glossary("Protocol", "protocols")}}) recht genau, deshalb bedeutet 502 häufig, dass einer oder beide Geräte falsch oder unvollständig programmiert worden.

## Erfahren Sie mehr

- [Liste der HTTP-Antwortcodes](/de/docs/Web/HTTP/Response_codes)
