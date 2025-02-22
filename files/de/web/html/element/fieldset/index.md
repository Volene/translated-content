---
title: <fieldset>
slug: Web/HTML/Element/fieldset
translation_of: Web/HTML/Element/fieldset
---
HTMLRef

Das **HTML \<fieldset> -Element** wird verwendet, um mehrere Steuerelemente sowie Bezeichnungen (HTMLElement ("label")) in einem Webformular zu gruppieren.

| Inhaltsverzeichnis    | fließender-Inhalt, sektion Wurzel, gelistete, formordnender Element, eindeutiger Inhalt. |
| --------------------- | ---------------------------------------------------------------------------------------- |
| Erlaubter Inhalt      | Ein optionales HTMLElement <legend>, gefolgt von einem fließendem Inhalt.                |
| Tag-Auslassung        | Keine                                                                                    |
| Erlaubte Eltern       | Jedes Element, das den flow content akzeptiert.                                          |
| Zulässige ARIA-Rollen | ARIARole("group"), ARIARole("presentation")                                              |
| DOM Schnittstelle     | {{domxref("HTMLFieldSetElement")}}                                             |

> **Note:** **Anmerkung:** Im Gegensatz zu fast jedem anderen Element schlägt die WHATWG-HTML-Rendering-Spezifikation cssxref ("min-width") vor: min-content als Teil des Standardstils für HTMLElement ("fieldset") und viele Browser implementieren solches Styling (oder etwas, das es annähert).

> **Note:** **Anmerkung:** Mit dem Element HTMLElement ("fieldset") wird erwartet, dass es einen neuen Kontext für die Blockformatierung herstellt (siehe HTML5-Spezifikation).

## Attribute

Dieses Element enthält die globalen Attribute.

- htmlattrdef("disabled") HTMLVersionInline(5)
  - : Wenn dieses boolesche Attribut gesetzt ist, sind die Formularsteuerelemente, die seine Nachfolger sind, mit Ausnahme der Nachfolger des ersten optionalen Elements HTMLElement ("legend"), deaktiviert, d.h. nicht editierbar. Sie erhalten keine Browserereignisse wie Mausklicks oder Fokus-bezogene Ereignisse. Oft zeigen Browser solche Steuerelemente als grau an.
- htmlattrdef("form") HTMLVersionInline(5)
  - : Dieses Attribut hat den Wert des id-Attributs des HTMLElement ("form") , mit dem es verknüpft ist. Ihr Standardwert ist die ID des nächsten HTMLElement ("Formular") , von dem sie abstammt.
- htmlattrdef("name") HTMLVersionInline(5)
  - : Der Name, der der Gruppe zugeordnet ist
    > **Note:** Die Bezeichnung für das Feldset wird durch das erste HTMLElement ("legend") angegeben, das ein untergeordnetes Element(Kind Element) dieses Feldsatzes ist.

## Beispiele

### Example #1: Form with fieldset, legend, and label

```html
<form action="test.php" method="post">
  <fieldset>
    <legend>Title</legend>
    <input type="radio" id="radio">
    <label for="radio">Click me</label>
  </fieldset>
</form>
```

### Example #2: Simulieren eines editierbaren HTMLElement ("select") durch ein Feldset von Radioboxen und Textboxen \*

Das folgende Beispiel besteht aus reinem HTML und CSS. Es gibt keinen JavaScript-Code.

Seien Sie gewarnt, dass Bildschirmleser und Hilfsgeräte das folgende Formular nicht korrekt interpretieren. Dieses Beispiel wäre ungültiger HTML-Code, wenn die richtigen Elemente verwendet würden.

