---
title: cursor
slug: Web/CSS/cursor
tags:
  - CSS
  - CSS Eigenschaft
  - Cursor
  - NeedsBrowserCompatibility
  - NeedsMobileBrowserCompatibility
  - Referenz
translation_of: Web/CSS/cursor
---
{{CSSRef}}

## Übersicht

Die `cursor` CSS Eigenschaft legt den Cursor fest, der angezeigt wird, wenn sich der Mauszeiger über einem Element befindet.

{{cssinfo}}

## Syntax

```css
/* Schlüsselwortwerte */
cursor: pointer;
cursor: auto;

/* Verwendung von URL und Koordinaten */
cursor:  url(cursor1.png) 4 12, auto;
cursor:  url(cursor2.png) 2 2, pointer;

/* Globale Werte */
cursor: inherit;
cursor: initial;
cursor: unset;
```

## Werte

- \<uri>
  - : Eine durch Kommata getrennte Liste, die auf benutzerdefinierte Bilder verweist, die als Cursor angezeigt werden sollen. Mehr als eine Angabe macht Sinn, um eine Ausweichlösung (Fallback) bei nicht unterstützten Bildformaten in anderen Browsern bereitzustellen. Am Ende der Liste **muss** ein Fallback stehen, welches einen Cursor ohne URL angibt, um einen Mauszeiger anzeigen zu können, wenn kein benutzerdefiniertes Bild geladen werden kann. Siehe auch: [Verwendung von URL Werten für die cursor Eigenschaft](/de/Verwendung_von_URL_Werten_für_die_cursor_Eigenschaft "de/Verwendung_von_URL_Werten_für_die_cursor_Eigenschaft") für weitere Details.
- \<x> \<y> {{ experimental_inline() }}
  - : Optionale Angabe von X- und Y-Koordinaten (vom Internet Explorer nicht unterstützt). Angegeben werden zwei Zahlen ohne Einheit.
