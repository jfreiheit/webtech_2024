# Objekte

Objekte in JavaScript werden in *JavaScript Object Notation* beschrieben. Wir werden darauf in [JavaScript Object Notation (JSON)](#javascript-object-notation-json) genauer eingehen, zeigen zunächst aber ein einfaches Beispiel eines JavaScript-Objektes zur Einführung:

```javascript
let person={vorname:"Maria", nachname: "Musterfrau"};
```

Es wurde ein Objekt `person` definiert mit 2 Feldern `vorname` und `nachname` und diesen Feldern wurden Werte zugewiesen. Der Zugriff auf die Felder erfolgt mittels Punkt-Notation, also `person.vorname` und `person.nachname`. 

- Sie können die Werte auch einfach überschreiben, z.B. `person.nachname = "Schmidt"`. 
- Sie können das Objekt auch um weitere Eigenschaften erweitern, z.B. `person.alter = 42`.

Neben der üblichen Punktnotation ist auch zu erwähnen, dass die Eigenschaften auch Schlüssel eines assoziativen Arrays sind, d.h. Sie können auf die Werte auch wie folgt zugreifen:

```javascript
person["vorname"]       // Maria
person["nachname"]      // Schmidt
person["alter"]         // 42
``` 

Mithilfe von `delete` können Eigenschaften gelöscht werden, z.B. `delete person.alter;`. Ab dann ist `person.alter` `undefined`. 

Objekteigenschaften können auch Funktionen sein, z.B. 

```javascript
person.name=function(){ return this.vorname + " " + this.nachname };
```

Der Aufruf erfolgt dann über `person.name();`


### Ein Beispiel mit einem JavaScript-Objekt

Wir betrachten folgendes JavaScript-Objekt, mit dem wir eine Farbe im [HSL-Format](https://www.w3schools.com/colors/colors_hsl.asp) repräsentieren:

```js
colorHSL = {
    hue:  50,
    saturation: 50,
    lightness: 50,
    name: () => `hsl(${colorHSL.hue} , ${colorHSL.saturation}%, ${colorHSL.lightness}%)`
}
```

Beachten Sie, dass ein JavaScript-Objekt (im Gegensatz zu einem Objekt im JSON-Format) auch Funktionen als Eigenschaften besitzen kann, siehe Eigenschaft `name` im Objekt `colorHSL`. Zur Verwendung dieses Objektes erstellen wir uns zunächst folgendes HTML:

```html linenums="1"
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-rbsA2VBKQhggwzxH7pPCaAqO46MgnOM80zW1RWuH61DGLwZJEdK2Kadq2F9CUG65" crossorigin="anonymous">
    <title>Javascript</title>
    <style>
        div#output {
            height: 300px;
        }
    </style>
</head>
<body class="container" onload="setBackgroundColorDiv()">
    
    <h1>JavaScript-Objekte</h1>
    <div id="output">

    </div>
    <div class="my-3">
        <div class="row">
            <div class="col-2">
                <label for="hueIP" class="form-label">Hue (Farbton)</label>
            </div>
            <div class="col-2">
                <input type="text" class="form-range" id="hueOP" value="50">
            </div>
            <div class="col-8">
                <input type="range" class="form-range" min="0" max="360" id="hueIP" oninput="newHue()" value="50">
            </div>
        </div>
        <div class="row">
            <div class="col-2">
                <label for="satIP" class="form-label">Saturation (Sättigung)</label>
            </div>
            <div class="col-2">
                <input type="text" class="form-range" id="satOP" value="50">
            </div>
            <div class="col-8">
                <input type="range" class="form-range" min="0" max="100" id="satIP" oninput="newSat()" value="50">
            </div>
        </div>
        <div class="row">
            <div class="col-2">
                <label for="lightIP" class="form-label">Lightness (Helligkeit)</label>
            </div>
            <div class="col-2">
                <input type="text" class="form-range" id="lightOP" value="50">
            </div>
            <div class="col-8">
                <input type="range" class="form-range" min="0" max="100" id="lightIP" oninput="newLight()" value="50">
            </div>
        </div>
    </div>
</body>
</html>
```

Das ergibt folgendes Aussehen:

![Object](./files/263_javascript.png)

Für die `<input type="range"`-Felder wird das `input`-Event behandelt. Für jeden Slider wird eine eigene Funktion aufgerufen, das hätte man aber auch alles in einer Funktion erledigen können. Hier der JavaScript-Code, der per `<script>`-Element eingebunden wird:

```js linenums="1"
    let colorHSL = {};

    function setBackgroundColorDiv() {
        colorHSL = {
            hue:  50,
            saturation: 50,
            lightness: 50,
            name: () => `hsl(${colorHSL.hue} , ${colorHSL.saturation}%, ${colorHSL.lightness}%)`
        }
        let outputDiv = document.querySelector('#output');
        outputDiv.style.backgroundColor = colorHSL.name();
        console.log(colorHSL.name());
    }

    function newHue() {
        let sliderValue = document.querySelector('#hueIP').value;
        colorHSL.hue = sliderValue;
        document.querySelector('#hueOP').value = sliderValue;
        document.querySelector('#output').style.backgroundColor = colorHSL.name();
        console.log(colorHSL.name())
    }

    function newSat() {
        let sliderValue = document.querySelector('#satIP').value;
        colorHSL.saturation = sliderValue;
        document.querySelector('#satOP').value = sliderValue;
        document.querySelector('#output').style.backgroundColor = colorHSL.name();
        console.log(colorHSL.name())
    }

    function newLight() {
        let sliderValue = document.querySelector('#lightIP').value;
        colorHSL.lightness = sliderValue;
        document.querySelector('#lightOP').value = sliderValue;
        document.querySelector('#output').style.backgroundColor = colorHSL.name();
        console.log(colorHSL.name())
    }
```

Die Funktion `setBackgroundColorDiv()` definiert zunächst die Eigenschaften des JavaScript-Objektes `colorHSL`. Die Variable ist global definiert, damit alle Funktionen auf diese Variable Zugriff haben. Die Funktion `setBackgroundColorDiv()` wird durch das `load`-Event aufgerufen (siehe Zeile `15` im HTML-Code). Die Funktion `name` im `colorHSL`-Objekt gibt den CSS-Wert der Farbe als String zurück. Beachten Sie die Verwendung der `back ticks` für den String. Diese Erlauben die [Interpolation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals?retiredLocale=de) unter Verwendung des `${}`-Operators.

Die drei Funktionen `newXXX` hätten auch durch eine ersetzt werden können:

```js linenums="1"
    function newValues() {
        let sliderValueH = document.querySelector('#hueIP').value;
        let sliderValueS = document.querySelector('#satIP').value;
        let sliderValueL = document.querySelector('#lightIP').value;

        colorHSL.hue = sliderValueH;
        colorHSL.saturation = sliderValueS;
        colorHSL.lightness = sliderValueL;

        document.querySelector('#hueOP').value = sliderValueH;
        document.querySelector('#satOP').value = sliderValueS;
        document.querySelector('#lightOP').value = sliderValueL;

        document.querySelector('#output').style.backgroundColor = colorHSL.name();
        console.log(colorHSL.name())
    }
```

!!! hint "Objektausgabe auf Konsole"
    Angenommen, Sie wollen ein Objekt auf die Konsole ausgeben und zuvor noch eine eigene Ausgabe. Verwenden Sie dann nicht den Zeichenkettenverbindungsoperator `+`, also nicht z.B. `console.log('colorHSL' + colorHSL);`. Das führt nur dazu, dass für das Objekt `toString()` aufgerufen wird und das ergibt dann `colorHSL[object Object]`. Verwenden Sie stattdessen ein Komma, z.B. `console.log('colorHSL', colorHSL);`. Das ergibt dann das Gewünschte: `colorHSL {hue: 50, saturation: 50, lightness: 50, name: ƒ}`. 

#### JSON.parse() und JSON.stringify()

Mithilfe von [JSON.stringify()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON) können Sie ein JavaScript-Objekt in das JSON-Format überführen. Beachten Sie, dass Funktionen im JSON-Format nicht erlaubt sind. Aus obigem `colorHSL`-Objekt würde mithilfe von `JSON.stringify(colorHSL)` folgendes JSON erzeugt werden:

```json
{
    "hue":50,
    "saturation":50,
    "lightness":50
}
```

Mithilfe von `JSON.parse()` erzeugen Sie aus einem JSON ein JavaScript-Objekt. Beachten Sie, dass `let newColorHSL = JSON.parse(JSON.stringify(colorHSL))` ein JavaScript-Objekt ohne die Funktion `name` erzeugt:

```js
{
    hue: 50, 
    saturation: 50, 
    lightness: 50
}
```


## JavaScript Object Notation (JSON)

Eine kurze Einführung zu Objekten in JavaScript haben wir bereits oben gegeben. Dort haben wir auch gesagt, dass wir auf die Notation solcher Objekte in JavaScript nochmal genauer eingehen wollen. Dies geschieht hier. *JavaScript Object Notation (JSON)* ist ein Datenaustauschformat, das einerseits einfach für Menschen zu lesen und zu schreiben ist und andererseits gut von Maschinen *geparst* (analysiert) und erzeugt werden kann. Ein Objekt in JSON beginnt mit einer geschweiften Klammer `{` und endet mit `}`. JSON besteht im wesentlichen aus Schlüssel-Werte-Paaren, die durch Komma getrennt sind. 

```bash
{
    "schlüssel1": wert1,
    "schlüssel2": wert2,
}
```

Die *Schlüssel* sind Strings in doppelten Hochkamma (`""`), dann folgt ein Doppelpunkt `:` und dann folgt der Wert. *Werte* können Strings, Zahlen, Wahrheitswerte, Arrays und Objekte (und `null`) sein. 

Hier ein Beispiel (erweitert [**aus**](https://wiki.selfhtml.org/wiki/JSON)):

```json linenums="1"
{
  "name": "Georg",
  "alter": 47,
  "verheiratet": false,
  "beruf": null,
  "kinder": [
    {
      "name": "Lukas",
      "alter": 19,
      "schulabschluss": "Gymnasium"
    },
    {
      "name": "Lisa",
      "alter": 14,
      "schulabschluss": null
    }
  ]
}
```

- Der Wert zum Schlüssel `"name"` in Zeile `2` ist ein String (`string`). 
- Der Wert zum Schlüssel `"alter"` in Zeile `3` ist eine Zahl (`number`). 
- Der Wert zum Schlüssel `"verheiratet"` in Zeile `4` ist ein Wahrheitswert (`boolean`). 
- Der Wert zum Schlüssel `"kinder"` in Zeilen `6-17` ist Array. 
- Die Elemente in diesem Array sind selbst wieder Objekte in JavaScript Object Notation, bestehend aus jeweils drei Schlüssel-Werte-Paaren.
- Das `"kinder"`ist numerisch indiziert, d.h. wir können über den Index `0` auf das erste Kind (`"Lukas"`) und über den Index `1` auf das zweite Kind (`"Lisa"`) zugreifen

### Zugriff auf ein JSON

Der Zugriff auf die Werte eines JSON erfolgt mittels Punktnotation über den Schlüssel. Wir nehmen obiges Beispiel und speichern es in einer Variablen `georg`:

```javascript linenums="1"
let georg = {
              "name": "Georg",
              "alter": 47,
              "verheiratet": false,
              "beruf": null,
              "kinder": [
                {
                  "name": "Lukas",
                  "alter": 19,
                  "schulabschluss": "Gymnasium"
                },
                {
                  "name": "Lisa",
                  "alter": 14,
                  "schulabschluss": null
                }
              ]
            }
```

Dann können wir auf die einzelnen Werte wie folgt zugreifen:

```javascript
georg.name      // "Georg"
georg.alter     // 47
let kinder = georg.kinder;  // Array aus 2 Objekten
kinder[0].name      // "Lukas"
kinder[1].name      // "Lisa"
```

Man kann übrigens auch anstelle der Punktnotation ein JSON wie ein assoziatives Array auffassen und z.B. anstelle von `georg.name` über `georg['name']` auf den Wert `"Georg"` zugreifen. 

Es wäre auch möglich, das "Kinder"-Array in ein weiteres JSON umzuwandeln:

```javascript linenums="1" hl_lines="2 3 8 13 15 16 21 26"
// anstelle von:
  "kinder": [
    {
      "name": "Lukas",
      "alter": 19,
      "schulabschluss": "Gymnasium"
    },
    {
      "name": "Lisa",
      "alter": 14,
      "schulabschluss": null
    }
  ],
// ginge z.B. auch:
  "kinder": {
    "erstesKind" : {
      "name": "Lukas",
      "alter": 19,
      "schulabschluss": "Gymnasium"
    },
    "zweitesKind" : {
      "name": "Lisa",
      "alter": 14,
      "schulabschluss": null
    }
  },
```

Dann ist der Zugriff über den Index (also z.B. `georg.kinder[0]`) nicht mehr möglich. Stattdessen aber:

```javascript
georg.kinder.erstesKind.name
georg.kinder.zweitesKind.alter
```

### JSON.parse() und JSON.stringify()

Um JavaScript-Objekte nach JSON zu konvertieren, steht die JavaScript-Funktion `JSON.stringify()` zur Verfügung. Um aus einem JSON ein JavaScript-Objekt zu machen, wird `JSON.parse()` angewendet. Bei der Konvertierung von einem Objekt nach JSON gelten zwei einfache Regeln:

- in JavaScript-Objekten sind die Schlüssel nicht als Strings in `""` eingefasst, in JSON aber doch
- in JavaScript-Objekten können die Werte auch Funktionen sein, in JSON nicht

Angenommen, wir haben folgendes JavaScript-Objekt (im Unterschied zu oben, kann in Objekten eine Eigenschaft auch eine Funktion als Wert besitzen):

```js
let georgObj = {
  name: "Georg",
  alter: 47,
  verheiratet: false,
  beruf: null,
  kinder: [
    {
      name: "Lukas",
      alter: 19,
      schulabschluss: "Gymnasium"
    },
    {
      name: "Lisa",
      alter: 14,
      schulabschluss: null
    }
  ],
  biografie: function() {
            return this.name + " ist " + this.alter + " und hat " + this.kinder.length + " Kinder.";
  },
}
```
Wir könnten z.B. aufrufen:
```js
console.log(georgObj.kinder[1].name)
console.log(georgObj.biografie())
```
und bekämen die Ausgaben:
```bash
Lisa
Georg ist 47 und hat 2 Kinder.
```

Wir können dieses Objekt nun mithilfe von `JSON.stringify()` in ein JSON umwandeln:
```js
let georgJSON = JSON.stringify(georgObj)
```

Das JSON sieht dann wie folgt aus:
```json
{
  "name":"Georg",
  "alter":47,
  "verheiratet":false,
  "beruf":null,
  "kinder":[
    {
      "name":"Lukas",
      "alter":19,
      "schulabschluss":"Gymnasium"
    },
    {
      "name":"Lisa",
      "alter":14,
      "schulabschluss":null
    }
  ]
}
```

Alle Schlüssel sind in `""` eingefasst und die Funktion `biografie` wurde entfernt.

Wandeln wir dieses JSON wieder mithilfe von `JSON.parse()` zurück in ein Objekt
```js
let georgObjFromJSON = JSON.parse(georgJSON)
```

erhalten wir
```js
{
  name: "Georg",
  alter: 47,
  verheiratet: false,
  beruf: null,
  kinder: [
    {
      name: "Lukas",
      alter: 19,
      schulabschluss: "Gymnasium"
    },
    {
      name: "Lisa",
      alter: 14,
      schulabschluss: null
    }
  ]
}
```

wobei das `kinder`-Array ebenfalls numerisch indiziert ist (Index `0` und `1`). Das gilt auch für das JSON.


### Optionale Verkettung

Der `?`-Operator wird verwendet, wenn nicht sicher ist, ob eine Eigenschaft existiert bzw. ob ein Wert für die Eigenschaft gesetzt ist. Betrachten wir folgendes Beispiel:

```js linenums="1"
let person = {
    vorname : "Maria",
    nachname: "Musterfrau",
    adresse : {
        strasse : "Wilhelminenhofstr.",
        nummer: 75,
        ort: "Berlin",
        plz: 12459
    }
}
```

Dann kann der `?`-Operator z.B. so verwendet werden:

```js linenums="1"
person.adresse?.ort
```

Die Idee dahinter ist, dass auf die Eigenschaft zugegriffen werden kann, wenn sie existiert und wenn sie einen Wert besitzt. Dieser Operator vermeidet Laufzeitfehler bzw. eine Abfrage auf Existenz.  

### Viele Objekte im Array

Wenn Sie viele "gleiche" Objekte speichern, dann in einem Array. Die folgende Datei zeigt viele Objekte in JSON, die in einem Array abgelegt sind:

??? "data/members.json"
    ```json
    {
      "members": [
        {
          "forename": "Catherine",
          "surname": "Williams",
          "email": "cwilliamsl@360.cn"
        },
        {
          "forename": "Adam",
          "surname": "Anderson",
          "email": "aanderson8@google.fr"
        },
        {
          "forename": "Susan",
          "surname": "Andrews",
          "email": "sandrewsn@google.co.jp"
        },
        {
          "forename": "Catherine",
          "surname": "Andrews",
          "email": "candrewsp@noaa.gov"
        },
        {
          "forename": "Alan",
          "surname": "Bradley",
          "email": "abradley1c@globo.com"
        },
        {
          "forename": "Anne",
          "surname": "Brooks",
          "email": "abrooks16@bravesites.com"
        },
        {
          "forename": "Russell",
          "surname": "Brown",
          "email": "rbrownq@nifty.com"
        },
        {
          "forename": "Ryan",
          "surname": "Burton",
          "email": "rburton18@foxnews.com"
        },
        {
          "forename": "Roy",
          "surname": "Campbell",
          "email": "rcampbell1@geocities.com"
        },
        {
          "forename": "Russell",
          "surname": "Campbell",
          "email": "rcampbell17@eventbrite.com"
        },
        {
          "forename": "Bonnie",
          "surname": "Coleman",
          "email": "bcoleman11@fc2.com"
        },
        {
          "forename": "Ernest",
          "surname": "Coleman",
          "email": "ecoleman15@businessweek.com"
        },
        {
          "forename": "Richard",
          "surname": "Cruz",
          "email": "rcruz7@unc.edu"
        },
        {
          "forename": "Sean",
          "surname": "Cruz",
          "email": "scruz10@answers.com"
        },
        {
          "forename": "Rebecca",
          "surname": "Cunningham",
          "email": "rcunninghamd@mac.com"
        },
        {
          "forename": "Margaret",
          "surname": "Evans",
          "email": "mevansh@pcworld.com"
        },
        {
          "forename": "Jeffrey",
          "surname": "Ford",
          "email": "jford14@cnet.com"
        },
        {
          "forename": "Andrea",
          "surname": "Gardner",
          "email": "agardnerv@woothemes.com"
        },
        {
          "forename": "Deborah",
          "surname": "George",
          "email": "dgeorge6@furl.net"
        },
        {
          "forename": "Sean",
          "surname": "Gibson",
          "email": "sgibsony@alexa.com"
        },
        {
          "forename": "Virginia",
          "surname": "Graham",
          "email": "vgrahamk@aol.com"
        },
        {
          "forename": "Steven",
          "surname": "Hamilton",
          "email": "shamiltonu@state.tx.us"
        },
        {
          "forename": "Virginia",
          "surname": "Hawkins",
          "email": "vhawkinsf@ehow.com"
        },
        {
          "forename": "Edward",
          "surname": "Hicks",
          "email": "ehicksc@pcworld.com"
        },
        {
          "forename": "Mark",
          "surname": "Johnson",
          "email": "mjohnsonj@hostgator.com"
        },
        {
          "forename": "Ruth",
          "surname": "Jordan",
          "email": "rjordan1a@smugmug.com"
        },
        {
          "forename": "Antonio",
          "surname": "Kim",
          "email": "akim4@odnoklassniki.ru"
        },
        {
          "forename": "Jennifer",
          "surname": "Marshall",
          "email": "jmarshallt@gnu.org"
        },
        {
          "forename": "Eric",
          "surname": "Matthews",
          "email": "ematthews5@independent.co.uk"
        },
        {
          "forename": "Raymond",
          "surname": "Mcdonald",
          "email": "rmcdonald2@ihg.com"
        },
        {
          "forename": "Eric",
          "surname": "Miller",
          "email": "emillere@creativecommons.org"
        },
        {
          "forename": "Jonathan",
          "surname": "Morales",
          "email": "jmoralesa@ovh.net"
        },
        {
          "forename": "Marie",
          "surname": "Morgan",
          "email": "mmorganb@cloudflare.com"
        },
        {
          "forename": "Amanda",
          "surname": "Nelson",
          "email": "anelson13@indiatimes.com"
        },
        {
          "forename": "Lisa",
          "surname": "Olson",
          "email": "lolsonr@telegraph.co.uk"
        },
        {
          "forename": "Alice",
          "surname": "Ortiz",
          "email": "aortizw@histats.com"
        },
        {
          "forename": "Peter",
          "surname": "Phillips",
          "email": "pphillipss@1688.com"
        },
        {
          "forename": "Matthew",
          "surname": "Porter",
          "email": "mporter9@europa.eu"
        },
        {
          "forename": "Tammy",
          "surname": "Ray",
          "email": "trayx@weather.com"
        },
        {
          "forename": "Mark",
          "surname": "Richardson",
          "email": "mrichardson1d@ihg.com"
        },
        {
          "forename": "Joan",
          "surname": "Roberts",
          "email": "jroberts12@alibaba.com"
        },
        {
          "forename": "Kathleen",
          "surname": "Rose",
          "email": "kroseg@pinterest.com"
        },
        {
          "forename": "Steve",
          "surname": "Sanders",
          "email": "ssanders1b@wikispaces.com"
        },
        {
          "forename": "Shirley",
          "surname": "Scott",
          "email": "sscottm@macromedia.com"
        },
        {
          "forename": "Lillian",
          "surname": "Stephens",
          "email": "lstephens19@hugedomains.com"
        },
        {
          "forename": "Nicole",
          "surname": "Thompson",
          "email": "nthompson3@admin.ch"
        },
        {
          "forename": "Marie",
          "surname": "Thompson",
          "email": "mthompsonz@yelp.com"
        },
        {
          "forename": "Alan",
          "surname": "Vasquez",
          "email": "avasquezo@miibeian.gov.cn"
        },
        {
          "forename": "Mildred",
          "surname": "Watkins",
          "email": "mwatkins0@miibeian.gov.cn"
        },
        {
          "forename": "Eugene",
          "surname": "Williams",
          "email": "ewilliamsi@deliciousdays.com"
        }
      ]
    }
    ```

Ein Array ist stets numerisch indiziert, d.h. Sie können unter Verwendung des Index die einzelnen Objekte auslesen, also z.B. `members[1]` ist

```js
{
  "forename": "Adam",
  "surname": "Anderson",
  "email": "aanderson8@google.fr"
}
```

 


