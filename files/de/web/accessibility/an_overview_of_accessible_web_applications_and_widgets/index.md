---
title: Übersicht zu barrierefreien Web-Applikationen und Komponenten
slug: Web/Accessibility/An_overview_of_accessible_web_applications_and_widgets
tags:
  - ARIA
  - Accessibility
  - Guide
  - Handbuch
  - Komponente
  - Web apps
translation_of: Web/Accessibility/An_overview_of_accessible_web_applications_and_widgets
original_slug: Web/Barrierefreiheit/An_overview_of_accessible_web_applications_and_widgets
---
Das Web entwickelt sich weiter: Statische seitenbasierte Websites werden zunehmend durch dynamische, desktopartige Web-Applikationen ersetzt, die mit JavaScript und AJAX arbeiten. Designer erstellen allein durch die Kombination von JavaScript, HTML und CSS beeindruckende neue Benutzeroberflächen und Steuerungsmechanismen. Dieser Wandel hat das Potential, durch responsives Design die Benutzerfreundlichkeit enorm zu verbessern, doch besteht für viele Benutzer die Gefahr wegen Zugänglichkeitsbarrieren ausgeschlossen zu werden. JavaScript hat keinen sehr guten Ruf, was die Barrierefreiheit anbelangt, da JavaScript-Techniken oft Probleme in Kombination mit Unterstützungstechnologie wie z.B. Screenreadern verursachen. Es gibt jedoch andere Möglichkeiten, dynamische Oberflächen zu erstellen, damit diese auch für Menschen mit Behinderungen ohne Einschränkungen benutzbar sind.

## Das Problem

Die meisten JavaScript-Toolkits stellen eine Bibliothek für clientseitige Komponenten bereit, welche den Benutzeroberflächen von bekannten Desktopumgebungen nachempfunden sind. Slider, Menüleisten, Dateisystem-Bäume usw. lassen sich mit einer Kombination von JavaScript, CSS und HTML erstellen. In der HTML4-Spezifikation werden keine Tags festgelegt, welche diese Komponenten semantisch beschreiben und Entwickler greifen daher üblicherweise auf Tags wie \<div> und \<span> zurück. Die so entwickelten Oberflächen sehen Desktop-Applikation sehr ähnlich, enthalten jedoch in der Regel nicht genügend semantische Informationen, um die korrekte Funktion unterstützender Technologie zu gewährleisten. So können dynamische Inhalte einer Webseite von Benutzern, die z.B. eine Website (aus welchen Gründen auch immer) nicht sehen können, nicht vollständlig erfasst werden. Börsenticker, Updates von Twitter-Feeds, Fortschrittsanzeigen und ähnliche Komponenten manipulieren das DOM auf eine Weise, die von Unterstützungstechnologie nicht erkannt werden kann. An dieser Stelle kommt [ARIA](/en/ARIA "ARIA") zum Einsatz.

_Beispiel 1: Markup für eine Tabs-Komponente mit ARIA-Labeln. Im Markup sind keine Informationen enthalten, welche die Form und Funktion der Komponente beschreiben._

```html
<!-- Dies ist eine Komponente für Tabs. Wie könnten Sie das wissen, würden sie nur das Markup betrachten? -->
<ol>
  <li id="ch1Tab">
    <a href="#ch1Panel">Chapter 1</a>
  </li>
  <li id="ch2Tab">
    <a href="#ch2Panel">Chapter 2</a>
  </li>
  <li id="quizTab">
    <a href="#quizPanel">Quiz</a>
  </li>
</ol>

<div>
  <div id="ch1Panel">Chapter 1 content goes here</div>
  <div id="ch2Panel">Chapter 2 content goes here</div>
  <div id="quizPanel">Quiz content goes here</div>
</div>
```

_Beispiel 2: Die Tabs-Komponente könnte z.B. wie folgt aussehen. Bei der visuellen Betrachtung lässt sich dies erkennen, es gibt jedoch keine maschinenlesbare Beschreibungen für Unterstützungstechnologie._
![Screenshot of the tabs widget](/@api/deki/files/4926/=Tabs_Widget.png)

