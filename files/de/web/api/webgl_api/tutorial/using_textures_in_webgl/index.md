---
title: Texturen in WebGL verwenden
slug: Web/API/WebGL_API/Tutorial/Using_textures_in_WebGL
tags:
  - Tutorial
  - WebGL
translation_of: Web/API/WebGL_API/Tutorial/Using_textures_in_WebGL
original_slug: Web/API/WebGL_API/Tutorial/Texturen_in_WebGL_verwenden
---
{{WebGLSidebar("Tutorial")}} {{PreviousNext("Web/API/WebGL_API/Tutorial/3D-Objekte_mit_WebGL_erstellen", "Web/API/WebGL_API/Tutorial/Beleuchtung_in_WebGL")}}

Jetzt wo unser Beispielprogramm über einen rotierenden 3D-Würfel verfügt, wollen wir darauf eine Textur legen, statt der bisher verwendeten, einfachen Farben.

## Texturen laden

Als Erstes müssen wir ein paar Zeilen Code hinzufügen, um die Texturen zu laden. In unserem Fall werden wir eine einzige Textur verwenden, die auf alle sechs Seiten des rotierenden Würfels gelegt wird, aber die gleiche Technik kann verwendet werden, um jede beliebig viele Texturen auf ein Objekt zu legen.

Der Code, der die Textur lädt, sieht so aus:

```js
function initTextures() {
  gl.enable(gl.TEXTURE_2D);
  cubeTexture = gl.createTexture();
  cubeImage = new Image();
  cubeImage.onload = function() { handleTextureLoaded(cubeImage, cubeTexture); }
  cubeImage.src = "cubetexture.png";
}

function handleTextureLoaded(image, texture) {
  gl.bindTexture(gl.TEXTURE_2D, texture);
  gl.texImage2D(gl.TEXTURE_2D, 0, image, true);
  gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MAG_FILTER, gl.LINEAR);
  gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MIN_FILTER, gl.LINEAR_MIPMAP_NEAREST);
  gl.generateMipmap(gl.TEXTURE_2D);
  gl.bindTexture(gl.TEXTURE_2D, null);
}
```

Die Routine `initTextures()` aktiviert zunächst die Unterstützung von Texturen, dann wird das GL Textur-Objekt `cubeTexture` durch Aufruf der GL `createTexture()` Funktion erstellt. Um die Textur von der Bilddatei zu laden, wird dann ein `Image`-Objekt erstellt und in die Grafikdatei geladen, die wir als unsere Textur verwenden wollen. Die `handleTextureLoaded()` Callback-Routine wird ausgeführt, wenn das Bild geladen wurde.

Um schließlich die Textur zu erstellen, legen wir fest, dass die neue Textur die aktuelle Textur ist, mit welcher wir arbeiten wollen und verbinden diese mit `gl.TEXTURE_2D`. Danach wird das geladene Bild mit `texImage2D()` die Bilddaten in die Textur schreiben.

