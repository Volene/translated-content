---
title: String.prototype.charAt()
slug: Web/JavaScript/Reference/Global_Objects/String/charAt
tags:
  - JavaScript
  - Method
  - Prototype
  - Reference
  - String
translation_of: Web/JavaScript/Reference/Global_Objects/String/charAt
---
{{JSRef}}

Die **`charAt()`**-Methode gibt das Zeichen an einer bestimmten Stelle eines Strings wieder.

## Syntax

    str.charAt(index)

### Parameter

- `index`
  - : Eine Zahl zwischen 0 und `str.length-1`. Ist kein `index` gegeben, ist dieser automatisch 0.

### Wiedergegebener Wert

Ein String, der das Zeichen an der angegebenen `index`-Stelle wiedergibt. Wenn `index` außerhalb der Reichweite liegt, wird ein leerer String zurückgegeben.

## Beschreibung

Zeichen in einem String werden von links nach rechts indexiert. Der Index des ersten Zeichens ist 0, der Index des letzten Zeichens eines Strings namens `stringName` ist` stringName.length - 1`.

Wenn kein Index bereitgestellt wird, ist dieser standardmäßig 0.

## Beispiele

### Wiedergabe von Zeichen an verschiedenen Stellen eines Strings

Das folgende Beispiel gibt Zeichen an verschiedenen Orten im String "`Brave new world`" wieder:

```js
var anyString = 'Brave new world';
console.log("Das Zeichen bei Index 0   ist '" + anyString.charAt()   + "'");
// kein Index definiert, 0 als Standard genutzt

console.log("Das Zeichen bei Index 0   ist '" + anyString.charAt(0)   + "'");
console.log("Das Zeichen bei Index 1   ist '" + anyString.charAt(1)   + "'");
console.log("Das Zeichen bei Index 2   ist '" + anyString.charAt(2)   + "'");
console.log("Das Zeichen bei Index 3   ist '" + anyString.charAt(3)   + "'");
console.log("Das Zeichen bei Index 4   ist '" + anyString.charAt(4)   + "'");
console.log("Das Zeichen bei Index 999 ist '" + anyString.charAt(999) + "'");
```

Diese Zeilen geben folgendes wieder:

```js
Das Zeichen bei Index 0   ist 'B'
Das Zeichen bei Index 0   ist 'B'
Das Zeichen bei Index 1   ist 'r'
Das Zeichen bei Index 2   ist 'a'
Das Zeichen bei Index 3   ist 'v'
Das Zeichen bei Index 4   ist 'e'
Das Zeichen bei Index 999 ist ''
```

### Erhalten von vollständigen Zeichen

Der folgende Code versichert, dass der Gebrauch eines String-Loops immer das vollständige Zeichen wiedergibt - auch wenn der String Zeichen enthält, die nicht auf der mehrsprachigen Basisebene (MBE) vorhanden sind.

```js
var str = 'A \uD87E\uDC04 Z'; // direkter Einsatz von nicht MBE-Zeichen auch möglich
for (var i = 0, chr; i < str.length; i++) {
  if ((chr = getWholeChar(str, i)) === false) {
    continue;
  }
  // Übernehme diese Zeile zu Beginn jedes Loops,
  // gib den kompletten String und Iterator an
  // und gebe eine Variable wieder, die das individuelle Zeichen wiederspiegelt.

  console.log(chr);
}

function getWholeChar(str, i) {
  var code = str.charCodeAt(i);

  if (Number.isNaN(code)) {
    return ''; // Position not found
  }
  if (code < 0xD800 || code > 0xDFFF) {
    return str.charAt(i);
  }

  // High surrogate (could change last hex to 0xDB7F to treat high private
  // surrogates as single characters)
  if (0xD800 <= code && code <= 0xDBFF) {
    if (str.length <= (i + 1)) {
      throw 'High surrogate without following low surrogate';
    }
    var next = str.charCodeAt(i + 1);
      if (0xDC00 > next || next > 0xDFFF) {
        throw 'High surrogate without following low surrogate';
      }
      return str.charAt(i) + str.charAt(i + 1);
  }
  // Low surrogate (0xDC00 <= code && code <= 0xDFFF)
  if (i === 0) {
    throw 'Low surrogate without preceding high surrogate';
  }
  var prev = str.charCodeAt(i - 1);

  // (could change last hex to 0xDB7F to treat high private
  // surrogates as single characters)
  if (0xD800 > prev || prev > 0xDBFF) {
    throw 'Low surrogate without preceding high surrogate';
  }
  // We can pass over low surrogates now as the second component
  // in a pair which we have already processed
  return false;
}
```

In einer ECMAScript 2016-Umgebung, welche destruktive Benennung erlaubt, ist eine bündigere und zu gewissem Grad flexiblere Alternative möglich, da es automatisch eine Erhöhung der entsprechenden Variable vornimmt (wenn das Zeichen
ein Ersatzpaar ist).