```html
<!doctype html>
<html>
<head>
<meta charset="UTF-8" />
<title>Editable [pseudo]select</title>
<style type="text/css">

/* Generic form fields */

fieldset.elist, input[type="text"], textarea, select,
option, fieldset.elist ul, fieldset.elist > legend,
fieldset.elist input[type="text"],
fieldset.elist > legend:after {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}

input[type="text"] {
  padding: 0 20px;
}

textarea {
  width: 500px;
  height: 200px;
  padding: 20px;
}

textarea, input[type="text"], fieldset.elist ul,
select, fieldset.elist > legend {
  border: 2px #cccccc solid;
  border-radius: 10px;
}

input[type="text"], fieldset.elist, select,
fieldset.elist > legend {
  height: 32px;
  font-family: Tahoma;
  font-size: 14px;
}

input[type="text"]:hover, textarea:hover,
select:hover, fieldset.elist:hover > legend {
  background-color: #ddddff;
}

select {
  padding: 4px 20px;
}

option {
  height: 30px;
  padding: 5px 4px;
}

option:not(:checked), textarea:focus {
  background-color: #ffcccc;
}

fieldset.elist > legend:after,
fieldset.elist label {
  height: 28px;
}

input[type="text"], fieldset.elist {
  width: 316px;
}

input[type="text"]:focus {
  background: #ffcccc url("data:image/gif;
  base64,R0lGODlhEAAQANU5APnoxuvr6+uxPdvb2+
  rq6ri4uO7qxunp6dPT06SHV+/rx8vLy+
  nezLO0sbe3t9Ksas+qaaCEV8rKyp2dnf39/
  QAAAK6ursifZHFxcc/
  Qzu3mxYyMjExCJnV1dc6maO7u7o+
  Pj2tXNoaGhtfDpKCDVu3lxM+
  tcaKEV9bW1qOFVWNjY8KrisTExNra2nBbObGxsby8vO/
  mu7Kyso9ZAuzs7MSgAIiKhf///8zMzP///
  wAAAAAAAAAAAAAAAAAAAAAAACH5BAEAADkALAAAAAAQ
  ABAAAAaXwJxwSCwOYzWkMpkkZmoAqDQaJdpqAqw2m53
  NRjlboAarFczomcE0C99o8DgNMVM8Tm3bbYDr9x11Dw
  kzDG5yc2oQJIRCenx/MxoeETM2Q3pxATMlF4MYlo17O
  AsdLispMyAioIY0BzMcITMTKBasjgssFTMqGxItMjYU
  oTQBBAQHxgE0wZcfMtDRMi/QrA022NnaNg1CQQA7")
  no-repeat 2px center !important;
}

input[type="text"]:focus, textarea:focus,
select:focus, fieldset.elist > legend {
  border: 2px #ccaaaa solid;
}

fieldset {
  border: 2px #af3333 solid;
  border-radius: 10px;
}

/* Editable [pseudo]select
(i.e. fieldsets with [class=elist]) */

fieldset.elist {
  display: inline-block;
  position: relative;
  vertical-align: middle;
  overflow: visible;
  padding: 0;
  margin: 0;
  border: none;
}

fieldset.elist ul {
  position: absolute;
  width: 100%;
  max-height: 320px;
  padding: 0;
  margin: 0;
  overflow: hidden;
  background-color: transparent;
}

fieldset.elist:hover ul {
  background-color: #ffffff;
  border: 2px #af3333 solid;
  left: 2px;
  overflow: auto;
}

fieldset.elist ul > li {
  list-style-type: none;
  background-color: transparent;
}

fieldset.elist label {
  display: none;
  width: 100%;
}

fieldset.elist input[type="text"] {
  width: 100%;
  height: 30px;
  line-height: 30px;
  border: none;
  background-color: transparent;
  border-radius: 0;
}

fieldset.elist > legend {
  display: block;
  margin: 0;
  padding: 0 0 0 5px;
  position: absolute;
  width: 100%;
  cursor: default;
  background-color: #ccffcc;
  line-height: 30px;
  font-style: italic;
}

fieldset.elist:hover > legend {
  position: relative;
  overflow: hidden;
}

fieldset.elist > legend:after {
  width: 20px;
  content: "\2335";
  float: right;
  text-align: center;
  border-left: 2px #cccccc solid;
  font-style: normal;
  cursor: default;
}

fieldset.elist:hover > legend:after {
  background-color: #99ff99;
}

fieldset.elist ul input[type="radio"] {
  display: none;
}

fieldset.elist input[type="radio"]:checked ~ label {
  display: block;
  width: 292px;
  background-color: #ffffff;
}

fieldset.elist:hover
input[type="radio"]:checked ~ label {
  width: 100%;
}

fieldset.elist:hover label {
  display: block;
  height: 100%;
}

fieldset.elist label:hover {
  background-color: #3333ff !important;
}

fieldset.elist:hover
input[type="radio"]:checked ~ label {
  background-color: #aaaaaa;
}

</style>

</head>
<body>

<form method="get" action="test.php">

<fieldset>
    <legend>Order a T-Shirt</legend>
    <p>Write your name (simple textbox):
    <input type="text" /></p>
    <p>Choose your size (simple select):
    <select>
        <option value="s">Small</option>
        <option value="m">Medium</option>
        <option value="l">Large</option>
        <option value="xl">Extra Large</option>
    </select></p>
    <div>What address do you want to use?
    (editable pseudoselect)
    <fieldset class="elist">
        <legend>Address&hellip;</legend>
        <ul>
            <li><input type="radio" value="1"
            id="address-switch_1" checked
            /><label for="address-switch_1"
            ><input type="text"
            value="19 Quaker Ridge Rd. Bethel CT 06801"
            /></label></li>
            <li><input type="radio" value="2"
            id="address-switch_2"
            /><label for="address-switch_2"
            ><input type="text"
            value="1000 Coney Island Ave.
            Brooklyn NY 11230"
            /></label></li>
            <li><input type="radio" value="3"
            id="address-switch_3"
            /><label for="address-switch_3"
            ><input type="text"
            value="2962 Dunedin Cv. Germantown TN 38138"
            /></label></li>
            <li><input type="radio" value="4"
            id="address-switch_4"
            /><label for="address-switch_4"
            ><input type="text"
            value="915 E 7th St. Apt 6L. Brooklyn NY 11230"
            /></label></li>
        </ul>
    </fieldset>
    </div>
    <p>Write a comment:<br />
    <textarea></textarea></p>
    <p><input type="reset" value="Reset" />
    <input type="submit" value="Send!" /></p>
</fieldset>

</form>

</body>
</html>
```

