---
title: 3D-Objekte mit WebGL erstellen
slug: Web/API/WebGL_API/Tutorial/Creating_3D_objects_using_WebGL
tags:
  - Tutorial
  - WebGL
translation_of: Web/API/WebGL_API/Tutorial/Creating_3D_objects_using_WebGL
original_slug: Web/API/WebGL_API/Tutorial/3D-Objekte_mit_WebGL_erstellen
---
{{WebGLSidebar("Tutorial")}} {{PreviousNext("Web/API/WebGL_API/Tutorial/Objekte_mit_WebGL_animieren", "Web/API/WebGL_API/Tutorial/Texturen_in_WebGL_verwenden")}}

Bringen wir unser Quadrat in die dritte Dimension, indem wir fünf oder mehr Flächen hinzufügen und daraus einen Würfel machen. Um das effizient zu machen, wechseln wir vom Zeichnen direkt über die Vertices zur `gl.drawArray()` Methode, um den Vertex-Array als eine Tabelle zu verwenden und die einzelnen Vertices in dieser Tabelle als Referenz für Positionen jeder Fläche zu definieren, indem wir `gl.drawElements()` aufrufen.

Bedenken Sie: Jede Fläche benötigt vier Vertices, die diese definieren, aber jeder Vertex wird von drei Flächen verwendet. Wir können eine Menge Daten sparen, indem wir eine Liste aller 24 Vertices erstellen und uns dann auf jeden Vertex durch dessen Index in der Liste beziehen, anstatt den gesamten Koordinatensatz zu verwenden.

## Die Vertex-Positionen des Würfels definieren

Zunächst wollen wir den Positionsspeicher der Vertices erstellen, indem wir den Code in `initBuffers()` ändern. Das geschieht genau so wie für das Quadrat, allerdings haben wir hier ein paar Datensätze mehr, da wir 24 Vertices (4 pro Seite) haben müssen:

```js
  var vertices = [
    // vordere Fläche
    -1.0, -1.0,  1.0,
     1.0, -1.0,  1.0,
     1.0,  1.0,  1.0,
    -1.0,  1.0,  1.0,

    // hintere Fläche
    -1.0, -1.0, -1.0,
    -1.0,  1.0, -1.0,
     1.0,  1.0, -1.0,
     1.0, -1.0, -1.0,

    // obere Fläche
    -1.0,  1.0, -1.0,
    -1.0,  1.0,  1.0,
     1.0,  1.0,  1.0,
     1.0,  1.0, -1.0,

    // untere Fläche
    -1.0, -1.0, -1.0,
     1.0, -1.0, -1.0,
     1.0, -1.0,  1.0,
    -1.0, -1.0,  1.0,

    // rechte Fläche
     1.0, -1.0, -1.0,
     1.0,  1.0, -1.0,
     1.0,  1.0,  1.0,
     1.0, -1.0,  1.0,

    // linke Fläche
    -1.0, -1.0, -1.0,
    -1.0, -1.0,  1.0,
    -1.0,  1.0,  1.0,
    -1.0,  1.0, -1.0
  ];
```

## Die Farben der Vertices definieren

Außerdem müssen wir einen Array für die Farben der 24 Vertices erstellen. Dieser Code definiert zunächst die Farben für jede Fläche und verwendet dann eine Schleife, um jeden der Vertices mit einer Farbe zu bestücken.

```js
  var colors = [
    [1.0,  1.0,  1.0,  1.0],    // vordere Fläche: weiß
    [1.0,  0.0,  0.0,  1.0],    // hintere Fläche: rot
    [0.0,  1.0,  0.0,  1.0],    // obere Fläche: grün
    [0.0,  0.0,  1.0,  1.0],    // untere Fläche: blau
    [1.0,  1.0,  0.0,  1.0],    // rechte Fläche: gelb
    [1.0,  0.0,  1.0,  1.0]     // linke Fläche: violett
  ];

  var generatedColors = [];

  for (j=0; j<6; j++) {
    var c = colors[j];

    for (var i=0; i<4; i++) {
      generatedColors = generatedColors.concat(c);
    }
  }

  cubeVerticesColorBuffer = gl.createBuffer();
  gl.bindBuffer(gl.ARRAY_BUFFER, cubeVerticesColorBuffer);
  gl.bufferData(gl.ARRAY_BUFFER, new WebGLFloatArray(generatedColors), gl.STATIC_DRAW);
```

## Das Element-Array definieren

Sobald die Vertex-Arrays generiert worden sind, müssen wir das Element-Array erstellen.

```js
  cubeVerticesIndexBuffer = gl.createBuffer();
  gl.bindBuffer(gl.ELEMENT_ARRAY_BUFFER, cubeVerticesIndexBuffer);

  // Dieser Array definiert jede Fläche als zwei Dreiecke über die Indizes
  // im Vertex-Array, um die Position jedes Dreiecks festzulegen.

  var cubeVertexIndices = [
    0,  1,  2,      0,  2,  3,    // vorne
    4,  5,  6,      4,  6,  7,    // hinten
    8,  9,  10,     8,  10, 11,   // oben
    12, 13, 14,     12, 14, 15,   // unten
    16, 17, 18,     16, 18, 19,   // rechts
    20, 21, 22,     20, 22, 23    // links
  ]

  // Sende nun das Element-Array zum GL

  gl.bufferData(gl.ELEMENT_ARRAY_BUFFER,
      new WebGLUnsignedShortArray(cubeVertexIndices), gl.STATIC_DRAW);
```

Das `cubeVertexIndices` Array definiert jede Fläche als ein paar von Dreiecken, alle Vertices des Dreiecks werden als ein Index im Vertex-Array des Würfels festgelegt. Daher ist der Würfel aus einer Sammlung von 12 Dreiecken beschrieben.

## Den Würfel zeichnen

Als nächstes müssen wir etwas Code zur `drawScene()` Funktion hinzufügen, um über den Indexspeicher des Würfels zu zeichnen. Wir fügen neue `bindBuffer()` und `drawElements()` Aufrufe hinzu:

```js
  gl.bindBuffer(gl.ELEMENT_ARRAY_BUFFER, cubeVerticesIndexBuffer);
  setMatrixUniforms();
  gl.drawElements(gl.TRIANGLES, 36, gl.UNSIGNED_SHORT, 0);
```

Da jede Seite unseres Würfels aus zwei Dreiecken besteht, gibt es 6 Vertices pro Seite, oder 36 Vertices im Würfel, obwohl einige davon doppelt sind. Da unser Index-Array jedoch aus einfachen Integern besteht, stellt dies keinen unkoordinierbaren Betrag an Daten dar, welcher für jeden Frame der Animation durchgegangen werden muss.

Jetzt haben wir einen animierten Würfel, welcher herum springt, rotiert und über sechs unterschiedliche Seiten verfügt. Wenn Ihr Browser WebGL unterstützt, [schauen Sie sich hier die Demo in Aktion an](/samples/webgl/sample5/index.html "https://developer.mozilla.org/samples/webgl/sample5/index.html").

{{PreviousNext("Web/API/WebGL_API/Tutorial/Objekte_mit_WebGL_animieren", "Web/API/WebGL_API/Tutorial/Texturen_in_WebGL_verwenden")}}