Die nächsten zwei Zeilen legen Filter für die Textur fest, die steuern, wie das Bild gefiltert wird, wenn es skaliert wird. In diesem Fall verwenden wir lineare Filter, wenn das Bild hoch skaliert wird und [Mip-Mapping](http://de.wikipedia.org/wiki/Mip_Mapping) wenn wir herunter skalieren. Dann wird die Mip-Map generiert, indem `generateMipMap()` aufgerufen wird. Schließlich teilen wir WebGL mit, dass wir mit der Arbeit an der Textur fertig sind, in dem wir `null` mit `gl.TEXTURE_2D` verknüpfen.

## Textur auf die Flächen legen

Nun ist die Textur geladen und bereit eingesetzt zu werden. Bevor wir die Textur aber verwenden können, müssen wir die Texturkoordinaten auf die Vertices der Flächen des Würfels legen. Das ersetzt den vorherigen Code in `initBuffers()`, der die Farben für jede Fläche festgelegt hat.

```js
  cubeVerticesTextureCoordBuffer = gl.createBuffer();
  gl.bindBuffer(gl.ARRAY_BUFFER, cubeVerticesTextureCoordBuffer);

  var textureCoordinates = [
    // vorne
    0.0,  0.0,
    1.0,  0.0,
    1.0,  1.0,
    0.0,  1.0,
    // hinten
    0.0,  0.0,
    1.0,  0.0,
    1.0,  1.0,
    0.0,  1.0,
    // oben
    0.0,  0.0,
    1.0,  0.0,
    1.0,  1.0,
    0.0,  1.0,
    // unten
    0.0,  0.0,
    1.0,  0.0,
    1.0,  1.0,
    0.0,  1.0,
    // rechts
    0.0,  0.0,
    1.0,  0.0,
    1.0,  1.0,
    0.0,  1.0,
    // links
    0.0,  0.0,
    1.0,  0.0,
    1.0,  1.0,
    0.0,  1.0
  ];

  gl.bufferData(gl.ARRAY_BUFFER, new WebGLFloatArray(textureCoordinates),
                gl.STATIC_DRAW);
```

Zuerst erstellt dieser Code einen GL-Buffer in welchen wir die Texturkoordinaten für jede Fläche speichern werden, dann verknüpfen wir diesen Buffer als das Array in welchen wir schreiben werden.

Das `textureCoordinates` Array definiert die Texturkoordinaten entsprechend jedem Vertex von jeder Fläche. Beachten Sie, dass die Texturkoordinaten sich im Bereich von 0.0 bis 1.0 befinden. Beim Texturmapping werden die Dimensionen von Texturen immer auf einen Bereich von 0.0 bis 1.0 normiert, egal welche Größe die Textur wirklich hat.

Sobald wir das Texturmapping-Array erstellt haben, speichern wir das Array in den Buffer, sodass GL die Daten zur Verfügung hat.

## Die Shader aktualisieren

Das Shader-Programm - und der Code, der die Shader initialisiert - muss aktualisiert werden, damit die Textur anstatt der Farben verwendet wird.

Werfen wir zunächst einen Blick auf die einfache Änderung, die in `initShaders()` benötigt wird:

```js
  textureCoordAttribute = gl.getAttribLocation(shaderProgram, "aTextureCoord");
  gl.enableVertexAttribArray(textureCoordAttribute);
```

Das ersetzt den Code, der die Vertex Farbattribute enthielt, mit dem, der nun die Texturkoordinaten für jeden Vertex enthält.

### Der Vertex-Shader

Als Nächstes müssen wir den Vertex-Shader ersetzen, sodass statt der Farbdaten die Texturkoordinaten abgerufen werden.

```html
    <script id="shader-vs" type="x-shader/x-vertex">
      attribute vec3 aVertexPosition;
      attribute vec2 aTextureCoord;

      uniform mat4 uMVMatrix;
      uniform mat4 uPMatrix;

      varying vec2 vTextureCoord;

      void main(void) {
        gl_Position = uPMatrix * uMVMatrix * vec4(aVertexPosition, 1.0);
        vTextureCoord = aTextureCoord;
      }
    </script>
```

Die wichtigste Änderung ist hier, dass anstatt die Vertex-Farbe abzurufen, die Texturkoordinaten gesetzt werden. Das gibt den Ort der Textur entsprechend zum Vertex an.

### Der Fragment-Shader

Der Fragment-Shader muss in ähnlicher Weise geändert werden:

```html
    <script id="shader-fs" type="x-shader/x-fragment">
      varying vec2 vTextureCoord;

      uniform sampler2D uSampler;

      void main(void) {
        gl_FragColor = texture2D(uSampler, vec2(vTextureCoord.s, vTextureCoord.t));
      }
    </script>
```

Anstatt einen Farbwert auf die Fragment-Farbe zu legen, wird die Fragment-Farbe berechnet in dem der **texel** (der Pixel innerhalb der Textur) abgerufen wird, der am Besten auf die Fragement-Position laut dem Sampler passt.

## Zeichnen des textuierten Würfels

Die Änderungen an der `drawScene()` Funktion sind einfach (mit der Ausnahme, dass ich nun zur besseren Anschaulichkeit die Verschiebungen entfernt habe und der Würfel nur noch rotiert wird).

Der Code, der die Farben auf die Textur legt ist weg und wurde ersetzt:

```js
  gl.activeTexture(gl.TEXTURE0);
  gl.bindTexture(gl.TEXTURE_2D, cubeTexture);
  gl.uniform1i(gl.getUniformLocation(shaderProgram, "uSampler"), 0);
```

GL ermöglicht 32 Textur-Register; der Erste davon ist `gl.TEXTURE0`. Wir verknüpfen unsere geladene Textur zu diesem Register, dann wird der Shader-Sampler `uSampler` gesetzt (im Shader-Program festgelegt), um die Textur zu benutzen.

Jetzt sollte der rotierende Würfel gut anzuschauen zu sein. Wenn Ihr Browser WebGL unterstützt, können Sie [das Live-Beispiel ausprobieren](/samples/webgl/sample6/index.html "https://developer.mozilla.org/samples/webgl/sample6/index.html").

{{PreviousNext("Web/API/WebGL_API/Tutorial/3D-Objekte_mit_WebGL_erstellen", "Web/API/WebGL_API/Tutorial/Beleuchtung_in_WebGL")}}
