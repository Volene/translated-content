---
title: CDN
slug: Glossary/CDN
tags:
  - Glossary
  - Infrastructure
translation_of: Glossary/CDN
---
Ein **CDN** (Content Delivery Network) ist eine Gruppe von Servern, die sich über viele Standorte erstreckt. Diese Server speichern duplizierte Kopien von Daten, um Datenanforderungen, basierend darauf welche der Server sich räumlich am nähesten zu den entsprechenden anfragenden Endnutzern befinden, zu beantworten. CDNs ermöglichen schnelle Leistung, die weniger stark von hoher Datenverkehrsauslastung beeinflusst wird.

CDNs werden auf breiter Ebene genutzt um CSS- und Javascript-Dateien (Static Assets, Statische Inhalte) von Bibliotheken wie Bootstrap, jQuery etc. auszuliefern. Derartige Bibliotheksdateien über ein CDN auszuliefern, ist aus mehreren Gründen vorzuziehen:

- Statische Inhalte von Bibliotheken über ein CDN auszuliefern, vermindert die Last auf Deinen eigenen Servern.
- Die meisten CDNs haben Serverstandorte rund um den Erdball, so dass die Server des CDN u.U. näher bei Deinen Nutzern sind, als Deine eigenen Server. Geographische Distanz wirkt sich proportional auf die Latenz aus.
- CDNs sind bereits mit den richtigen Cache-Einstellungen konfiguriert. Die Benutzung eines CDN erspart Dir die Konfiguration für die Bereitstellung von statischen Inhalten auf Deinen eigenen Servern.
