# JSON und Direktiven

In diesem Kapitel geht es darum, wie wir innerhalb einer Komponente mit TypeScript Daten verwalten und diese Daten im HTML verwenden, um sie entweder anzuzeigen oder die Struktur des HTML-Codes mit diesen Daten zu ändern. Außerdem betrachten wir, wie in TypeScript auf Ereignisse reagieren können, die die Nutzerinnen beim Verwenden der Anwendung auslösen. Um die Verwaltung von Daten zu diskutieren, betrachten wir zunächst, wie Daten in TypeScript/JavaScript notiert werden. 

## JavaScript Object Notation (JSON)

Eine kurze Einführung zu Objekten in JavaScript haben wir bereits im [**JavaScript-Kapitel**](javascript.md#objekte) gegeben. Dort haben wir auch gesagt, dass wir auf die Notation solcher Objekte in JavaScript nochmal genauer eingehen wollen. Dies geschieht hier. *JavaScript Object Notation (JSON)* ist ein Datenaustauschformat, das einerseits einfach für Menschen zu lesen und zu schreiben ist und andererseits gut von Maschinen *geparst* (analysiert) und erzeugt werden kann. Ein Objekt in JSON beginnt mit einer geschweiften Klammer `{` und endet mit `}`. JSON besteht im wesentlichen aus Schlüssel-Werte-Paaren, die durch Komma getrennt sind. 

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
georg.name 		// "Georg"
georg.alter 	// 47
let kinder = georg.kinder; 	// Array aus 2 Objekten
kinder[0].name		// "Lukas"
kinder[1].name 		// "Lisa"
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

Ein Array ist stets numerisch indiziert, d.h. Sie können unter Verwendung des Index die einzelnen Objekte auslesen. 


## Templates (Bindings)

Unter *Templates* werden in Angular Konstrukte verstanden, die direkt in das HTML eingefügt werden. Die HTML-Syntax wird um Angular-Syntax erweitert. Nachfolgend einige Beispiele dafür. 

### {{ Interpolation }}

*Interpolation* ist die einfachste Form des *data binding*. Syntaktisch erkennt man Interpolation an den doppelten geschweiften Klammern `{{ Interpolation }}`. 

=== "lesson.component.ts"
``` javascript linenums="1" hl_lines="11-12"
import { Component } from '@angular/core';

@Component({
  selector: 'app-lesson',
  standalone: true,
  imports: [],
  templateUrl: './lesson.component.html',
  styleUrl: './lesson.component.css'
})
export class LessonComponent {
  headline = 'Hallo';
  name = 'Jörn Freiheit';
}
```

Im obigen Beispiel hat die Komponente `LessonComponent` zwei Eigenschaften (Objektvariablen): `headline` und `name`. Auf diese Eigenschaften können wir mithilfe von *Interpolation* im HTML zugreifen:


=== "lesson.component.html"
``` html
<h1>{{ headline }} {{ name }} !</h1>
```

Es entsteht:
```bash
Hallo Jörn Freiheit !
```

Eine Interpolation kann auch Ausdrücke enthalten, die aufgelöst werden, z.B.

``` html
<p>1 + 2 = {{1 + 2}}.</p>
```

Es entsteht:
```bash
1 + 2 = 3
```

### [ Attributdirektiven ]

Sie können Attribute von HTML-Elementen an Werte von Eigenschaften binden. Angenommen, Sie haben in Ihrer `*.component.ts` eine Eigenschaft `isFormValid`, die entweder `true` oder `false` sein kann, dann können Sie z.B. ein Button disablen bzw. enablen wie folgt:

```html
<button [disabled]="isFormValid">Save</button>
```

Oder falls Sie folgende Deklarationen in Ihrer `*.component.ts` haben:

```js
  fiwLogoURL='https://corporatedesign.htw-berlin.de/files/Presse/Corporate_Design/Piktogramme_Studiengaenge/FB4_FIW.jpg'
  imageWidth = 100
```

können Sie diese im HTML wie folgt verwenden:

```html
  <img [src]="fiwLogoURL" alt="FIW-Logo" [style.width.px]="imageWidth">
```

Ebenso können Sie CSS-Klassen für Elemente definieren:

```js
  buttonClasses = ['btn', 'btn-primary']
```

mit folgender Verwendung:

```html
<button [disabled]="isFormValid" [class]="buttonClasses">Save</button>
```

oder z.B. sogar eine Operator wie folgt:

```js
  sichtbar = false
```

und

```html
<p [style.display]="sichtbar ? 'block' : 'none'">
    dieser Absatz ist sichtbar bzw unsichtbar, je nach Wert von sichtbar
</p>
```

usw. Siehe [hier](https://angular.dev/guide/templates/binding).

### ( EventListener )

Während wir in plain JavaScript die `on...`-Attribute für Events verwendet haben, werden in Angular die Ereignisse in runde Klammern `( )` einfasst, um sie zu behandeln, z.B.

```html
<button (click)="klickMich()">Klick Mich!</button>
```

und

```js
  klickMich(): void {
    console.log('geklickt')
  }
```

Angular kann dabei der Ereignisbehandlung eine Referenz auf das Ereignis übergeben. Dies erfolgt über die Variable `$event`. Damit kann das Ereignis ausgewertet werden, z.B. 

```html
<input type="text" (keyup)="eingabe($event)" />
```

und


```js
  eingabe(event: KeyboardEvent): void {
    console.log(`Folgende Taste wurde geklickt: ${event.key}`);
    if (event.key === 'Enter') {
      console.log('Eingabe war die Enter-Taste.');
    }
  }
```

Für mögliche Vergleiche mit Tastaturwerten siehe [hier](https://developer.mozilla.org/de/docs/Web/API/UI_Events/Keyboard_event_key_values). 

Dieses Prinzip gilt für alle nativen DOM-Ereignisse. Hier ein kurzer Überblick über die wichtigsten (für eine umfangreichere Liste siehe [hier](https://developer.mozilla.org/en-US/docs/Web/Events#Standard_Events) oder [hier](https://www.w3schools.com/jsref/dom_obj_event.asp)):

| Ereignis        | Beschreibung                                       |
|-----------------|----------------------------------------------------|
| `click`         | Mausklick auf das Element                          |
| `change`        | Der Inhalt/Wert eines Elementes hat sich geändert  |
| `mouseover`     | die Maus wird über das Element bewegt              |
| `mouseout`      | die Maus wird vom Element wegbewegt                |
| `keydown`       | eine Taste der Tastatur wird gedrückt              |
| `keyup`         | Loslassen einer Taste                              |
| `load`          | der Browser hat die Seite vollständig geladen      |
| `focus`         | Fokussieren des Elements (z.B. Anklicken)          |
| `blur`          | Verlieren des Fokus (z.B. Klick außerhalb)         |
| `submit`        | Abschicken eines Formulars                         |
| `copy`, `paste` | Kopieren, Einfügen von Text                        |

Alle Events (in TypeScript/Angular) sind vom Typ `Event`. Es gibt noch speziellere Eventtypen, die aber alle auf dem Interface `Event` basieren, z.B. `MouseEvent`, `InputEvent`, `KeyboardEvent`, `UIEvent`, `ClipboardEvent`. Weitere Details siehe [hier](https://developer.mozilla.org/en-US/docs/Web/API/Event).

Die einfache JavaScript-Attributschreibweise (`on...`) kann in Angular nicht verwendet werden, sondern immer nur die *event binding*-Schreibweise von Angular (mit den runden Klammern)!


## Konstrollstrukturen

### Kontrollstruktur `@for`

Man kann mithilfe einer [Direktive](#direktiven) durch ein Array laufen und jedes einzelne Element mithilfe von Interpolation ausgeben. Dazu führen wir eine weitere Objektvariable `wekkdays` ein, die ein Array enthält:


=== "lesson.component.ts"
``` javascript linenums="1" hl_lines="13"
import { Component } from '@angular/core';

@Component({
  selector: 'app-lesson',
  standalone: true,
  imports: [],
  templateUrl: './lesson.component.html',
  styleUrl: './lesson.component.css'
})
export class LessonComponent {
  headline = 'Hallo';
  name = 'Jörn Freiheit';
  weekdays = ['Montag', 'Dienstag', 'Mittwoch', 'Donnerstag', 'Freitag', 'Samstag', 'Sonntag'];
}
```

Im HTML kann die `@for`-Direktive nun wie folgt angewendet werden:


=== "lesson.component.html"
``` html linenums="1" hl_lines="4-6"
<h1>{{ headline }} {{ name }} !</h1>
<p>1 + 2 = {{ 1+2 }}</p>
<ul>
@for (day of weekdays; track $index; let idx = $index) {
    <li>{{ idx+1 }}. Tag der Woche ist {{ day }}</li> 
}
</ul>
```

Es entsteht:
```bash
1. Tag der Woche ist Montag
2. Tag der Woche ist Dienstag
3. Tag der Woche ist Mittwoch
4. Tag der Woche ist Donnerstag
5. Tag der Woche ist Freitag
6. Tag der Woche ist Samstag
7. Tag der Woche ist Sonntag
```

Die `track`-Angabe ist notwendig. Hier steht nur der Index des Arrays zur Verfügung, der getracked werden kann. Wenn Sie ein Array von Objekten zur Verfügung haben, können Sie auch eine Eigenschaft der Objekte tracken. Die Verwendung des Index mithilfe von `let idx = $index` ist hingegen optional. Darin ist `idx` eine Variable, der Sie jeden beliebigen Namen geben können. Sie können diese Angabe z.B. auch noch um `let idx = $index, e = $even` oder `let idx = $index, o = $odd` erweitern und hätten dann einen `boolean`-Wert `e` bzw. `o`, der `true` ist, wenn der Index gerade (ungerade) und sonst `false` ist. Es ist auch möglich, z.B. `let idx = $index, l = $last` bzw. `let idx = $index, f = $first` anzugeben, dann kann geprüft werden, ob es sich um das erste bzw. letzte Element im Array handelt. Sie auch [hier](https://angular.dev/guide/templates/control-flow#repeat-content-with-the-for-block).

Die `@for`-Kontrollstruktur kann noch um einen `@empty`-Block erweitert werden, für den Fall, dass das Array kein Element enthält:

```html
<ul>
@for (day of weekdays; track $index; let idx = $index, f = $first) {
    <li>{{ idx+1 }}. Tag der Woche ist {{ day }}</li> 
} @empty {
    <li>keine Einträge im Datenarray vorhanden</li>
}
</ul>
```

### Kontrollstruktur `@if`

Mit Hilfe der `@if`-Kontrollstruktur kann ein Block angezeigt werden (oder nicht) in Abhängigkeit eines logischen Ausdrucks:

```html
@if(weekdays.length == 7) {
    <p>Alle Einträge vorhanden.</p>
} @else {
    <p>es fehlen Einträge</p>
}
```

Diese Kontrollstruktur kann auch verschachtelt werden (wie auch `@for`):

```html
@if(weekdays.length == 7) {
    <p>Alle Einträge vorhanden.</p>
} @else if(weekdays.length > 0) {
    <p>es fehlen Einträge</p>
} @else {
    <p>es sind gar keine Einträge vorhanden</p> 
}
```

Beachten Sie, dass vor dem zweiten `if` kein `@` steht.


### Kontrollstruktur `@switch`

Wie oben gezeigt, kann die `@switch`-Kontrollstruktur mit der `@if...else`-Struktur nachgebaut werden. Ein typisches Beispiel für die `@switch`-Kontrollstruktur ist das Einbinden der passenden Komponente, z.B.:

```html
@switch (userPermissions) {
  @case ('admin') {
    <app-admin-dashboard />
  }
  @case ('reviewer') {
    <app-reviewer-dashboard />
  }
  @case ('editor') {
    <app-editor-dashboard />
  }
  @default {
    <app-viewer-dashboard />
  }
}
```

## Pipes |

Pipes dienen der Nachbehandlung von Werten in der Ansicht. Genutzt werden Pipes mithilfe von `|`. Ein typisches Beispiel für Pipes ist die Umformung einer Datumsangabe mithilfe von `DatePipe`:

```html
<p>{{ haltbarkeitsdatum | date }}</p>
```

in der dazugehörigen `*.component.ts` muss `DatePipe` importiert werden:

```js linenums="1" hl_lines="1 7 12"
import { DatePipe } from '@angular/common';
import { Component } from '@angular/core';

@Component({
  selector: 'app-lesson',
  standalone: true,
  imports: [DatePipe],
  templateUrl: './lesson.component.html',
  styleUrl: './lesson.component.css'
})
export class LessonComponent {
  haltbarkeitsdatum = '2024-12-24'

}
```

Es erscheint:
```bash
Dec 24, 2024
```

Mit 

```html
<p>{{ haltbarkeitsdatum | date }}</p>
```

erscheint
```bash
24.12.2024
```

Mit `CurrencyPipe` wird ein passendes Währungssymbol eingefügt, `PercentPipe` fügt ein Prozentzeichen dahinter (und rundet) usw. Für verfügbare Pipes in Angular siehe [hier](https://angular.dev/guide/templates/pipes#built-in-pipes).

Eine besondere Bedeutung hat `AsyncPipe`. Darauf kommen wir nochmal bei den Themen [Promises]() und [Observables]() zu sprechen.

### #Elementreferenzen

Über eine *Elementreferenz*, die man im HTML-Code mittels des Rautensymbols definiert, kann in Angular sehr einfach auf das Element zugegriffen werden. Das folgende Beispiel zeigt eine solche *Elementreferenz*:

```html
<input #id type="text" value="Elementreferenz" />
{{ id.value }}
```

In dem Beispiel wurde einem Textfeld die Elementreferenz `id` zugewiesen (kann jeder Name sein), erkennbar an `#id`. Über diese Elementreferenz (den Namen) lässt sich nun direkt auf dieses Element zugreifen. Im obigen Beispiel wird die `value`-Eigenschaft ausgelesen, also der Wert, der in das Textfeld eingegeben wird (oder, wie oben, vordefiniert ist). Beachten Sie jedoch, dass der Wert nicht automatisch angepasst wird, sobald eine Eingabe erfolgt. Dies muss durch ein Ereignis (z.B. `change` oder `input`) getriggert werden. 


---

***der folgende Abschnitt wird noch überarbeitet, hier hat sich in den letzten Angular-Versionen einiges getan***
___


#### Eigene Ereignisse

Für eine Komponente kann ein eigenes - nicht natives - Ereignis definiert werden. Dies geschieht, indem für eine Komponente eine neue Eigenschaft (z.B. `myEvent`) definiert wird und diese vom Typ `EventEmitter` deklariert wird. Mithilfe von Generics kann der Typ des Events angegeben werden, der ausgelöst werden soll - wenn Sie den Typ nicht genau kennen, verwenden Sie `any`. Soll das Ereignis an die Elternkomponente weitergeleitet werden, was meistens der Fall ist, wird der Decorator `@Output()`verwendet. 
Das Auslösen des Events geschieht dann durch die `emit()`-Methode von `EventEmitter`. Hier ein typisches Beispiel (zunächst die Kindkomponente `EventsComponent` - also `events.component.html` und `events.component.ts`):

=== ".html"
    ``` html
    <button (click)="emitMyEvent()">Click here!</button>
    ```
=== ".ts"    
    ``` javascript linenums="1"
    import {Component, EventEmitter, Output} from '@angular/core';

    @Component({
      selector: 'app-events',
      templateUrl: './events.component.html',
      styleUrls: ['./events.component.css']
    })
    export class EventsComponent {
      @Output() myEvent = new EventEmitter<any>();

      emitMyEvent() {
        this.myEvent.emit();
      }

    }
    ``` 

Die `.html`-Datei definiert einen Button mit dem nativen Ereignis `click`. Dieses wird durch die Methode `emitMyEvent()` behandelt. 

In der `.ts`-Datei ist diese Methode definiert (Zeilen 11-13). Darin wird das eigene Event `myEvent` ausgelöst. Dieses Event ist ein Objekt vom Typ `EventEmitter`, typisiert als `any` (beliebiger Typ). Das Auslösen dieses Events wird an die aufrufende Komponente (die Elternkomponente) ausgegeben (Decorator `@Output()`). Deklaration der Eigenschaft und Dekorieren mit `@Output()` in Zeile 9. Das Auslösen des eigenen Events erfolgt durch den Aufruf der Methode `emit()` aus `EventEmitter` (Zeile 12).

In der Elternkomponente kann dieses Ereignis nun empfangen werden (Beispiel einer Elternkomponente `AppComponent` - also `app.component.html` und `app.component.ts`):

=== ".html"
    ``` html
    <app-events (myEvent)="handleEventFromEventsComponent()"></app-events>
    ```
=== ".ts"    
    ``` javascript linenums="1"
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.css']
    })
    export class AppComponent {

      handleEventFromEventsComponent() {
        console.log('myEvent in der Kindkomponente ausgelöst');
      }

    }
    ``` 

In der `AppComponent` (das kann natürlich eine beliebige Komponente sein), wird die `EventsComponent` eingebunden (siehe `<app-events>` im Template der `AppComponent`). Dadurch entsteht die Hierarchie Elternkomponente `AppComponent` --> Kindkomponente `EventsComponent` im DOM. 

Mithilfe von *event binding* wird die Behandlung des Ereignisses `myEvent` an die Methode `handleEventFromEventsComponent()` gebunden. In dieser Methode erfolgt hier einfach nur eine Ausgabe auf die Konsole. 

Interessant ist, dass wir dadurch die Möglichkeit haben, Daten von der Kindkomponente zur Elternkomponente fließen zu lassen. Dazu übergeben wir diese Daten als `payload` des Ereignisses. Dafür typisieren wir `EventEmitter` mit dem Typ, von dem wir Daten übergeben wollen (z.B. `Book` - siehe [Bücher-App](books.md#event-binding)). Die beiden obigen Beispiele sehen dann wie folgt aus (zuerst wieder `EventsComponent`): 

=== ".html"
    ``` html
    <button (click)="emitMyEvent(book)">Click here!</button>
    ```
=== ".ts"    
    ``` javascript linenums="1"
    import {Component, EventEmitter, Output} from '@angular/core';

    @Component({
      selector: 'app-events',
      templateUrl: './events.component.html',
      styleUrls: ['./events.component.css']
    })
    export class EventsComponent {
      @Output() myEvent = new EventEmitter<Book>();

      emitMyEvent(book: Book) {
        this.myEvent.emit(book);
      }

    }
    ``` 

Im Template (HTML) werden die Daten der Ereignisbehandlung übergeben. Das `EventEmitter`-Objekt ist mit dem konkreten Datentyp typisiert. Bei Aufruf der Methode `emit()` werden die Daten an die Elternkomponente übergeben. 

Die Elternkomponente (hier wieder `AppComponent` kann diese Daten, die von der Kindkomponente an die Elternkomponente via Ereignis geflossen sind, nun weiterverarbeiten bzw. darstellen):

=== ".html"
    ``` html
    <app-events (myEvent)="handleEventFromEventsComponent($event)"></app-events>
    ```
=== ".ts"    
    ``` javascript linenums="1"
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.css']
    })
    export class AppComponent {

      handleEventFromEventsComponent(book: Book) {
        console.log(book.title);
      }

    }
    ``` 

Wichtig beim *event binding* der Elternkomponente ist, dass der *payload* des Ereignisses mit `$event` übergeben wird (siehe auch [Native DOM-Ereignisse](#native-dom-ereignisse)). 