```js
var str = 'A\uD87E\uDC04Z'; // direkter Einsatz von nicht MBE-Zeichen auch möglich
for (var i = 0, chr; i < str.length; i++) {
  [chr, i] = getWholeCharAndI(str, i);
  // Adapt this line at the top of each loop, passing in the whole string and
  // the current iteration and returning an array with the individual character
  // and 'i' value (only changed if a surrogate pair)
  // Übernehme diese Zeile zu Beginn jedes Loops,
  // gib den kompletten String und Iterator an
  // und gebe einen Array wieder, der die individuellen Zeichen und 'i'-Wert wiederspiegelt
  // (nur geändert, wenn Ersatzpaar).

  console.log(chr);
}

function getWholeCharAndI(str, i) {
  var code = str.charCodeAt(i);

  if (Number.isNaN(code)) {
    return ''; // Position nicht gefunden
  }
  if (code < 0xD800 || code > 0xDFFF) {
    return [str.charAt(i), i]; // Normales Zeichen, 'i' bleibt gleich
  }

  // High surrogate (could change last hex to 0xDB7F to treat high private
  // surrogates as single characters)
  if (0xD800 <= code && code <= 0xDBFF) {
    if (str.length <= (i + 1)) {
      throw 'High surrogate without following low surrogate';
    }
    var next = str.charCodeAt(i + 1);
      if (0xDC00 > next || next > 0xDFFF) {
        throw 'High surrogate without following low surrogate';
      }
      return [str.charAt(i) + str.charAt(i + 1), i + 1];
  }
  // Low surrogate (0xDC00 <= code && code <= 0xDFFF)
  if (i === 0) {
    throw 'Low surrogate without preceding high surrogate';
  }
  var prev = str.charCodeAt(i - 1);

  // (could change last hex to 0xDB7F to treat high private surrogates
  // as single characters)
  if (0xD800 > prev || prev > 0xDBFF) {
    throw 'Low surrogate without preceding high surrogate';
  }
  // Return the next character instead (and increment)
  return [str.charAt(i + 1), i + 1];
}
```

### Korrigiere `charAt()`, um Zeichen der nicht mehrsprachigen Basisebene (MBE) zu unterstützen

Das obige Beispiel dürfte häufiger für diejenigen hilfreich sein, die nicht MBE-Zeichen unterstützen möchten (da man nicht wissen muss, wo nicht MBE-Zeichen vorkommen). Falls man wünscht (durch Angabe eines Indexwerts) die Ersatzpaare innerhalb eines Strings als Einzelcharakter zu behandeln, kann man folgendes nutzen:

```js
function fixedCharAt(str, idx) {
  var ret = '';
  str += '';
  var end = str.length;

  var surrogatePairs = /[\uD800-\uDBFF][\uDC00-\uDFFF]/g;
  while ((surrogatePairs.exec(str)) != null) {
    var li = surrogatePairs.lastIndex;
    if (li - 2 < idx) {
      idx++;
    } else {
      break;
    }
  }

  if (idx >= end || idx < 0) {
    return '';
  }

  ret += str.charAt(idx);

  if (/[\uD800-\uDBFF]/.test(ret) && /[\uDC00-\uDFFF]/.test(str.charAt(idx + 1))) {
    // Gehe eins weiter, da eins der Zeichen Teil eines Ersatzpaares ist
    ret += str.charAt(idx + 1);
  }
  return ret;
}
```

## Spezifikationen

| Spezifikation                                                                                                | Status                       | Kommentar        |
| ------------------------------------------------------------------------------------------------------------ | ---------------------------- | ---------------- |
| {{SpecName('ES1')}}                                                                                     | {{Spec2('ES1')}}         | erste Definition |
| {{SpecName('ES5.1', '#sec-15.5.4.4', 'String.prototype.charAt')}}                     | {{Spec2('ES5.1')}}     |                  |
| {{SpecName('ES6', '#sec-string.prototype.charat', 'String.prototype.charAt')}}     | {{Spec2('ES6')}}         |                  |
| {{SpecName('ESDraft', '#sec-string.prototype.charat', 'String.prototype.charAt')}} | {{Spec2('ESDraft')}} |                  |

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{jsxref("String.prototype.indexOf()")}}
- {{jsxref("String.prototype.lastIndexOf()")}}
- {{jsxref("String.prototype.charCodeAt()")}}
- {{jsxref("String.prototype.codePointAt()")}}
- {{jsxref("String.prototype.split()")}}
- {{jsxref("String.fromCodePoint()")}}
- [JavaScript has a Unicode problem – Mathias Bynens](https://mathiasbynens.be/notes/javascript-unicode)
