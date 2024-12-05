# Templates (Bindings)

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

### [ Attributbindings ]

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

Kontrollstrukturen zählen zu den *templates*. Auch diese werden in den HTML-Code eingefügt und bewirken entweder eine iterative (`@for`) oder eine selektive (`@if` bzw. `@switch`) Abarbeitung des HTML-Codes.

### Kontrollstruktur `@for`

Man kann mithilfe einer *Kontrollstruktur* `@for` durch ein Array laufen und jedes einzelne Element mithilfe von Interpolation ausgeben. Dazu führen wir eine weitere Objektvariable `wekkdays` ein, die ein Array enthält:


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






