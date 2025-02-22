---
title: Array.from()
slug: Web/JavaScript/Reference/Global_Objects/Array/from
tags:
  - Array
  - ECMAScript 2015
  - JavaScript
  - Method
  - Reference
  - polyfill
translation_of: Web/JavaScript/Reference/Global_Objects/Array/from
---
{{JSRef}}

Die **`Array.from()`** Methode erstellt eine neue, oberflächlich kopierte Array Instanz von einem Array-ähnlichen oder iterierbaren Objekt.

{{EmbedInteractiveExample("pages/js/array-from.html")}}

## Syntax

    Array.from(arrayLike[, mapFn[, thisArg]])

### Parameter

- `arrayLike`
  - : Ein Array-ähnliches oder iterierbares Objekt, welches zu einem Array konvertiert wird.
- `mapFn`{{Optional_inline}}
  - : Map Funktion, welche auf jedes Element des Arrays angewendet wird.
- `thisArg`{{Optional_inline}}
  - : Wert, welcher als `this` beim Ausführen von `mapFn` genutzt wird.

### Rückgabewert

Eine neue {{jsxref("Array")}} Instanz.

## Beschreibung

**`Array.from()`** erstellt ein Array aus:

- Array-ähnliche Objekte (Objekte mit einer `length` Eigenschaft und indexierten Elementen) oder
- [Iterierbare Objekte](/de/docs/Web/JavaScript/Guide/iterable) (Objekte welche Elemente zurückgeben können, wie zum Beispiel {{jsxref("Map")}} und {{jsxref("Set")}}).

**Array.from()** hat einen optionalen Parameter `mapFn`, welcher es erlaubt eine {{jsxref("Array.prototype.map", "map")}} Funktion auf jedem Element des Arrays (oder Subklassen) das erstellt wird, auszuführen. Genauer gesagt, ist `Array.from(obj, mapFn, thisArg)` dasselbe wie `Array.from(obj).map(mapFn, thisArg)`, mit dem Unterschied, dass kein Array als Zwischenergebnis produziert wird. Das ist besonders wichtig für Array Subklassen, wie [typed Arrays](/de/docs/Web/JavaScript/Typed_arrays). Das Array des Zwischenergebnisses
würde sonst Werte kürzen, um dem zutreffenden Typ zu entsprechen.

Die `length` Eigenschaft der `from()` Methode ist 1.

In ES2015 erlaubt die class Syntax, Subklassen für eingebaute und benutzerdefinierte Klassen. Klassenseitige statische Methoden wie `Array.from()` sind von der Subklasse `Array` vererbt und erzeugen eine neue Instanz der Subklasse und nicht von `Array`.

## Beispiele

### Array von einem `String`

```js
Array.from('foo');
// ["f", "o", "o"];
```

### Array von einem `Set`

```js
var s = new Set(["foo", window]);
Array.from(s);
// ["foo", window]
```

### Array von einem `Map`

```js
var m = new Map([[1, 2], [2, 4], [4, 8]]);
Array.from(m);
// [[1, 2], [2, 4], [4, 8]]

var mapper = new Map([['1', 'a'], ['2', 'b']]);
Array.from(mapper.values());
// ['a', 'b'];

Array.from(mapper.keys());
// ['1', '2'];
```

### Array von einem Array ähnlichen Objekt (`arguments`)

```js
function f() {
  return Array.from(arguments);
}

f(1, 2, 3);

// [1, 2, 3]
```

### Einsatz von Arrow-Funktionen und `Array.from`

```js
// Using an arrow function as the map function to
// manipulate the elements
Array.from([1, 2, 3], x => x + x);
// [2, 4, 6]


// Generate a sequence of numbers
// Since the array is initialized with `undefined` on each position,
// the value of `v` below will be `undefined`
Array.from({length: 5}, (v, i) => i);
// [0, 1, 2, 3, 4]
```

## Polyfill