Betrachten Sie dieses Beispiel in Aktion.

## Spezifikation

| Specification                                                              | Status               | Comment                                                             |
| -------------------------------------------------------------------------- | -------------------- | ------------------------------------------------------------------- |
| SpecName('HTML WHATWG', 'forms.html#the-fieldset-element', '<fieldset>')   | Spec2('HTML WHATWG') | Definition of the `fieldset` element                                |
| SpecName('HTML WHATWG', 'rendering.html#the-fieldset-and-legend-elements') | Spec2('HTML WHATWG') | Suggested default rendering of the `fieldset` and `legend` elements |
| SpecName('HTML5 W3C', 'forms.html#the-fieldset-element', '<fieldset>')     | Spec2('HTML5 W3C')   |                                                                     |
| SpecName('HTML4.01', 'interact/forms.html#h-17.10', '<fieldset>')          | Spec2('HTML4.01')    | Initial definition                                                  |

## Browser compatibility

{{Compat}}

\[1] Nicht alle Formularsteuerungsnachkommen eines deaktivierten Fieldsets sind in IE11 ordnungsgemäß deaktiviert. siehe IE Bug 817488: Eingabe \[Typ = "Datei"] nicht deaktiviert in deaktiviertem Feldset und IE Bug 962368: Kann Eingabe \[Typ = "Text"] innerhalb von Feldset \[deaktiviert] bearbeiten.

## Bugs

- [WebKit bug 123507](https://bugs.webkit.org/show_bug.cgi?id=123507) - `min-width: {{cssxref("-webkit-min-content")}}` on fieldset
- StackOverflow-Diskussion mit Workarounds für die oben genannten Fehler

## Siehe auch

- Andere form-bezogene Elemente: HTMLElement("form"), HTMLElement("legend"), HTMLElement("label"), HTMLElement("button"), HTMLElement("select"), HTMLElement("datalist"), HTMLElement("optgroup"), HTMLElement("option"), HTMLElement("textarea"), HTMLElement("keygen"), HTMLElement("input"), HTMLElement("output"), HTMLElement("progress") and HTMLElement("meter").