- Schlüsselwortwerte
  - : **Bewege die Maus über einen Wert zum Testen:**
     <table class="standard-table">
      <tbody>
        <tr>
          <th>Kategorie</th>
          <th>
            CSS Wert<br /><span style="font-size: x-small"
              >Mouseover zum Testen</span
            >
          </th>
          <th></th>
          <th>Beschreibung</th>
        </tr>
        <tr style="cursor: auto">
          <td rowspan="3">Allgemein</td>
          <td><code>auto</code></td>
          <td></td>
          <td>
            Der Browser bestimmt aufgrund des aktuellen Kontextes, welcher Cursor
            angezeigt wird.<br />Wenn der Mauszeiger sich zum Beispiel über dem Text
            befindet, wird der <code>text</code> Cursor angezeigt.
          </td>
        </tr>
        <tr style="cursor: default">
          <td><code>default</code></td>
          <td>
            <img
              alt="default.gif"
              class="default internal"
              src="/@api/deki/files/3438/=default.gif"
            />
          </td>
          <td>Standard Cursor. Üblicherweise durch ein Pfeil dargestellt.</td>
        </tr>
        <tr style="cursor: none">
          <td><code>none</code></td>
          <td></td>
          <td>Es wird kein Cursor wird angezeigt.</td>
        </tr>
        <tr style="cursor: context-menu">
          <td rowspan="5" style="cursor: auto">Links &#x26; Status</td>
          <td><code>context-menu</code></td>
          <td>
            <img
              alt="context-menu.png"
              class="default internal"
              src="/@api/deki/files/3461/=context-menu.png"
            />
          </td>
          <td>
            Ein Kontextmenü wird unter dem Cursor angezeigt.<br />Unter Windows
            nicht verfügbar. {{ Bug("258960") }}
          </td>
        </tr>
        <tr style="cursor: help">
          <td><code>help</code></td>
          <td>
            <img
              alt="help.gif"
              class="default internal"
              src="/@api/deki/files/3442/=help.gif"
            />
          </td>
          <td>Zeigt an, dass Hilfe verfügbar ist.</td>
        </tr>
        <tr style="cursor: pointer">
          <td><code>pointer</code></td>
          <td>
            <img
              alt="pointer.gif"
              class="default internal"
              src="/@api/deki/files/3449/=pointer.gif"
            />
          </td>
          <td>
            Wird zum Beispiel angezeigt, wenn der Mauszeiger sich über Links
            befindet. Üblicherweise durch eine Hand dargestellt.
          </td>
        </tr>
        <tr style="cursor: progress">
          <td><code>progress</code></td>
          <td>
            <img
              alt="progress.gif"
              class="default internal"
              src="/@api/deki/files/3450/=progress.gif"
            />
          </td>
          <td>
            Zeigt an, dass das Programm im Hintergrund arbeitet und der Benutzer
            kann, anders als bei <code>wait</code>, weiterhin mit der Oberfläche
            arbeiten.
          </td>
        </tr>
        <tr style="cursor: wait">
          <td><code>wait</code></td>
          <td>
            <img
              alt="wait.gif"
              class="default internal"
              src="/@api/deki/files/3457/=wait.gif"
            />
          </td>
          <td>
            Zeigt an, dass das Programm arbeitet. Manchmal auch durch eine Sanduhr
            oder eine Uhr dargestellt.
          </td>
        </tr>
        <tr style="cursor: cell">
          <td rowspan="4" style="cursor: auto">Auswahl</td>
          <td><code>cell</code></td>
          <td>
            <img
              alt="cell.gif"
              class="default internal"
              src="/@api/deki/files/3434/=cell.gif"
            />
          </td>
          <td>Zeigt an, dass Zellen ausgewählt werden können.</td>
        </tr>
        <tr style="cursor: crosshair">
          <td><code>crosshair</code></td>
          <td>
            <img
              alt="crosshair.gif"
              class="default internal"
              src="/@api/deki/files/3437/=crosshair.gif"
            />
          </td>
          <td>
            Ein Kreuz, das oft zur Auswahl eines Bereiches in Bildern verwendet
            wird.
          </td>
        </tr>
        <tr style="cursor: text">
          <td><code>text</code></td>
          <td>
            <img
              alt="text.gif"
              class="default internal"
              src="https://developer.mozilla.org/files/3809/text.gif"
            />
          </td>
          <td>Zeigt an, dass der Text ausgewählt werden kann.</td>
        </tr>
        <tr style="cursor: vertical-text">
          <td><code>vertical-text</code></td>
          <td>
            <img
              alt="vertical-text.gif"
              class="default internal"
              src="/@api/deki/files/3456/=vertical-text.gif"
            />
          </td>
          <td>Zeigt an, dass vertikaler Text ausgewählt werden kann.</td>
        </tr>
        <tr style="cursor: alias">
          <td rowspan="5" style="cursor: auto">Drag and Drop</td>
          <td><code>alias</code></td>
          <td>
            <img
              alt="alias.gif"
              class="default internal"
              src="/@api/deki/files/3432/=alias.gif"
            />
          </td>
          <td>Zeigt an, dass ein Tastenkürzel vorhanden ist.</td>
        </tr>
        <tr style="cursor: copy">
          <td><code>copy</code></td>
          <td>
            <img
              alt="copy.gif"
              class="default internal"
              src="/@api/deki/files/3436/=copy.gif"
            />
          </td>
          <td>Zeigt an, dass etwas kopiert werden kann.</td>
        </tr>
        <tr style="cursor: move">
          <td><code>move</code></td>
          <td>
            <img
              alt="move.gif"
              class="default internal"
              src="/@api/deki/files/3443/=move.gif"
            />
          </td>
          <td>Zeigt an, dass das Objekt bewegt werden kann.</td>
        </tr>
        <tr style="cursor: no-drop">
          <td><code>no-drop</code></td>
          <td>
            <img
              alt="no-drop.gif"
              class="internal"
              src="/@api/deki/files/3445/=no-drop.gif"
            />
          </td>
          <td>
            Zeigt an, dass an der aktuellen Stelle nichts hinein gezogen werden
            darf.<br />{{bug("275173")}} unter Windows ist
            <code>no-drop</code> gleich wie <code>not-allowed</code>.
          </td>
        </tr>
        <tr style="cursor: not-allowed">
          <td><code>not-allowed</code></td>
          <td>
            <img
              alt="not-allowed.gif"
              class="default internal"
              src="/@api/deki/files/3446/=not-allowed.gif"
            />
          </td>
          <td>Zeigt an, dass hier etwas nicht erlaubt ist.</td>
        </tr>
        <tr style="cursor: all-scroll">
          <td rowspan="15" style="cursor: auto">Skalierung &#x26; Scrollen</td>
          <td><code>all-scroll</code></td>
          <td>
            <img
              alt="all-scroll.gif"
              class="default internal"
              src="/@api/deki/files/3433/=all-scroll.gif"
            />
          </td>
          <td>
            Zeigt an, dass etwas in alle Richtungen gescrollt werden kann.<br />{{ bug("275174") }}
            unter Windows ist <code>all-scroll</code> gleich wie <code>move</code>.
          </td>
        </tr>
        <tr style="cursor: col-resize">
          <td><code>col-resize</code></td>
          <td>
            <img
              alt="col-resize.gif"
              class="default internal"
              src="/@api/deki/files/3435/=col-resize.gif"
            />
          </td>
          <td>
            Zeigt an, dass das Element bzw. die Spalte horizontal skaliert werden
            kann. Meistens als Pfeile dargestellt, die nach rechts und links zeigen
            und in der Mitte einen Trennbalken haben.
          </td>
        </tr>
        <tr style="cursor: row-resize">
          <td><code>row-resize</code></td>
          <td>
            <img
              alt="row-resize.gif"
              class="default internal"
              src="/@api/deki/files/3451/=row-resize.gif"
            />
          </td>
          <td>
            Zeigt an, dass das Element bzw. die Zeile vertikal skaliert werden kann.
            Meistens als Pfeile dargestellt, die nach unten und oben zeigen und in
            der Mitte einen Trennbalken haben.
          </td>
        </tr>
        <tr style="cursor: n-resize">
          <td><code>n-resize</code></td>
          <td>
            <img
              alt="n-resize.gif"
              class="default internal"
              src="https://developer.mozilla.org/files/4083/n-resize.gif"
            />
          </td>
          <td rowspan="8">
            Zeigt an, dass von einer Ecke aus skaliert werden kann. Der
            <code>se-resize</code> Cursor wird zum Beispiel benutzt, wenn, von der
            unteren rechten Ecke aus, etwas bewegt/skaliert werden soll.
          </td>
        </tr>
        <tr style="cursor: e-resize">
          <td><code>e-resize</code></td>
          <td>
            <img
              alt="e-resize.gif"
              class="default internal"
              src="https://developer.mozilla.org/files/4085/e-resize.gif"
            />
          </td>
        </tr>
        <tr style="cursor: s-resize">
          <td><code>s-resize</code></td>
          <td>
            <img
              alt="s-resize.gif"
              class="default internal"
              src="https://developer.mozilla.org/files/4087/s-resize.gif"
            />
          </td>
        </tr>
        <tr style="cursor: w-resize">
          <td><code>w-resize</code></td>
          <td>
            <img
              alt="w-resize.gif"
              class="default internal"
              src="https://developer.mozilla.org/files/4089/w-resize.gif"
            />
          </td>
        </tr>
        <tr style="cursor: ne-resize">
          <td><code>ne-resize</code></td>
          <td>
            <img
              alt="ne-resize.gif"
              class="default internal"
              src="https://developer.mozilla.org/files/4091/ne-resize.gif"
            />
          </td>
        </tr>
        <tr style="cursor: nw-resize">
          <td><code>nw-resize</code></td>
          <td>
            <img
              alt="nw-resize.gif"
              class="default internal"
              src="https://developer.mozilla.org/files/4093/nw-resize.gif"
            />
          </td>
        </tr>
        <tr style="cursor: se-resize">
          <td><code>se-resize</code></td>
          <td>
            <img
              alt="se-resize.gif"
              class="default internal"
              src="https://developer.mozilla.org/files/4097/se-resize.gif"
            />
          </td>
        </tr>
        <tr style="cursor: sw-resize">
          <td><code>sw-resize</code></td>
          <td>
            <img
              alt="sw-resize.gif"
              class="default internal"
              src="https://developer.mozilla.org/files/4095/sw-resize.gif"
            />
          </td>
        </tr>
        <tr style="cursor: ew-resize">
          <td><code>ew-resize</code></td>
          <td>
            <img
              alt="ew-resize.gif"
              class="default internal"
              src="https://developer.mozilla.org/files/3806/3-resize.gif"
            />
          </td>
          <td rowspan="4">
            Zeigt an, dass in zwei Richtungen (bidirektional) skaliert werden kann.
          </td>
        </tr>
        <tr style="cursor: ns-resize">
          <td><code>ns-resize</code></td>
          <td>
            <img
              alt="ns-resize.gif"
              class="default internal"
              src="https://developer.mozilla.org/files/3808/6-resize.gif"
            />
          </td>
        </tr>
        <tr style="cursor: nesw-resize">
          <td><code>nesw-resize</code></td>
          <td>
            <img
              alt="nesw-resize.gif"
              class="default internal"
              src="https://developer.mozilla.org/files/3805/1-resize.gif"
              style="height: 26px; width: 26px"
            />
          </td>
        </tr>
        <tr style="cursor: nwse-resize">
          <td><code>nwse-resize</code></td>
          <td>
            <img
              alt="nwse-resize.gif"
              class="default internal"
              src="https://developer.mozilla.org/files/3807/4-resize.gif"
            />
          </td>
        </tr>
        <tr style="cursor: zoom-in">
          <td rowspan="2">Zoom</td>
          <td><code>zoom-in</code></td>
          <td>
            <img
              alt="zoom-in.gif"
              class="default"
              src="/@api/deki/files/3459/=zoom-in.gif"
            />
          </td>
          <td rowspan="2" style="cursor: auto">
            <p>Indicates that something can be zoomed (magnified) in or out.</p>
          </td>
        </tr>
        <tr style="cursor: zoom-out">
          <td><code>zoom-out</code></td>
          <td>
            <img
              alt="zoom-out.gif"
              class="default"
              src="/@api/deki/files/3460/=zoom-out.gif"
            />
          </td>
        </tr>
        <tr id="grab" style="cursor: grab">
          <td rowspan="2">Greifen</td>
          <td><code>grab</code></td>
          <td>
            <img
              alt="grab.gif"
              class="default"
              src="/@api/deki/files/3440/=grab.gif"
            />
          </td>
          <td rowspan="2" style="cursor: auto">
            <p>Indicates that something can be grabbed (dragged to be moved).</p>
          </td>
        </tr>
        <tr style="cursor: grabbing">
          <td><code>grabbing</code></td>
          <td>
            <img
              alt="grabbing.gif"
              class="default"
              src="/@api/deki/files/3441/=grabbing.gif"
            />
          </td>
        </tr>
      </tbody>
    </table>

