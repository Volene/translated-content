---
title: Array.prototype.indexOf()
slug: Web/JavaScript/Reference/Global_Objects/Array/indexOf
tags:
  - Array
  - JavaScript
  - Method
  - Prototype
  - Reference
  - polyfill
translation_of: Web/JavaScript/Reference/Global_Objects/Array/indexOf
---
{{JSRef}}

Die Methode **`indexOf()`** gibt den Index zurück, an dem ein bestimmtes Element im Array zum ersten Mal auftritt oder -1 wenn es nicht vorhanden ist.

> **Note:** **Hinweis:** Für die String Methode, siehe {{jsxref("String.prototype.indexOf()")}}.

{{EmbedInteractiveExample("pages/js/array-indexof.html")}}

## Syntax

    arr.indexOf(searchElement[, fromIndex])

### Parameter

- `searchElement`
  - : Element, das im Array gefunden werden soll.
- `fromIndex` {{optional_inline}}
  - : Der Index, an dem die Suche beginnen soll. Wenn dieser Index größer oder gleich der Länge des Arrays ist, wird -1 zurückgegeben, d. h. das Array wird nicht durchsucht. Ist der Startindex negativ, wird er als Versatz vom Ende des Arrays verstanden. Das Array wird dann immer noch von vorne nach hinten durchsucht.

### Rückgabewert

Der Index, an dem das gefundene Element das erste Mal angetroffen wurde, andernfalls **-1** wenn nichts gefunden wurde.

## Beschreibung