## ARIA

[WAI-ARIA](http://www.w3.org/WAI/intro/aria.php), die Spezifikation für **Accessible Rich Internet Applications** der [Web Accessibility Initiative](http://www.w3.org/WAI/) des W3C beschreibt, wie fehlende semantischen Informationen hinzugefügt werden können, die für das Erfassen der Inhalte bei der Benutzung von Unterstützungstechnologie, wie z.B. Screen Readern, benötigt werden. ARIA ermöglicht Entwicklern, ihre Komponenten genauer zu beschreiben, indem dem Markup spezielle Attribute hinzugefügt werden. ARIA wurde entwickelt, um die Lücke zwischen Standard-HTML-Tags und desktopartigen Komponenten von dynamischen Web-Applikationen zu schließen und legt Rollen- und Zustansbeschreibungen für verbreitete UI-Komponenten fest.

Die ARIA-Spezifikation beschreibt drei verschiedene Arten von Attributen: Rollen, Zustände und Eigenschaften. Rollen werden Komponenten zugewiesen, die bei HTML4 nicht vorhanden sind, wie z.B. Slider, Menüleisten, Tabs und Dialoge. Eigenschaften beschreiben Charakteristiken dieser Komponenten, wie z.B. ob sie per Drag & Drop ziehbar sind, ein benötigtes Element besitzen oder ein Popup mit ihnen verbunden ist. Zustände beschreiben den aktuellen Interaktionsstatus eines Elements - so wird der Unterstützungstechnologie mitgeteilt, ob das Element gerade beschäftigt, deaktiviert, selektiert oder versteckt ist.

ARIA-Attribute sind dafür geschaffen, automatisch vom Browser interpretiert und für die nativen Barrierefreiheit-APIs des jeweiligen Betriebssystems übersetzt zu werden. Wenn ARIA vorhanden ist, kann die Unterstützungstechnologie JavaScript-Komponenten erkennen und mit diesen interagieren, auf dieselbe Weise wie bei Desktop-Software. Hierdurch kann eine konsistentere Benutzerführung ermöglicht werden, als noch bei älteren Generationen von Web-Applkationen, da Benutzer von Unterstützungstechnologie auch bei webbasierten Applikationen auf ihre Kenntnisse über Desktop-Software zurückgreifen können.

_Beispiel 3: Markup für die Tabs-Komponente mit hinzugefügten ARIA-Attributen._

```html
<!-- Durch die zugeteilte Rolle sind die Tabs erkennbar! -->
<!-- role-Attribute wurden der Liste und den einzelnen Elementen hinzugefügt. -->
<ol role="tablist">
  <li id="ch1Tab" role="tab">
    <a href="#ch1Panel">Chapter 1</a>
  </li>
  <li id="ch2Tab" role="tab">
    <a href="#ch2Panel">Chapter 2</a>
  </li>
  <li id="quizTab" role="tab">
    <a href="#quizPanel">Quiz</a>
  </li>
</ol>

<div>
  <!-- Beachten Sie die Attribute 'role' und 'aria-labelledby', welche die Tab-Panels beschreiben. -->
  <div id="ch1Panel" role=”tabpanel” aria-labelledby="ch1Tab">Chapter 1 content goes here</div>
  <div id="ch2Panel" role=”tabpanel” aria-labelledby="ch2Tab">Chapter 2 content goes here</div>
  <div id="quizPanel" role=”tabpanel” aria-labelledby="quizTab">Quiz content goes here</div>
</div>
```

ARIA wird von allen aktuellen Versionen der bekannten Browser unterstützt, einschließlich Firefox, Safari, Opera, Chrome und Internet Explorer. Viele Unterstützungstechnologien, wie z.B. die Open-Source-Screenreader NVDA und Orca, unterstützen ARIA ebenfalls. Auch JavaScript-Biblitheken wie jQuery UI, YUI, Google Closure und Dojo Dijit setzen ARIA-Markup ein.

### Darstellungänderungen

Dynamische Änderungen der Darstellung sind zum Beispiel die Veränderung der Elementeigenschaften mit CSS (wie z.B. ein roter Rand um ein Feld, das fehlerhafte Daten enthält oder eine Farbänderung bei einer aktivierten Checkbox) oder das Anzeigen und Verstecken von Inhalten.

#### Zustandsänderungen

ARIA stellt Attribute zur Deklaration des aktuellen Zustands von Komponenten bereit. Die Beispiele in dieser Einführung werden die folgenden Attribute verwendet (es gibt allerdings noch einige mehr):

- **`aria-checked`**: Zeigt den Zustand einer Checkbox (Auswahlkästchen) oder eines Radiobuttons (Optionsfeld) an.
- **`aria-disabled`**: Zeigt an, dass ein Element zwar sichtbar, jedoch nicht editierbar ist oder anderweitig betätigt werden kann.
- **`aria-grabbed`**: Zeigt an, ob sich ein Objekt bei einer Drag & Drop-Interaktion im "grabbed"-Zustand befindet.

(Eine komplette Liste aller Zustände finden Sie in der [Liste zu ARIA-Zuständen und Eigenschaften](http://www.w3.org/TR/wai-aria/states_and_properties))

Entwickler sollten ARIA-Zustände einsetzen, um den Zustand von Komponenten zu deklarieren und mit CSS-Attribut-Selektoren die visuelle Darstellung je nach Zustand entsprechend verändern (anstatt per Skript den Klassennamen des Elements zu ändern).

Die Website der Open Ajax Alliance stellt Beispiel zu CSS-Attributseletoren in Verbindung mit ARIA bereit. Das Beispiel zeigt die Oberfläche eines WYSIWYG-Editors mit einem dynamischen Menü-System. Elemente, die gerade selektiert sind, unterscheiden sich visuell von anderen Elementen. Relevant sind hier besonders die unten beschriebenen Teile.

Bei diesem Beispiel wird für des Menüs der HTML-Code aus Beispiel 1a verwendet. In Zeile 7 und 13 wird die Eigenschaft aria-checked eingesetzt, um den Zustand der Selektion anzuzeigen.

    <ul id="fontMenu" class="menu" role="menu" aria-hidden="true">
      <li id="sans-serif"
          class="menu-item"
          role="menuitemradio"
          tabindex="-1"
          aria-controls="st1"
          aria-checked="true">Sans-serif</li>
      <li id="serif"
          class="menu-item"
          role="menuitemradio"
          tabindex="-1"
          aria-controls="st1"
          aria-checked="false">Serif</li>
      ...

Für die Änderung der visuellen Darstellung des selektierten Elements wird der CSS-Code aus Beispiel 1b verwendet. Beachten Sie, dass keine Klassennamen benutzt werden, einzig der Zustand des aria-checked-Attribute in Zeile 1 entscheidet also über die Darstellung des Elements.

    li[aria-checked="true"] {
      font-weight: bold;
      background-image: url('images/dot.png');
      background-repeat: no-repeat;
      background-position: 5px 10px;
    }

Zur Aktualisierung der Eigenschaft aria-checked wird der JavaScript-Code aus Beispiel 1c verwendet. Auch das Skript ändert nur den Wert der Attribute (Zeile 3 und 8) und es wird kein Klassenname hinzugefügt oder entfernt.

    var processMenuChoice = function(item) {
      // 'check' the selected item
      item.setAttribute('aria-checked', 'true');
      // 'un-check' the other menu items
      var sib = item.parentNode.firstChild;
      for (; sib; sib = sib.nextSibling ) {
        if ( sib.nodeType === 1 && sib !== item ) {
          sib.setAttribute('aria-checked', 'false');
        }
      }
    };

#### Änderung der Sichtbarkeit

Bei Änderungen der Sichtbarkeit von Elementen (verstecken oder sichtbar machen von Elementen) sollten Entwickler nur den Wert der Eigenschaft **aria-hidden** verändern. Dabei sollte die oben beschreibene Technik angewendet und CSS (`display:none`) eingesetzt werden, um das Element zu verstecken.

Auf der Website der Open Ajax Alliance findet man hierzu ein Beispiel mit einem Tooltip bei dem das Attribut **aria-hidden** eingesetzt wird, um die Sichtbarkeit des Tooltips zu verändern. Das Beispiel zeigt ein einfaches Formular, bei dem Anweisungen zu den einzelnen Feldern eingeblendet werden. Auf die wichtigsten Details wird im Folgenden genauer eingegangen.

Beispiel 2a zeigt den HTML-Code für einen Tooltip. In Zeile 9 wird der Zustand von **aria-hidden** auf `true` gesetzt.

    <div class="text">
        <label id="tp1-label" for="first">First Name:</label>
        <input type="text" id="first" name="first" size="20"
               aria-labelledby="tp1-label"
               aria-describedby="tp1"
               aria-required="false" />
        <div id="tp1" class="tooltip"
             role="tooltip"
             aria-hidden="true">Your first name is a optional</div>
    </div>

Das Beispiel 2b unten zeigt den CSS-Code für das Markup. Wie schon beim ersten Beispiel wird auch hier kein Klassenname benutzt, sondern nur der Wert der Attribute **aria-hidden** geändert.

    div.tooltip[aria-hidden="true"] {
      display: none;
    }

Beispiel 2c zeigt den JavaScript-Code zur Aktulisierung der Eigenschaft **aria-hidden**. Wieder wird per Skript nur die Attribute **aria-hidden** in Zeile 2 verändert und kein Klassenname hinzugefügt oder entfernt.

    var showTip = function(el) {
      el.setAttribute('aria-hidden', 'false');
    }

### Role changes

> **Note:** In Bearbeitung

Mit ARIA können Entwicklern solchen Elementen, bei denen wichtige semantische Informationen fehlen, eine Rolle zuweisen. Wenn z.B. eine ungeordnete Liste für die Erstellung eines Menüs benutzt wird, sollte dem `ul`-Elemente die Rolle `menubar` zugeteilt werden und jedem untergeordneten `li`-Listenelement die Rolle `menuitem`.

Die **Rolle** eines Elements sollte nicht verändert werden. Stattdessen sollte das bestehende Element entfernt und ein neues Element mit neuer **Rolle** hinzugefügt werden.

Wenn man z.B. eine Texteditor-Komponente mit einem Ansichtsmodus und einem Editiermodus erstellen möchte, dann kommt ein Entwickler vielleicht auf die Idee für das Textfeld ein schreibgeschütztes input-Element einzusetzen, diesem für den Ansichtsmodus die Rolle `button` zuzuweisen und beim Wechsel in den Editiermodus die Rolle und den Schreibschutz zu entfernen (da `input`-Elemente eigene Rollen zugewiesen werden können).

Diese Vorgehensweise ist keine gute Idee. Stattdessen sollte für den Ansichtsmodus ein anderes Element, wie z.B. ein `div`- oder `span`-Element mit der Rolle `button` verwendet werden und für den Editiermodus ein `input`-Textelement.

### Asynchrone Inhaltsänderungen

> **Note:** In Bearbeitung. Siehe auch [Live Regions](/en/ARIA/Live_Regions "Live Regions")

## Tastaturnavigation

Von Entwicklern wird oft wenig darauf geachtet, ob Oberflächenkomponenten auch mit der Tastatur bedienbar sind. Damit die Kompnenten für möglichst viele Benutzer zugänglich sind, sollte für alle Funktionen der Komponenten einer Web-Applikation überprüft werden, ob sie auch ausschließlich mit Tastatur und ohne Maus bedient werden können. Für die praktische Umsetzung sollten die üblichen Konventionen für Desktop-Komponenten befolgt werden, also die Benutzung von Tab-, Enter-, Leertaste und Pfeiltasten ermöglicht werden.

Traditionell ist die Tastaturnavigation im Web auf die Tab-Taste begrenzt. Der Nutzer drückt Tab um jeden Link, Button oder Formular auf der Seite nacheinander zu fukussieren, Shift-Tab um zum letzten Element zu springen. Das ist eine eindimensionale Form der Navigation—vor und zurück, ein Element pro Schritt. Auf sehr umfangreichen Seiten muss ein Nutzer der Tastaturnavigation oft dutzende Male die Tab-Taste drücken, um zu dem gewünschten Bereich zu kommen. Die Implementierung von Navigationskonventionen von Desktop-Programmen im Web hat das Potential die Navigation für viele Nutzer zu beschleunigen.

Hier eine Zusammenfassung wie Tastaturnavigation in einer ARIA-unterstützten Web-Applikation funktionieren sollte:

- Die Tab-Taste fokussiert eine Komponente als ganzes. Beispielsweise sollte das navigieren zu einer Menüleiste dessen erstes Element fokussieren
- Die Pfeiltasten sollten die Navigation innerhalb der Komponente ermöglichen. Zum Beispiel indem man mit dem linken und rechten Pfeil den Fokus auf den vorherigen und nächsten Menüpunkt verschiebt
- Wenn die Komponente nicht innerhalb eines Formulars liegt, sollten die Enter- und Leertaste das Kontrollelement auswählen oder aktivieren
- Innerhalb eines Formulars sollte die Leertaste das Element auswählen oder aktivieren, während die Enter-Taste die Standardfunktion des Formulars aufruft
- Ahme im Zweifelsfall die Desktop Standardfunktionalität dieses Elements nach

In dem Beispiel der Tab-Komponente oben sollte der Nutzer also in der Lage sein mit den Tab- und Shift-Tab Tasten in und aus dem Komponenten-Container (\<ol> in unserem Beispiel) zu navigieren. Sobald der Fokus innerhalb des Containers liegt, sollten die Pfeiltasten dem Nutzer erlauben zwischen den einzelnen Tabs (die \<li> Elemente) zu navigieren. Ab hier variieren die Konventionen je nach Plattform. Unter Windows wird der nächste Tab automatisch aktivieren, wenn der Nutzer die Pfeiltasten drückt. Unter macOS, kann der Nutzer entweder die Enter- oder die Leertaste drücken, um den nächsten Tab zu aktivieren. Ein umfangreiches Tutorial zur Erstellung von [Tastaturnavigation in JavaScript Komponenten](/en/Accessibility/Keyboard-navigable_JavaScript_widgets) beschreibt wie man diese Funktionsweise mit JavaScript implementieren kann.

Für mehr Details zu Koventionen bei desktopartiger Tastaturnavigation gibt es einen umfangreichen [DHTML style guide](http://dev.aol.com/dhtml_style_guide). Dieser stellt einen Überblick darüber bereit, wie Tastaturnavigation in jeder von ARIA unterstützten Komponente funktionieren sollte. Die W3C bietet ebenfalls ein hilfreiches [ARIA Best Practices](http://www.w3.org/WAI/PF/aria-practices/Overview.html) Dokument, das Konventionen für Tastaturnavigation und Shortcuts für eine Vielzahl von Komponenten beinhaltet.

## Weiterführende Links

- [ARIA](/en/ARIA "ARIA")
- [Web applications and ARIA FAQ](/en/Accessibility/Web_applications_and_ARIA_FAQ "Web applications and ARIA FAQ")
- [WAI-ARIA Specification](http://www.w3.org/TR/wai-aria/)
- [WAI-ARIA Best Practices](http://www.w3.org/WAI/PF/aria-practices/Overview.html)
- [DHTML Style Guide](http://dev.aol.com/dhtml_style_guide)