### Formale Syntax

{{csssyntax}}

## Beispiele

    .foo {
      cursor: crosshair;
    }

    /* Benutze move wenn cell nicht unterstützt wird. */
    .bar {
      cursor: move;
      cursor: cell;
    }

    /* Standardwert als Fallback für url() muss angegeben werden (funktioniert nicht ohne) */
    .baz {
      cursor: url(hyper.cur), auto;
    }

## Spezifikationen

| Spezifikation                                                                | Status                               | Kommentar                                                                      |
| ---------------------------------------------------------------------------- | ------------------------------------ | ------------------------------------------------------------------------------ |
| {{SpecName('CSS3 Basic UI', '#cursor', 'cursor')}}         | {{Spec2('CSS3 Basic UI')}} | Mehrere Schlüsselwörter und die Positionierungssyntax für `url()` hinzugefügt. |
| {{SpecName('CSS2.1', 'ui.html#cursor-props', 'cursor')}} | {{Spec2('CSS2.1')}}             | Ursprüngliche Definition                                                       |

## Browser Kompatibilität

{{Compat("css.properties.cursor")}}

## Siehe auch

- [Using URL values for the cursor property (en)](/de/docs/CSS/Using_URL_values_for_the_cursor_property "Using URL values for the cursor property")
- {{cssxref("pointer-events")}}