`Array.from()` wurde zum ECMA-262 Standard in der 6ten Version hinzugefügt. Es kann sein, dass diese in anderen Implementationen des Standards nicht verfügbar ist. Man kann das mit folgendem Code am Anfang eines Skriptes umgehen. Das Skript erlaubt das Benutzen von `Array.from()` in Implementationen, welche Array.from() nicht nativ unterstützen. Dieser Algorithmus ist genau derselbe, welcher in EMCA-262, 6te Version implementiert ist, angenommen Object und TypeError haben ihre originalen Werte und `callback.call` evaluiert den Original Wert von {{jsxref("Function.prototype.call")}}. Außerdem können echte iterierbare Elemente nicht mit einem Polyfill implementiert werden. Diese Implementation unterstützt keine generischen iterierbaren Elemente so wie sie definiert sind in der 6ten Version von ECMA-262.

```js
// Production steps of ECMA-262, Edition 6, 22.1.2.1
if (!Array.from) {
  Array.from = (function () {
    var toStr = Object.prototype.toString;
    var isCallable = function (fn) {
      return typeof fn === 'function' || toStr.call(fn) === '[object Function]';
    };
    var toInteger = function (value) {
      var number = Number(value);
      if (isNaN(number)) { return 0; }
      if (number === 0 || !isFinite(number)) { return number; }
      return (number > 0 ? 1 : -1) * Math.floor(Math.abs(number));
    };
    var maxSafeInteger = Math.pow(2, 53) - 1;
    var toLength = function (value) {
      var len = toInteger(value);
      return Math.min(Math.max(len, 0), maxSafeInteger);
    };

    // The length property of the from method is 1.
    return function from(arrayLike/*, mapFn, thisArg */) {
      // 1. Let C be the this value.
      var C = this;

      // 2. Let items be ToObject(arrayLike).
      var items = Object(arrayLike);

      // 3. ReturnIfAbrupt(items).
      if (arrayLike == null) {
        throw new TypeError('Array.from requires an array-like object - not null or undefined');
      }

      // 4. If mapfn is undefined, then let mapping be false.
      var mapFn = arguments.length > 1 ? arguments[1] : void undefined;
      var T;
      if (typeof mapFn !== 'undefined') {
        // 5. else
        // 5. a If IsCallable(mapfn) is false, throw a TypeError exception.
        if (!isCallable(mapFn)) {
          throw new TypeError('Array.from: when provided, the second argument must be a function');
        }

        // 5. b. If thisArg was supplied, let T be thisArg; else let T be undefined.
        if (arguments.length > 2) {
          T = arguments[2];
        }
      }

      // 10. Let lenValue be Get(items, "length").
      // 11. Let len be ToLength(lenValue).
      var len = toLength(items.length);

      // 13. If IsConstructor(C) is true, then
      // 13. a. Let A be the result of calling the [[Construct]] internal method
      // of C with an argument list containing the single item len.
      // 14. a. Else, Let A be ArrayCreate(len).
      var A = isCallable(C) ? Object(new C(len)) : new Array(len);

      // 16. Let k be 0.
      var k = 0;
      // 17. Repeat, while k < len… (also steps a - h)
      var kValue;
      while (k < len) {
        kValue = items[k];
        if (mapFn) {
          A[k] = typeof T === 'undefined' ? mapFn(kValue, k) : mapFn.call(T, kValue, k);
        } else {
          A[k] = kValue;
        }
        k += 1;
      }
      // 18. Let putStatus be Put(A, "length", len, true).
      A.length = len;
      // 20. Return A.
      return A;
    };
  }());
}
```

## Spezifikationen

| Spezifikation                                                                | Status                       | Kommentar            |
| ---------------------------------------------------------------------------- | ---------------------------- | -------------------- |
| {{SpecName('ES2015', '#sec-array.from', 'Array.from')}}     | {{Spec2('ES2015')}}     | Initiale Definition. |
| {{SpecName('ESDraft', '#sec-array.from', 'Array.from')}} | {{Spec2('ESDraft')}} |                      |

## Browserkompatibilität

{{Compat("javascript.builtins.Array.from")}}

## Siehe auch

- {{jsxref("Array")}}
- {{jsxref("Array.prototype.map()")}}
- {{jsxref("TypedArray.from()")}}