`indexOf()` vergleicht `searchElement` mit Elementen des Arrays mittels [strikter Gleichheit](/de/docs/Web/JavaScript/Reference/Operators/Vergleichsoperatoren#Die_Gleichheitsoperatoren_anwenden) (dieselbe Methode, die bei `===` angewendet wird).

## Beispiele

### Verwendung von `indexOf()`

Das folgende Beispiel nutzt `indexOf()` um Werte in einem Array zu ermitteln.

```js
var array = [2, 9, 9];
array.indexOf(2);     // 0
array.indexOf(7);     // -1
array.indexOf(9, 2);  // 2
array.indexOf(2, -1); // -1
array.indexOf(2, -3); // 0
```

### Alle Vorkommnisse eines Elements ermitteln

```js
var indices = [];
var array = ['a', 'b', 'a', 'c', 'a', 'd'];
var element = 'a';
var idx = array.indexOf(element);
while (idx != -1) {
  indices.push(idx);
  idx = array.indexOf(element, idx + 1);
}
console.log(indices);
// [0, 2, 4]
```

### Ermitteln, ob ein Element in einem Array existiert und das Array aktualisieren

```js
function updateVegetablesCollection (veggies, veggie) {
    if (veggies.indexOf(veggie) === -1) {
        veggies.push(veggie);
        console.log('New veggies collection is : ' + veggies);
    } else if (veggies.indexOf(veggie) > -1) {
        console.log(veggie + ' already exists in the veggies collection.');
    }
}

var veggies = ['potato', 'tomato', 'chillies', 'green-pepper'];

updateVegetablesCollection(veggies, 'spinach');
// New veggies collection is : potato,tomato,chillies,green-pepper,spinach
updateVegetablesCollection(veggies, 'spinach');
// spinach already exists in the veggies collection.
```

## Polyfill

`indexOf()` wurde dem ECMA-262-Standard in der 5. Auflage hinzugefügt. Als solches ist es möglicherweise nicht in allen Implementierungen des Standards enthalten. Sie können dies umgehen, indem Sie den folgenden Code am Anfang Ihrer Skripte einfügen, um die Verwendung von `indexOf()` in Implementierungen zu ermöglichen, die es nicht nativ unterstützen. Dieser Algorithmus entspricht dem in der 5. Auflage von ECMA-262 angegebenen Algorithmus, vorausgesetzt {{jsxref("TypeError")}} und {{jsxref("Math.abs()")}} haben ihre ursprünglichen Werte.

```js
if (!Array.prototype.indexOf)  Array.prototype.indexOf = (function(Object, max, min){
  "use strict";
  return function indexOf(member, fromIndex) {
    if(this===null||this===undefined)throw TypeError("Array.prototype.indexOf called on null or undefined");

    var that = Object(this), Len = that.length >>> 0, i = min(fromIndex | 0, Len);
    if (i < 0) i = max(0, Len+i); else if (i >= Len) return -1;

    if(member===void 0){ for(; i !== Len; ++i) if(that[i]===void 0 && i in that) return i; // undefined
    }else if(member !== member){   for(; i !== Len; ++i) if(that[i] !== that[i]) return i; // NaN
    }else                           for(; i !== Len; ++i) if(that[i] === member) return i; // all else

    return -1; // if the value was not found, then return -1
  };
})(Object, Math.max, Math.min);
```

Wenn Sie sich jedoch mehr für all die kleinen technischen Elemente interessieren, die durch den ECMA-Standard definiert werden, und Leistung oder Prägnanz weniger von Belang sind, dann könnte diese erklärende Polyfill-Lösung nützlicher für Sie sein.

```js
// Production steps of ECMA-262, Edition 5, 15.4.4.14
// Reference: http://es5.github.io/#x15.4.4.14
if (!Array.prototype.indexOf) {
  Array.prototype.indexOf = function(searchElement, fromIndex) {

    var k;

    // 1. Let o be the result of calling ToObject passing
    //    the this value as the argument.
    if (this == null) {
      throw new TypeError('"this" is null or not defined');
    }

    var o = Object(this);

    // 2. Let lenValue be the result of calling the Get
    //    internal method of o with the argument "length".
    // 3. Let len be ToUint32(lenValue).
    var len = o.length >>> 0;

    // 4. If len is 0, return -1.
    if (len === 0) {
      return -1;
    }

    // 5. If argument fromIndex was passed let n be
    //    ToInteger(fromIndex); else let n be 0.
    var n = fromIndex | 0;

    // 6. If n >= len, return -1.
    if (n >= len) {
      return -1;
    }

    // 7. If n >= 0, then Let k be n.
    // 8. Else, n<0, Let k be len - abs(n).
    //    If k is less than 0, then let k be 0.
    k = Math.max(n >= 0 ? n : len - Math.abs(n), 0);

    // 9. Repeat, while k < len
    while (k < len) {
      // a. Let Pk be ToString(k).
      //   This is implicit for LHS operands of the in operator
      // b. Let kPresent be the result of calling the
      //    HasProperty internal method of o with argument Pk.
      //   This step can be combined with c
      // c. If kPresent is true, then
      //    i.  Let elementK be the result of calling the Get
      //        internal method of o with the argument ToString(k).
      //   ii.  Let same be the result of applying the
      //        Strict Equality Comparison Algorithm to
      //        searchElement and elementK.
      //  iii.  If same is true, return k.
      if (k in o && o[k] === searchElement) {
        return k;
      }
      k++;
    }
    return -1;
  };
}
```

## Spezifikationen

| Specification                                                                                                | Status                       | Comment                                               |
| ------------------------------------------------------------------------------------------------------------ | ---------------------------- | ----------------------------------------------------- |
| {{SpecName('ES5.1', '#sec-15.4.4.14', 'Array.prototype.indexOf')}}                     | {{Spec2('ES5.1')}}     | Initiale Definition. Implementiert in JavaScript 1.6. |
| {{SpecName('ES6', '#sec-array.prototype.indexof', 'Array.prototype.indexOf')}}     | {{Spec2('ES6')}}         |                                                       |
| {{SpecName('ESDraft', '#sec-array.prototype.indexof', 'Array.prototype.indexOf')}} | {{Spec2('ESDraft')}} |                                                       |

## Browserkompatibilität

{{Compat("javascript.builtins.Array.indexOf")}}

## Kompatibilitätshinweise

- Ab Firefox 47 {{geckoRelease(47)}} gibt diese Methode nicht mehr -0 zurück, z. B. gibt `[0].indexOf(0, -0)` jetzt immer `+0` zurück ({{bug(1242043)}}).

## Siehe auch

- {{jsxref("Array.prototype.lastIndexOf()")}}
- {{jsxref("TypedArray.prototype.indexOf()")}}
- {{jsxref("String.prototype.indexOf()")}}
