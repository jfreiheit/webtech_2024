# Routing und Services


## Single- vs. Multi-Page-Applikationen

Wenn wir durch z.B. dieses Skript hangeln oder Wikipedia, dann stellen wir fest, dass sich nach jedem Klick auf einen Link eine neue HTML-Seite öffnet. Das wird insbesondere deutlich wenn die Entwicklungstools geöffnet sind. Jeder Klick auf einen Hyperlink erwirkt eine neue Anfrage an einen Webserver mit dem Request, eine neue HTML-Seite von diesem Webserver zu laden und im Browser zu öffnen. Es handelt sich dabei also um eine Webanwendung mit vielen (Unter-)Seiten, eine sogenannte *Multi-Page-Applikation (MPA)*. 

Wenn wir stattdessen z.B. die Angular-Seite `https://angular.dev` öffnen und uns die Developertools anschauen, dann stellen wir fest, dass kaum HTML-Code im `<body>`-Element enthalten ist. Stattdessen wird der gesamte HTML-Code per JavaScript im Browser eingebunden. Damit werden Inhalte in die Seite immer genau dann eingebunden, wenn sie angezeigt werden sollen. Um zwischen einzelnen Ansichten der Webanwendung zu wechseln, wird keine neue Webseite vom Webserver geholt. Stattdessen bleiben wir stets in derselben HTML-Seite (*Single-Page-Applikation (SPA)*), was sehr gut sichtbar wird, wenn wir die Developertools eingeschaltet lassen und innerhalb der Webanwendung umhernavigieren. Stattdessen werden nur Inhalte (über eine REST-API) vom Server geladen. 

Das Hyperlink-Konzept bei Single-Page-Applikationen ist also ein anderes, als bei Multi-Page-Applikationen. Während in MPAs Hyperlinks verwendet werden, sprechen wir bei SPAs von *Routen*. Das dazugehörige Konzept heißt *Routing*. 


## Erste einfache Routen

Wir erstellen uns mithilfe von 

```bash
ng new routing
```
ein neues Angular-Projekt. Alle Fragen beantworten wir einfach durch Bestätigung mit der `Enter`-Taste. Um das Routing auszuprobieren, benötigen wir zunächst ein paar Komponenten, zwischen denen wir wechseln können. Wir wechseln in den Ordner `routing` und erstellen wir uns folgende Komponenten:

```bash
ng g c nav
ng g c home
ng g c login
ng g c about
ng g c footer
```

Außerdem fügen wir unserem Projekt noch Bootstrap hinzu, damit wir ein besseres Design erzielen (hat aber nichts mit Routing zu tun). Dazu führen wir zunächst 

```bash
npm install bootstrap
```
aus und fügen dann folgende Zeilen in die `angular.json` ein:

=== "angular.json"
```json linenums="1" hl_lines="30 34 91 95"
{
  "$schema": "./node_modules/@angular/cli/lib/config/schema.json",
  "version": 1,
  "newProjectRoot": "projects",
  "projects": {
    "vorbServices": {
      "projectType": "application",
      "schematics": {},
      "root": "",
      "sourceRoot": "src",
      "prefix": "app",
      "architect": {
        "build": {
          "builder": "@angular-devkit/build-angular:application",
          "options": {
            "outputPath": "dist/vorb-services",
            "index": "src/index.html",
            "browser": "src/main.ts",
            "polyfills": [
              "zone.js"
            ],
            "tsConfig": "tsconfig.app.json",
            "assets": [
              {
                "glob": "**/*",
                "input": "public"
              }
            ],
            "styles": [
              "node_modules/bootstrap/dist/css/bootstrap.min.css",
              "src/styles.css"
            ],
            "scripts": [
              "node_modules/bootstrap/dist/js/bootstrap.min.js"
            ]
          },
          "configurations": {
            "production": {
              "budgets": [
                {
                  "type": "initial",
                  "maximumWarning": "500kB",
                  "maximumError": "1MB"
                },
                {
                  "type": "anyComponentStyle",
                  "maximumWarning": "2kB",
                  "maximumError": "4kB"
                }
              ],
              "outputHashing": "all"
            },
            "development": {
              "optimization": false,
              "extractLicenses": false,
              "sourceMap": true
            }
          },
          "defaultConfiguration": "production"
        },
        "serve": {
          "builder": "@angular-devkit/build-angular:dev-server",
          "configurations": {
            "production": {
              "buildTarget": "vorbServices:build:production"
            },
            "development": {
              "buildTarget": "vorbServices:build:development"
            }
          },
          "defaultConfiguration": "development"
        },
        "extract-i18n": {
          "builder": "@angular-devkit/build-angular:extract-i18n"
        },
        "test": {
          "builder": "@angular-devkit/build-angular:karma",
          "options": {
            "polyfills": [
              "zone.js",
              "zone.js/testing"
            ],
            "tsConfig": "tsconfig.spec.json",
            "assets": [
              {
                "glob": "**/*",
                "input": "public"
              }
            ],
            "styles": [
              "node_modules/bootstrap/dist/css/bootstrap.min.css",
              "src/styles.css"
            ],
            "scripts": [
              "node_modules/bootstrap/dist/js/bootstrap.min.js"
            ]
          }
        }
      }
    }
  }
}
```


Die Komponenten können Sie wie folgt implementieren: 


=== "nav.component.html"
	```html linenums="1"
	<nav class="sticky-top navbar navbar-expand-lg navbar-light bg-light">
	    <div class="container-fluid">
	        <a class="navbar-brand" href="#">Webtech</a>
	        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
	      <span class="navbar-toggler-icon"></span>
	    </button>
	        <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
	            <div class="navbar-nav">
	                <a class="nav-link" href="#">Home</a>
	                <a class="nav-link" href="#">Login</a>
	                <a class="nav-link" href="#">About</a>
	            </div>
	        </div>
	    </div>
	</nav>
	```

=== "footer.component.html"
	```html linenums="1"
	<div class="fixed-bottom text-white-50 bg-dark p-3 text-center">
		Routing
	</div>
	```

=== "home.component.html"
	```html linenums="1"
	<main class="d-flex align-items-center min-vh-100">
	    <div class="container text-center">
	        Welcome home!
	    </div>
	</main>
	```

=== "home.component.css"
	```css linenums="1"
	main {
	    background-color: grey;
	}
	```

=== "about.component.html"
	```html linenums="1"
	<main class="d-flex align-items-center min-vh-100">
	    <div class="container text-center">
	        Everything about me...
	    </div>
	</main>
	```

=== "about.component.css"
	```css linenums="1"
	main {
	    background-color: rgb(95, 4, 4);
	    color: lightgrey;
	}
	```

=== "login.component.html"
	```html linenums="1"
	<main class="d-flex align-items-center min-vh-100">
	    <fieldset class="container col-4 col-offset-4">
	        <legend class="ms-3">Login</legend>
	        <form>
	            <div class="form-group m-3">
	                <input type="text" class="form-control" id="login1" placeholder="username">
	            </div>
	            <div class="form-group m-3">
	                <input type="password" class="form-control" id="login2" placeholder="password">
	            </div>
	            <div class="m-3">
                	<button type="submit" class="btn btn-secondary">Login</button>
            	</div>
	        </form>
	    </fieldset>
	</main>
	```

=== "login.component.css"
	```css linenums="1"
	main {
	    background-color: rgb(164, 201, 243);
	}
	```

Die `app.component.html` sieht nun wie folgt aus:

=== "app.component.html"
	```html linenums="1"
	<app-nav></app-nav>
	<router-outlet></router-outlet>
	<app-footer></app-footer>
	```

und in der `app.component.ts` sind die `FooterComponent` und `NavComponent` importiert:


=== "app.component.js"
	```js linenums="1"
	import { Component } from '@angular/core';
	import { RouterOutlet } from '@angular/router';
	import { NavComponent } from './nav/nav.component';
	import { FooterComponent } from './footer/footer.component';

	@Component({
	  selector: 'app-root',
	  standalone: true,
	  imports: [RouterOutlet, NavComponent, FooterComponent],
	  templateUrl: './app.component.html',
	  styleUrl: './app.component.css'
	})
	export class AppComponent {
	  title = 'routing';
	}
	```

Die `AppComponent` ist nun so gestaltet, dass oben die `nav`-Komponente und unten die `footer`-Komponente  eingebunden wird. Dazwischen steht jedoch der Komponentenselektor `<router-outlet></router-outlet>`. An dessen Stelle wird nun jeweils die Komponente eingesetzt, die wir durch das Routing ausgewählt haben. Dies erledigen wir in den folgenden Schritten.

### Routen definieren 

Zunächst definieren wir die Routen und zu jeder Route, welche Komponente dafür eingebunden wird. Die Routendefinitionen erfolgen in der `app.routes.ts` und dort im `routes`-Array. Dazu wird das `routes`-Array mit Objekten befüllt, die jeweils einen `path`-Eintrag und einen `component`-Eintrag erhalten. Ein solches Objekt legt fest, für welchen Pfad welche Komponente aufgerufen wird. 

=== "app.routes.ts"
	```js linenums="1" hl_lines="2-4 7-9"
	import { Routes } from '@angular/router';
	import { AboutComponent } from './about/about.component';
	import { LoginComponent } from './login/login.component';
	import { HomeComponent } from './home/home.component';

	export const routes: Routes = [
	    { path: "about", component: AboutComponent },
		{ path: "login", component: LoginComponent },
		{ path: "home", component: HomeComponent }
	];
	```

Testen Sie nun die URLs

```bash
http://localhost:4200/about
http://localhost:4200/home
http://localhost:4200/login
```

und Sie sehen jeweils, dass die für die jeweilige Route angegebene Komponente eingebunden wird. Der `<router-outlet></router-outlet>`-Selektor wird also dynamisch befüllt, je nachdem welche Route aufgerufen wird. 

Eine Sache ist jetzt jedoch noch nicht optimal. Erstens ist ganz am Anfang, also für `http://localhost:4200` gar keine Komponente eingebunden und zweitens soll unsere `home`-Komponente gar nicht unter einer extra Route (`http://localhost:4200/home`), sondern tatsächlich bereits unter `http://localhost:4200`  aufgerufen werden. Wir passen deshalb das `routes`-Array entsprechend an:

=== "app.routes.ts"
	```js linenums="1" hl_lines="9"
	import { Routes } from '@angular/router';
	import { AboutComponent } from './about/about.component';
	import { LoginComponent } from './login/login.component';
	import { HomeComponent } from './home/home.component';

	export const routes: Routes = [
	    { path: "about", component: AboutComponent },
		{ path: "login", component: LoginComponent },
		{ path: "", component: HomeComponent, pathMatch: 'full' }
	];
	```


Die neuhinzugefügte Eigenschaft `pathMatch: 'full'` gibt an, dass diese Route nur aufgerufen wird, wenn danach nichts weiter in der URL folgt. Die Auswahl der Routen erfolgt nach dem *first-match-Prinzip*. Das heißt, dass für die angegebene URL die erste Route ausgewählt wird, die "passt". Mit `pathMatch: 'full'` geben wir an, dass die Route zwar passen muss, aber nicht nur ein Präfix einer längeren Route sein darf. Nun funktionieren die Routen wie gewünscht:

```bash
http://localhost:4200
http://localhost:4200/about
http://localhost:4200/login
```

Für die erste URL wird die `home`-Komponente eingebunden, bei der zweiten die `about`-Komponente und bei der dritten die `login`-Komponente. Nun fehlt für die Definition nur noch eine Sache: Was soll passieren, wenn eine Route eingegeben wird, die gar nicht existiert, also z.B.

```bash
http://localhost:4200/wrong
```

Für diesen Fall nutzen wir eine *Wildcard* `**` und leiten auf die Route für unsere `HomeComponent` um. Wir könnten stattdessen aber auch dafür eine `PageNotFoundComponent` (`404`-Seite) einfügen und diese für einen solchen Fall aufrufen. 

=== "app.routes.ts"
	```js linenums="1" hl_lines="10"
	import { Routes } from '@angular/router';
	import { AboutComponent } from './about/about.component';
	import { LoginComponent } from './login/login.component';
	import { HomeComponent } from './home/home.component';

	export const routes: Routes = [
	    { path: "about", component: AboutComponent },
		{ path: "login", component: LoginComponent },
		{ path: "", component: HomeComponent, pathMatch: 'full' },
		{ path: "**", redirectTo: "" }
	];
	```

Nun müssen wir noch organisieren, wie die Routen innerhalb unserer Anwendung aufgerufen werden können (und nicht nur durch Eingabe der jeweiligen URL).

### Routen aufrufen

Wir wollen die Routen durch Mausklick aufrufen. Dafür bietet sich unser Navigationsmenü an. Routen werden **nicht** per `href`-Attribut aufgerufen, sondern per `routerLink`. Wir passen dazu unsere `nav`-Komponente an:


=== "nav.component.html"
	```html linenums="1" hl_lines="3 9-11"
	<nav class="sticky-top navbar navbar-expand-lg navbar-light bg-light">
	    <div class="container-fluid">
	        <a class="navbar-brand" routerLink="">Webtech</a>
	        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
	      <span class="navbar-toggler-icon"></span>
	    </button>
	        <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
	            <div class="navbar-nav">
	                <a class="nav-link" routerLink="">Home</a>
	                <a class="nav-link" routerLink="login">Login</a>
	                <a class="nav-link" routerLink="about">About</a>
	            </div>
	        </div>
	    </div>
	</nav>
	```

Leider funktioniert das Routing jetzt noch nicht. Dazu müssen wir in der `nav.component.ts` erst noch `RouterLink` importieren:

=== "nav.component.ts"
	```html linenums="1" hl_lines="2 7"
	import { Component } from '@angular/core';
	import { RouterLink } from '@angular/router';

	@Component({
	  selector: 'app-nav',
	  standalone: true,
	  imports: [RouterLink],
	  templateUrl: './nav.component.html',
	  styleUrl: './nav.component.css'
	})
	export class NavComponent {

	}
	```



Wir können das `routerLink`-Attribut auch unter Verwendung von [Attributbinding](templates.md#attributbindings) festlegen (dann kann Routing später sogar über Variablen erfolgen). Wenn Sie es als Attributdirektive gestalten (hat später einen Vorteil bei parametrisierten Routen), dann sieht es so aus:

```js
[routerLink]="['login']"
[routerLink]="['about']"
[routerLink]="['']"
```

Angenommen, Sie definieren sich noch eine eigene CSS-Klasse, in der sie festlegen, dass die Menüeinträge anders aussehen, wenn sie der aktuellen Route entsprechen, wenn also z.B. `Login` im Menü fett erscheint, sobald `http://localhost:4200/login` ausgewählt wurde. Die CSS-Definition könnte dann so aussehen:

```css
.myactive {
    font-weight: bold;
}
```

Das heißt, Sie haben eine CSS-Klasse `myactive` definiert. Diese Klasse kann aktiviert werden, wenn die Route aktiv ist. Dazu verwenden Sie das Attribut `routerLinkActive` und weisen diesem Attribut den Wert `"myactive"` zu. Das Menü sähe dann so aus:

```html linenums="7"
<div class="collapse navbar-collapse" id="navbarNavAltMarkup">
    <div class="navbar-nav">
        <a class="nav-link" routerLink="" routerLinkActive="myactive">Home</a>
        <a class="nav-link" routerLink="login" routerLinkActive="myactive">Login</a>
        <a class="nav-link" routerLink="about" routerLinkActive="myactive">About</a>
    </div>
</div>
```	

Auch `RouterLinkActive` muss in der `nav.component.ts` importiert werden:


=== "nav.component.ts"
	```html linenums="1" hl_lines="2 7"
	import { Component } from '@angular/core';
	import { RouterLink, RouterLinkActive } from '@angular/router';

	@Component({
	  selector: 'app-nav',
	  standalone: true,
	  imports: [RouterLink, RouterLinkActive],
	  templateUrl: './nav.component.html',
	  styleUrl: './nav.component.css'
	})
	export class NavComponent {

	}
	```

Wenn Sie Bootstrap verwenden, dann ist `routerLinkActive` nur für eigene CSS-Klassen notwendig (so wie im Beispiel `myactive`). Die Bootstrap-Klasse `active` wird automatisch aktiviert, wenn die Route aktiv ist. 

### Routenparameter

Häufig sollen aus einer Liste von Objekten ein einzelnes Objekt ausgewählt und dargestellt werden. Angenommen, wir wollen folgende `staedte.json` 


??? "staedte,json"
	```json
	[
	    {
	        "id":1,
	        "jahr":1237,
	        "stadt":"Berlin",
	        "link":"http://de.wikipedia.org/wiki/Berlin",
	        "bild":"/assets/images/berlin.png"
	    },
	    {
	        "id":2,
	        "jahr":1624,
	        "stadt":"New York",
	        "link":"http://de.wikipedia.org/wiki/New_York_City",
	        "bild":"/assets/images/newyork.png"
	    },
	    {
	        "id":3,
	        "jahr":1252,
	        "stadt":"Stockholm",
	        "link":"http://de.wikipedia.org/wiki/Stockholm",
	        "bild":"/assets/images/stockholm.png"
	    },
	    {
	        "id":4,
	        "jahr":1827,
	        "stadt":"Bremerhaven",
	        "link":"http://de.wikipedia.org/wiki/Bremerhaven",
	        "bild":"/assets/images/bremerhaven.png"
	    },
	    {
	        "id":5,
	        "jahr":150,
	        "stadt":"Bremen",
	        "link":"http://de.wikipedia.org/wiki/Bremen",
	        "bild":"/assets/images/bremen.png"
	    },
	    {
	        "id":6,
	        "jahr":1202,
	        "stadt":"Bernau",
	        "link":"http://de.wikipedia.org/wiki/Bernau_bei_Berlin",
	        "bild":"/assets/images/bernau.png"
	    },
	    {
	        "id":7,
	        "jahr":929,
	        "stadt":"Brandenburg",
	        "link":"http://de.wikipedia.org/wiki/Brandenburg_an_der_Havel",
	        "bild":"/assets/images/brandenburg.png"
	    },
	    {
	        "id":8,
	        "jahr":805,
	        "stadt":"Magdeburg",
	        "link":"http://de.wikipedia.org/wiki/Magdeburg",
	        "bild":"/assets/images/magdeburg.png"
	    },
	    {
	        "id":9,
	        "jahr":1222,
	        "stadt":"Marburg",
	        "link":"http://de.wikipedia.org/wiki/Marburg",
	        "bild":"/assets/images/marburg.png"
	    },
	    {
	        "id":10,
	        "jahr":766,
	        "stadt":"Mannheim",
	        "link":"http://de.wikipedia.org/wiki/Mannheim",
	        "bild":"/assets/images/mannheim.png"
	    },
	    {
	        "id":11,
	        "jahr":782,
	        "stadt":"Mainz",
	        "link":"http://de.wikipedia.org/wiki/Mainz",
	        "bild":"/assets/images/mainz.png"
	    }
	]
	```

verwenden. Wir vereinfachen es und verwenden direkt das Array (von Objekten) und beschreiben die JavaScript-Objekte nicht in JSON, sondern direkt als Objekte (der Unterschied besteht darin, dass die Schlüssel nicht in Anführungsstrichen stehen, siehe [`JSON.parse()` und `JSON.stringify()`](objekte.md#jsonparse-und-jsonstringify).


??? "staedte als Array"
    ```js
    [
	    {
	        id: 1,
	        jahr: 1237,
	        stadt: "Berlin",
	        link: "http://de.wikipedia.org/wiki/Berlin",
	        bild: "/assets/images/berlin.png"
	    },
	    {
	        id: 2,
	        jahr: 1624,
	        stadt: "New York",
	        link: "http://de.wikipedia.org/wiki/New_York_City",
	        bild: "/assets/images/newyork.png"
	    },
	    {
	        id: 3,
	        jahr: 1252,
	        stadt: "Stockholm",
	        link: "http://de.wikipedia.org/wiki/Stockholm",
	        bild: "/assets/images/stockholm.png"
	    },
	    {
	        id: 4,
	        jahr: 1827,
	        stadt: "Bremerhaven",
	        link: "http://de.wikipedia.org/wiki/Bremerhaven",
	        bild: "/assets/images/bremerhaven.png"
	    },
	    {
	        id: 5,
	        jahr: 150,
	        stadt: "Bremen",
	        link: "http://de.wikipedia.org/wiki/Bremen",
	        bild: "/assets/images/bremen.png"
	    },
	    {
	        id: 6,
	        jahr: 1202,
	        stadt: "Bernau",
	        link: "http://de.wikipedia.org/wiki/Bernau_bei_Berlin",
	        bild: "/assets/images/bernau.png"
	    },
	    {
	        id: 7,
	        jahr: 929,
	        stadt: "Brandenburg",
	        link: "http://de.wikipedia.org/wiki/Brandenburg_an_der_Havel",
	        bild: "/assets/images/brandenburg.png"
	    },
	    {
	        id: 8,
	        jahr: 805,
	        stadt: "Magdeburg",
	        link: "http://de.wikipedia.org/wiki/Magdeburg",
	        bild: "/assets/images/magdeburg.png"
	    },
	    {
	        id: 9,
	        jahr: 1222,
	        stadt: "Marburg",
	        link: "http://de.wikipedia.org/wiki/Marburg",
	        bild: "/assets/images/marburg.png"
	    },
	    {
	        id: 10,
	        jahr: 766,
	        stadt: "Mannheim",
	        link: "http://de.wikipedia.org/wiki/Mannheim",
	        bild: "/assets/images/mannheim.png"
	    },
	    {
	        id: 11,
	        jahr: 782,
	        stadt: "Mainz",
	        link: "http://de.wikipedia.org/wiki/Mainz",
	        bild: "/assets/images/mainz.png"
	    }
    ]
    ``` 

Erstellen Sie sich im `public`-Ordner Ihres Angular-Projektes einen Ordner `assets`. In diesen Ordner kopieren Sie den `images`-Ordner, den Sie durch Entpacken der [images.zip](./files/images_staedte.zip) erhalten. 

Wir wollen nun über die Route auf ein einzelnes Objekt zugreifen. Wenn wir also z.B. `http://localhost:4200/cities/0` eingeben, soll das `Berlin`-Objekt ausgewählt werden, bei `http://localhost:4200/cities/1` das `New York`-Objekt usw. 

Dazu erstellen wir uns zunächst eine neue Komponente `cities` mit `ng g c cities` und folgendem Code:


=== "cities.component.html"
	```html linenums="1"
	<div class="container">
	    <h1>Städte</h1>

	    <table class="table table-striped">
	        <caption>Ausgewählte Städte</caption>
	        <thead>
	            <tr>
	                <th scope="col">Nr</th>
	                <th scope="col">Jahr</th>
	                <th scope="col">Stadt</th>
	                <th scope="col">Bild</th>
	            </tr>
	        </thead>
	        <tbody>
	            @for (stadt of staedte; track $index; let i = $index) {
	                <tr>
	                    <td>{{ i+1 }} </td>
	                    <td>{{ stadt.jahr }}</td>
	                    <td>{{ stadt.stadt }}</td>
	                    <td>
	                        <a [href]="stadt.link">
	                            <img [src]=" stadt.bild " [alt]="stadt.stadt " />
	                        </a>
	                    </td>
	                </tr>
	            }
	        </tbody>
	    </table>
	</div>
	```

=== "cities.component.ts"
	```js linenums="1"
	import { Component } from '@angular/core';

	@Component({
	  selector: 'app-cities',
	  standalone: true,
	  imports: [],
	  templateUrl: './cities.component.html',
	  styleUrl: './cities.component.css'
	})
	export class CitiesComponent {
	  staedte = [
	    {
	        id: 1,
	        jahr: 1237,
	        stadt: "Berlin",
	        link: "http://de.wikipedia.org/wiki/Berlin",
	        bild: "/assets/images/berlin.png"
	    },
	    {
	        id: 2,
	        jahr: 1624,
	        stadt: "New York",
	        link: "http://de.wikipedia.org/wiki/New_York_City",
	        bild: "/assets/images/newyork.png"
	    },
	    {
	        id: 3,
	        jahr: 1252,
	        stadt: "Stockholm",
	        link: "http://de.wikipedia.org/wiki/Stockholm",
	        bild: "/assets/images/stockholm.png"
	    },
	    {
	        id: 4,
	        jahr: 1827,
	        stadt: "Bremerhaven",
	        link: "http://de.wikipedia.org/wiki/Bremerhaven",
	        bild: "/assets/images/bremerhaven.png"
	    },
	    {
	        id: 5,
	        jahr: 150,
	        stadt: "Bremen",
	        link: "http://de.wikipedia.org/wiki/Bremen",
	        bild: "/assets/images/bremen.png"
	    },
	    {
	        id: 6,
	        jahr: 1202,
	        stadt: "Bernau",
	        link: "http://de.wikipedia.org/wiki/Bernau_bei_Berlin",
	        bild: "/assets/images/bernau.png"
	    },
	    {
	        id: 7,
	        jahr: 929,
	        stadt: "Brandenburg",
	        link: "http://de.wikipedia.org/wiki/Brandenburg_an_der_Havel",
	        bild: "/assets/images/brandenburg.png"
	    },
	    {
	        id: 8,
	        jahr: 805,
	        stadt: "Magdeburg",
	        link: "http://de.wikipedia.org/wiki/Magdeburg",
	        bild: "/assets/images/magdeburg.png"
	    },
	    {
	        id: 9,
	        jahr: 1222,
	        stadt: "Marburg",
	        link: "http://de.wikipedia.org/wiki/Marburg",
	        bild: "/assets/images/marburg.png"
	    },
	    {
	        id: 10,
	        jahr: 766,
	        stadt: "Mannheim",
	        link: "http://de.wikipedia.org/wiki/Mannheim",
	        bild: "/assets/images/mannheim.png"
	    },
	    {
	        id: 11,
	        jahr: 782,
	        stadt: "Mainz",
	        link: "http://de.wikipedia.org/wiki/Mainz",
	        bild: "/assets/images/mainz.png"
	    }
	  ]
	}
	```

=== "cities.component.css"
	```css linenums="1"
	td img {
	    width: 10%;
	}
	```

=== "app.routes.ts"
	```js linenums="1"
	import { Routes } from '@angular/router';
	import { AboutComponent } from './about/about.component';
	import { LoginComponent } from './login/login.component';
	import { HomeComponent } from './home/home.component';
	import { CitiesComponent } from './cities/cities.component';

	export const routes: Routes = [
	    { path: "about", component: AboutComponent },
	    { path: "cities", component: CitiesComponent },
		{ path: "login", component: LoginComponent },
		{ path: "", component: HomeComponent, pathMatch: 'full' },
	    { path: "**", redirectTo: "" }
	];
	```

### Parametrisierte Routen

Damit wir in der Lage sind, auf Routen, wie `http://localhost:4200/cities/0` oder `http://localhost:4200/cities/1` geeignet zu reagieren, müssen wir die jeweilige Zahl am Ende der Routen als Parameter definieren. Das machen wir in der `app.routes.ts` wie folgt:

=== "app.routes.ts"
	```js linenums="1" hl_lines="10"
	import { Routes } from '@angular/router';
	import { AboutComponent } from './about/about.component';
	import { LoginComponent } from './login/login.component';
	import { HomeComponent } from './home/home.component';
	import { CitiesComponent } from './cities/cities.component';

	export const routes: Routes = [
	    { path: "about", component: AboutComponent },
	    { path: "cities", component: CitiesComponent },
	    { path: "cities/:id", component: CitiesComponent },
		{ path: "login", component: LoginComponent },
		{ path: "", component: HomeComponent, pathMatch: 'full' },
	    { path: "**", redirectTo: "" }
	];
	```

Wir wollen zunächst diesen Parameter einfach nur in der `cities.component.ts` auslesen. Dazu benötigen wir das Modul `ActivatedRoute`. 


=== "cities.component.ts"
	```js linenums="1" hl_lines="2 16"
	import { Component } from '@angular/core';
	import { ActivatedRoute } from '@angular/router';

	@Component({
	  selector: 'app-cities',
	  standalone: true,
	  imports: [],
	  templateUrl: './cities.component.html',
	  styleUrl: './cities.component.css'
	})
	export class CitiesComponent {
	  staedte = [
	  	// alle Eintraege eingeklappt
	  ]

	  constructor(private route: ActivatedRoute) {}
	}
	```

Wir implementieren den Konstruktor der Klasse `CitiesComponent`. Per *dependency injection* wird darin `ActivatedRoute` eingebunden. Wir definieren uns eine Objektvariable `route`, die von diesem Typ ist. Die Spezifikation von `ActivatedRoute` finden Sie [hier](https://angular.dev/api/router/ActivatedRoute).

Nun implementieren wir noch das Interface `OnInit` in der Klasse `CitiesComponent`. Damit haben wir einen Lifecycle-hook, in wir uns "reinhängen" können. Beim Initialisieren der Komponente wollen wir ermitteln, welche Route dazu geführt hat, dass die Komponente aufgerufen wurde. Zum Implementieren des Interfaces müssen wir dieses zunächst importieren. Wir schreiben neben die Klasse `implements OnInit`. Dann schlägt der Quick-Fix vor, dass wir `OnInit` importieren (aus `@angular/core`). Dann ist jedoch die Klasse selbst noch rot unterstrichen, da wir zum Implementieren des Interfaces die Funktion `ngOnInit()` implementieren müssen. Wir folgen erneut dem Quick-Fix und die Funktion erscheint:


=== "cities.component.ts"
	```js linenums="1" hl_lines="1 11 18-20"
	import { Component, OnInit } from '@angular/core';
	import { ActivatedRoute } from '@angular/router';

	@Component({
	  selector: 'app-cities',
	  standalone: true,
	  imports: [],
	  templateUrl: './cities.component.html',
	  styleUrl: './cities.component.css'
	})
	export class CitiesComponent implements OnInit {
	  staedte = [
	  	// alle Eintraege eingeklappt
	  ]

	  constructor(private route: ActivatedRoute) {}

	  ngOnInit(): void {
	        throw new Error('Method not implemented.');
	  }
	}
	```

Nun implementieren wir die Funktion `ngOnInit()`. Die Implementierung sieht wie folgt aus:

=== "cities.component.ts"
	```js linenums="1" hl_lines="12 20-22"
	import { Component, OnInit } from '@angular/core';
	import { ActivatedRoute } from '@angular/router';

	@Component({
	  selector: 'app-cities',
	  standalone: true,
	  imports: [],
	  templateUrl: './cities.component.html',
	  styleUrl: './cities.component.css'
	})
	export class CitiesComponent implements OnInit {
	  id: string | null = "";
	  staedte = [
	  	// alle Eintraege eingeklappt
	  ]

	  constructor(private route: ActivatedRoute) {}

	  ngOnInit(): void {
	    this.id = this.route.snapshot.paramMap.get('id');
	    if(this.id) console.log('id : ', this.id);
	    else console.log('ohne Parameter');
	  }
	}
	```

Wir erstellen uns eine Objektvariable `id`. Diese ist vom Typ `string`, kann aber auch `null` sein. Wir initialisieren sie mit dem leeren `string`
. Der Initialisierungswert ist aber egal, da diese Variable auf jeden Fall bei der Initialisierung der Komponente (`ngOnInit()`) einen Wert bekommt (Zeile `20`). Zur Wertermittlung verwenden wir die Objektvariable `route`, die vom Typ `ActivatedRoute` ist (siehe [hier](https://angular.dev/api/router/ActivatedRoute)). Die Eigenschaft `snapshot`gibt die aktuelle Route zurück und `paramMap` alle Parameter der Route. Mithilfe von `get()` kann man aus der Menge der von `paramMap` zurückgegebenen Parameter nach einenm konkreten Parameter filtern. Wir filtern nach dem Parameter `id`, da wir diesen in `app.routes.ts` mit `{ path: "cities/:id", component: CitiesComponent },` so benannt haben. Wir hätten dort auch jeden beliebigen anderen Namen wählen können und hätten dann nach diesem Namen gefiltert. 

Die Funktion `get()` gibt nun entweder den Wert dieses Parameters in der Route als String zurück, z.B. `"0"` oder `"1"` oder aber, falls kein Parameterwert für `id` in der Route enthalten ist, den Wert `null`. In Zeile `21` fragen wir ab, ob die Objektvariable `id` nun einen Wert hat (oder `null` ist). Wenn sie einen Wert hat, wird dieser auf der Konsole ausgegeben, wenn der Wert `null` ist, wird auf der Konsole `ohne Parameter` ausgegeben. 

Wir erstellen uns nun noch eine Funktion, die im Falle eines Wertes für die Objektvariable `id` diesen Wert nimmt und damit die Stadt aus dem Array aussucht, die den Index hat, der mit `id` übereinstimmt.

=== "cities.component.ts - Erweiterung"
	```js linenums="92" hl_lines="1 9 13-18"
	  city: {id: number; jahr: number; stadt: string; link: string; bild: string } | null = null;
	  
	  constructor(private route: ActivatedRoute) {

	  }

	  ngOnInit(): void {
	    this.id = this.route.snapshot.paramMap.get('id');
	    if(this.id) this.filterStaedte();
	    else console.log('ohne Parameter');
	  }

	  filterStaedte(): void {
	    if(this.id) {
	        this.city = this.staedte[Number(this.id)];
	        console.log('stadt : ', this.city)
	    }
	  }
	```

Wir erstellen zunächst eine weitere Objektvariable `city`. Diese ist ein `Object` und wir definieren die Eigenschaften mithilfe von `city: {id: number; jahr: number; stadt: string; link: string; bild: string }`. Der Wert dieser Variable kann `null` sein, ist er initial auch. Wir verwenden diese Variable, um darin die Stadt zu speichern, die durch die parametrisierte Route ausgewählt wird. 

Die `filterStaedte()`-Funktion setzt bei parametrieserter Route den Wert der Variablen `city` durch Zugriff auf das `staedte`-Array. Da `id` ein `string` ist, wieder dieser mithilfe von `Number` in eine `number` konvertiert. 

Nun führen wir in `cities.component.html` nur noch die Fallunterscheidung ein, ob alle Städte oder nur eine angezeigt werden sollen:


=== "cities.component.html"
	```html linenums="1"
	<div class="container">
	    
	    @if(city) {
	        <h1>{{ city.stadt }} </h1>

	        <div class="card" style="width: 20%">
	            <img [src]="city.bild" class="card-img-top" [alt]="city.stadt">
	            <div class="card-body">
	              <h5 class="card-title">{{ city.stadt }}</h5>
	              <p class="card-text">
	                <a [href]="city.link">Weitere Informationen über {{ city.stadt }}</a>
	              </p>
	              <a routerLink="/cities" class="btn btn-primary">Zurück</a>
	            </div>
	          </div>
	    
	    } @else {
	        <h1>Städte</h1>

	    <table class="table table-striped table-responsive">
	        <caption>Ausgewählte Städte</caption>
	        <thead>
	            <tr>
	                <th scope="col">Nr</th>
	                <th scope="col">Jahr</th>
	                <th scope="col">Stadt</th>
	                <th scope="col">Bild</th>
	            </tr>
	        </thead>
	        <tbody>
	            @for (stadt of staedte; track $index; let i = $index) {
	                <tr>
	                    <td><a [routerLink]="['/cities', i]" class="btn btn-secondary">{{ i+1 }}</a> </td>
	                    <td>{{ stadt.jahr }}</td>
	                    <td>{{ stadt.stadt }}</td>
	                    <td>
	                        <a [href]="stadt.link">
	                            <img [src]=" stadt.bild " [alt]="stadt.stadt " />
	                        </a>
	                    </td>
	                </tr>
	            }
	        </tbody>
	    </table>

	    }
	</div>
	```


In der `cities.component.ts` muss nun auch `RouterLink` importiert werden, da wir in der Tabelle in der linken Spalte durch Klick auf die Buttons direkt die parametrisierten Routen aufrufen können. Hier nochmal die beiden anderen Dateien der `CitiesComponent` im Überblick:


??? "cities.component.ts"
	```js linenums="1"
	import { Component, OnInit } from '@angular/core';
	import { ActivatedRoute, RouterLink } from '@angular/router';

	@Component({
	  selector: 'app-cities',
	  standalone: true,
	  imports: [RouterLink],
	  templateUrl: './cities.component.html',
	  styleUrl: './cities.component.css'
	})
	export class CitiesComponent implements OnInit {
	  id: string | null = "";
	  staedte = [
	    {
	        id: 1,
	        jahr: 1237,
	        stadt: "Berlin",
	        link: "http://de.wikipedia.org/wiki/Berlin",
	        bild: "/assets/images/berlin.png"
	    },
	    {
	        id: 2,
	        jahr: 1624,
	        stadt: "New York",
	        link: "http://de.wikipedia.org/wiki/New_York_City",
	        bild: "/assets/images/newyork.png"
	    },
	    {
	        id: 3,
	        jahr: 1252,
	        stadt: "Stockholm",
	        link: "http://de.wikipedia.org/wiki/Stockholm",
	        bild: "/assets/images/stockholm.png"
	    },
	    {
	        id: 4,
	        jahr: 1827,
	        stadt: "Bremerhaven",
	        link: "http://de.wikipedia.org/wiki/Bremerhaven",
	        bild: "/assets/images/bremerhaven.png"
	    },
	    {
	        id: 5,
	        jahr: 150,
	        stadt: "Bremen",
	        link: "http://de.wikipedia.org/wiki/Bremen",
	        bild: "/assets/images/bremen.png"
	    },
	    {
	        id: 6,
	        jahr: 1202,
	        stadt: "Bernau",
	        link: "http://de.wikipedia.org/wiki/Bernau_bei_Berlin",
	        bild: "/assets/images/bernau.png"
	    },
	    {
	        id: 7,
	        jahr: 929,
	        stadt: "Brandenburg",
	        link: "http://de.wikipedia.org/wiki/Brandenburg_an_der_Havel",
	        bild: "/assets/images/brandenburg.png"
	    },
	    {
	        id: 8,
	        jahr: 805,
	        stadt: "Magdeburg",
	        link: "http://de.wikipedia.org/wiki/Magdeburg",
	        bild: "/assets/images/magdeburg.png"
	    },
	    {
	        id: 9,
	        jahr: 1222,
	        stadt: "Marburg",
	        link: "http://de.wikipedia.org/wiki/Marburg",
	        bild: "/assets/images/marburg.png"
	    },
	    {
	        id: 10,
	        jahr: 766,
	        stadt: "Mannheim",
	        link: "http://de.wikipedia.org/wiki/Mannheim",
	        bild: "/assets/images/mannheim.png"
	    },
	    {
	        id: 11,
	        jahr: 782,
	        stadt: "Mainz",
	        link: "http://de.wikipedia.org/wiki/Mainz",
	        bild: "/assets/images/mainz.png"
	    }
	  ]
	  city: {id: number; jahr: number; stadt: string; link: string; bild: string } | null = null;
	  
	  constructor(private route: ActivatedRoute) {

	  }

	  ngOnInit(): void {
	    this.id = this.route.snapshot.paramMap.get('id');
	    if(this.id) this.filterStaedte();
	    else console.log('ohne Parameter');
	  }

	  filterStaedte() {
	    if(this.id) {
	        this.city = this.staedte[Number(this.id)];
	        console.log('stadt : ', this.city)
	    }
	  }
	}

	```

??? "cities.component.css"
	```html linenums="1"
	table {
	    table-layout: fixed;
	    width: 80%;
	}

	th, td {
	    width: 25%;
	}
	td img {
	    width: 20%;
	}
	```


Die Daten haben wir hier noch als Array in einer Variablen gespeichert. Nun wollen wir die Daten jedoch in einen zentralen *Service* auslagern. 

## Services

Ein *Service* ist eine Klasse für einen konkreten Zweck. Services unterscheiden sich von Komponenten dahingehend, dass

- eine Komponente für die Nutzerinteraktion zuständig ist, 
- eine Komponente Eigenschaften (Daten) präsentiert, 
- eine Komponente Methoden zur Datenbindung (*data binding*) zur Verfügung stellt, um
- zwischen *View* und Anwendungslogik zu vermitteln.

Ein Service

- erfüllt eine konkrete Aufgabe, typischerweise mit Daten, 
- ohne sich um die Darstellung der Daten zu kümmern.
- Typische Aufgaben eines Services sind: Daten vom Server holen oder auf den Server laden, Nutzereingaben zu validieren. 
- Ein Service steht typischerweise allen Komponenten zur Verfügung (aber nicht jede Komponente muss einen Service nutzen).

Ein Service ist eine Klasse mit dem Decorator `@Injectable()`. Services enthalten Anwendungslogik, die aus Komponenten ausgelagert werden kann. Ein Service kann mittels CLI so erzeugt werden:

```
ng generate service nameDesServices
```

In dem Decorator `@Injectable()` wird mittels `providedIn: root` angegeben, dass der Service von allen Komponenten innerhalb des Root-Moduls genutzt werden kann. Ist der Service von anderen Services oder Komponenten abhängig, können diese Services oder Komponenten mittels *dependency injection* als Parameter des Service-Konstruktor eingebunden werden. Hier ein allgemeines Beispiel eines Services `MyService`:

=== "my.service.ts"
    ```javascript linenums="1"
    import { Injectable } from '@angular/core';

    @Injectable({
      providedIn: 'root'
    })
    export class MyService {

      constructor(private myDependency: MyDependency) {
      }
    }
    ```

Der Service kann dann mittels *dependency injection* von einer Komponente verwendet werden. Beispiel:

=== "example.component.ts"
    ```javascript
    import {Component, OnInit} from '@angular/core';

    import {MyService} from './shared/my.service';

    @Component({
      selector: 'app-example',
      templateUrl: './example.component.html',
      styleUrls: ['./example.component.css']
    })
    export class ExampleComponent implements OnInit {

      constructor(private myService: MyService) { }

      ngOnInit(): void {
        this.example.methodOfMyService();
      }

    }
    ```

Für weiterführende Informationen siehe [https://angular.dev/tutorials/learn-angular/19-creating-an-injectable-service#](https://angular.dev/tutorials/learn-angular/19-creating-an-injectable-service#).

### Service für das Routing-Beispiel

Für unser Routing-Beispiel wollen wir Daten über einen Service allen Komponenten zur Verfügung stellen. Wir erstellen dazu einen Service `data` und dazu auch noch ein *Interface* `data`, das das Datenmodell für eine `Stadt` beschreibt. Beides erstellen wir in einem `shared`-Ordner.

Zur Vorbereitung legen wir zunächst die folgende Datei `staedte.json` im `public/assets`-Ordner ab:

??? "public/assets/staedte,json"
	```json
	[
	    {
	        "id":1,
	        "jahr":1237,
	        "stadt":"Berlin",
	        "link":"http://de.wikipedia.org/wiki/Berlin",
	        "bild":"/assets/images/berlin.png"
	    },
	    {
	        "id":2,
	        "jahr":1624,
	        "stadt":"New York",
	        "link":"http://de.wikipedia.org/wiki/New_York_City",
	        "bild":"/assets/images/newyork.png"
	    },
	    {
	        "id":3,
	        "jahr":1252,
	        "stadt":"Stockholm",
	        "link":"http://de.wikipedia.org/wiki/Stockholm",
	        "bild":"/assets/images/stockholm.png"
	    },
	    {
	        "id":4,
	        "jahr":1827,
	        "stadt":"Bremerhaven",
	        "link":"http://de.wikipedia.org/wiki/Bremerhaven",
	        "bild":"/assets/images/bremerhaven.png"
	    },
	    {
	        "id":5,
	        "jahr":150,
	        "stadt":"Bremen",
	        "link":"http://de.wikipedia.org/wiki/Bremen",
	        "bild":"/assets/images/bremen.png"
	    },
	    {
	        "id":6,
	        "jahr":1202,
	        "stadt":"Bernau",
	        "link":"http://de.wikipedia.org/wiki/Bernau_bei_Berlin",
	        "bild":"/assets/images/bernau.png"
	    },
	    {
	        "id":7,
	        "jahr":929,
	        "stadt":"Brandenburg",
	        "link":"http://de.wikipedia.org/wiki/Brandenburg_an_der_Havel",
	        "bild":"/assets/images/brandenburg.png"
	    },
	    {
	        "id":8,
	        "jahr":805,
	        "stadt":"Magdeburg",
	        "link":"http://de.wikipedia.org/wiki/Magdeburg",
	        "bild":"/assets/images/magdeburg.png"
	    },
	    {
	        "id":9,
	        "jahr":1222,
	        "stadt":"Marburg",
	        "link":"http://de.wikipedia.org/wiki/Marburg",
	        "bild":"/assets/images/marburg.png"
	    },
	    {
	        "id":10,
	        "jahr":766,
	        "stadt":"Mannheim",
	        "link":"http://de.wikipedia.org/wiki/Mannheim",
	        "bild":"/assets/images/mannheim.png"
	    },
	    {
	        "id":11,
	        "jahr":782,
	        "stadt":"Mainz",
	        "link":"http://de.wikipedia.org/wiki/Mainz",
	        "bild":"/assets/images/mainz.png"
	    }
	]
	```

In diesen Ordner kopieren wir auch den `images`-Ordner, den Sie durch Entpacken der [images.zip](./files/images_staedte.zip) erhalten - falls Sie es nicht bereits vorher ([s.o.](routing.md#routenparameter)) gemacht haben. 

Mit 

```bash
ng g service shared/data
```

lassen wir die CLI den Service erstellen. Im Ordner `shared` entstehen zwei Dateien:

- `data.service.ts` und 
- `data.service.spec.ts`.

Letztere ist für Testzwecke und interessiert uns (derzeit noch) nicht. In diesen Service binden wir gleich unsere Daten ein und stellen eine Funktion zur Verfügung, die uns alle Daten nach außen zur Verfügung stellt. Zunächst erstellen wir noch, zur Gewährleistung der Typsicherheit, ein *Interface* für das Datenmodell:

```bash
ng g interface shared/city
```

Es entsteht eine Datei `city.ts` mit folgendem Inhalt:

=== "shared/city.ts"
	```js
	export interface City {
	}
	```

In dieses Interface tragen wir unser Datenmodell ein:

=== "shared/city.ts"
	```js
	export interface City {
	    id: number;
	    jahr: number;
	    stadt: string;
	    link: string;
	    bild: string;
	}
	```

Dem `data`-Service fügen wir nun ein Funktion hinzu, die die `staedte.json` einliest und alle Städte als JavaScript-Objekt zurückgibt. Dazu verwenden wir die [`fetch`-API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch). Diese gibt ein [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) zurück- Mit *Promises* beschäftigen wir uns später nochmal genauer. Die *Promise* wiederum enthält ein [`Response`-Objekt](https://developer.mozilla.org/en-US/docs/Web/API/Response). Da es sich bei uns dabei um ein JSON handelt, können wir dieses *Response*-Objekt mithilfe der statischen Funktion `Response.json()` in ein weiteres `Response`-Objekt umwandeln, welches die JSON-Daten zurückgibt. Zum Typisieren der Rückgabe der Funktion verwenden wir das Interface `City`:

=== "shared/data.service.ts"
	```js 
	import { Injectable } from '@angular/core';
	import { City } from './city';

	@Injectable({
	  providedIn: 'root'
	})
	export class DataService {

	  constructor() { }

	  async getAll(): Promise<City[]> {
	    let response = await fetch('./assets/staedte.json');
	    let staedte = await response.json();
	    console.log('staedte', staedte)
	    return staedte;
	  }
	}
	```


Das Rückgabeobjekt der Funktion `getAll()` ist also eine`Promise`, d.h. den Aufruf von `getAll()` können Sie entweder mit `then()`-verketten oder `await/async` verwenden. Dazu kommen wir gleich: 


### Verwendung des Services

Wir zeigen die Verwendung des Services zunächst am Beispiel der `cities`-Komponente. Dort hatten wir bisher die Daten direkt gespeichert. Nun sollen sie dort über den Service eingebunden werden. Dazu ändern wir die `cities.component.ts` wie folgt:

=== "cities.component.ts"
	```js linenums="1" hl_lines="3-4 16 19-23"
	import { Component, OnInit } from '@angular/core';
	import { ActivatedRoute, RouterLink } from '@angular/router';
	import { City } from '../shared/city';
	import { DataService } from '../shared/data.service';

	@Component({
	  selector: 'app-cities',
	  standalone: true,
	  imports: [RouterLink],
	  templateUrl: './cities.component.html',
	  styleUrl: './cities.component.css'
	})
	export class CitiesComponent implements OnInit {
	  id: string | null = "";

	  staedte: City[] = [];
	  city: {id: number; jahr: number; stadt: string; link: string; bild: string } | null = null;
	  
	  constructor(private route: ActivatedRoute, private service: DataService) {
	    this.service.getAll()
	    .then( response => this.staedte = response)
	    .then( staedte => console.log('staedte geladen', staedte))
	  }

	  ngOnInit(): void {
	    this.id = this.route.snapshot.paramMap.get('id');
	    if(this.id) this.filterStaedte();
	    else console.log('ohne Parameter');
	  }

	  filterStaedte() {
	    if(this.id) {
	        this.city = this.staedte[Number(this.id)];
	        console.log('stadt : ', this.city)
	    }
	  }
	}


	```

Der Service wird per *Dependency Injection* im Konstruktor eingebunden. Damit ist `service` (die Referenz auf den Service - können Sie nennen, wie Sie möchten) eine weitere Objekteigenschaft der `cities`-Komponent. Wir rufen die `getAll()`-Funktion des Services auf, die alle Daten des `staedte`-Arrays als Promise zurückgibt und speichern diese in der `staedte`-Variablen (siehe Konstruktor). Diese ist vonm Typ `City[]`. Um diesen Typ zu kennen, muss das Interface `City` in die Komponente importiert werden (Zeile `3`). Unsere Anwendung funktioniert nun wieder exakt wie zuvor. 

### Weiter mit parametrisierten Routen

Denselben Service wollen wir nun auch in der `city`-Komponente verwenden, in der wir eine einzelne Stadt nach ihrer `id` auswählen und darstellen wollen. Dazu erweitern wir zunächst den `data`-Service um eine Funktion, die uns ein einzelnes Stadt-Objekt für eine gegebene `id` zurückgibt:


=== "shared/data.service.ts"
	```js linenums="1" hl_lines="18-24"
	import { Injectable } from '@angular/core';
	import { City } from './city';

	@Injectable({
	  providedIn: 'root'
	})
	export class DataService {

	  constructor() { }

	  async getAll(): Promise<City[]> {
	    let response = await fetch('./assets/staedte.json');
	    let staedte = await response.json();
	    console.log('staedte', staedte)
	    return staedte;
	  }

	  async getOne(id: number): Promise<City[]> {
	    let response = await fetch('./assets/staedte.json');
	    let staedte: City[] = await response.json();
	    let stadt: City[] = staedte.filter( data => data.id == id );
	    console.log('stadt', stadt)
	    return stadt;
	  }
	}

	```

Diese Funktion gibt ein `City`-Array als ein `Promise` zurück. Da `id` in unserem JSON eindeutig ist, enthält das zurückgegebene Array entweder ein Element (die Stadt mit der passenden `id`) oder keins (wenn `id` nicht passt). Die Auswertung, ob das Array einen Eintrag enthält oder nicht, überlassen wir aber der aufrufenden Komponente. Im Gegensatz zu oben, wo wir den Parameter der Route als Index des Arrays verwendet haben, vergleichen wir nun mit der `id`. Dadurch ergibt sich ein Versatz von `1` (die Stadt mit der `id=1` hat den Index `0` im Array). Wir hätten hier natürlich auch stattdessen den ndex verwenden können, wollten nur mal `filter() ` verwenden, wenn es `id` schonmal gibt...

Die Tabelle, die wir in `cities.somponent.html` erzeugen, erweitern wir um eine Spalte, in der wir die Links auf die Detailseiten der jeweiligen Stadt hinterlegen:

=== "cities.component.html"
	```html linenums="1" hl_lines="28 34 42"
	<div class="container">
	    
	    @if(city) {
	        <h1>{{ city.stadt }} </h1>

	        <div class="card" style="width: 20%">
	            <img [src]="city.bild" class="card-img-top" [alt]="city.stadt">
	            <div class="card-body">
	              <h5 class="card-title">{{ city.stadt }}</h5>
	              <p class="card-text">
	                <a [href]="city.link">Weitere Informationen über {{ city.stadt }}</a>
	              </p>
	              <a routerLink="/cities" class="btn btn-primary">Zurück</a>
	            </div>
	          </div>
	    
	    } @else {
	        <h1>Städte</h1>

	    <table class="table table-striped table-responsive">
	        <caption>Ausgewählte Städte</caption>
	        <thead>
	            <tr>
	                <th scope="col">Nr</th>
	                <th scope="col">Jahr</th>
	                <th scope="col">Stadt</th>
	                <th scope="col">Bild</th>
	                <th scope="col">Details</th>
	            </tr>
	        </thead>
	        <tbody>
	            @for (stadt of staedte; track $index; let i = $index) {
	                <tr>
	                    <td>{{ i+1 }}</td>
	                    <td>{{ stadt.jahr }}</td>
	                    <td>{{ stadt.stadt }}</td>
	                    <td>
	                        <a [href]="stadt.link">
	                            <img [src]=" stadt.bild " [alt]="stadt.stadt " />
	                        </a>
	                    </td>
	                    <td><a [routerLink]="['/cities', i+1 ]" class="btn btn-secondary btn-sm">Details</a> </td>
	                </tr>
	            }
	        </tbody>
	    </table>

	    }
	</div>
	```

Wir sehen darin, dass der Wert für `routerLink` auch ein Array sein kann, dessen erster Eintrag die Route und dessen zweiter Eintrag eine anschließende `/id` sein kann. Der so beschriebene Wert ergibt dann die Routen `/cites/1`, `/cities/2` usw. Es hätte auch funktioniert, wenn wir `<a [routerLink]="'/cities/'+(i+1)">Detail</a>` geschrieben hätten. 

Die `cities.component.ts` sieht nun so aus: 

=== "cities.component.ts"
	```js linenums="1" hl_lines="28-30"
	import { Component, OnInit } from '@angular/core';
	import { ActivatedRoute, RouterLink } from '@angular/router';
	import { City } from '../shared/city';
	import { DataService } from '../shared/data.service';

	@Component({
	  selector: 'app-cities',
	  standalone: true,
	  imports: [RouterLink],
	  templateUrl: './cities.component.html',
	  styleUrl: './cities.component.css'
	})
	export class CitiesComponent implements OnInit {
	  id: string | null = "";
	  
	  staedte: City[] = [];
	  city: {id: number; jahr: number; stadt: string; link: string; bild: string } | null = null;
	  
	  constructor(private route: ActivatedRoute, private service: DataService) {
	    this.service.getAll()
	    .then( response => this.staedte = response)
	    .then( staedte => console.log('staedte geladen', staedte))
	  }

	  ngOnInit(): void {
	    this.id = this.route.snapshot.paramMap.get('id');
	    if(this.id) {
	        this.service.getOne(Number(this.id))
	        .then( response => this.city = response[0])
	        .then( stadt => console.log('city geladen', stadt))
	    }
	    else console.log('ohne Parameter');
	  }
	}
	```


### Neuladen bei neuer Route

Angenommen, wir erweitern die `city.component.html` um zwei weitere Navigationsbuttons, um zwischen den einzelnen Städten "zu blättern":


=== "cities.component.html"
	```html linenums="2" hl_lines="11 13"
    
    @if(city) {
        <h1>{{ city.stadt }} </h1>

        <div class="card" style="width: 20%">
            <img [src]="city.bild" class="card-img-top" [alt]="city.stadt">
            <div class="card-body">
              <h5 class="card-title">{{ city.stadt }}</h5>
              <p class="card-text">
                <a [href]="city.link">Weitere Informationen über {{ city.stadt }}</a>
              </p>
              <a [routerLink]="['/cities', city.id-1]" class="btn btn-primary m-1"> &lt; </a>
              <a routerLink="/cities" class="btn btn-primary m-1">Alle Städte</a>
              <a [routerLink]="['/cities', city.id+1]" class="btn btn-primary m-1"> &gt; </a>
            </div>
          </div>
    
    } @else {
	```

Wenn wir nun auf einen solchen Navigationsbutton klicken, dann sehen wir, dass sich im URL-Fenster die Route ändert. Jedoch erscheint keine neue Stadt. Das liegt daran, dass die Komponente nicht automatisch neu geladen wird, wenn sich nur der Routenparameter ändert. Der Parameter wird nur beim Initialisieren der Komponente ausgelesen (in `ngOnInit()`). Es lässt sich jedoch "beobachten", ob sich der Parameter ändert. `paramMap` von `ActivatedRoute` liefert einen sogenannten `Observer`. An diesen `Observer` kann man sich mithilfe von `subscribe()` anmelden. Sobald sich der `Observer` ändert, werden alle *Subscriber* darüber benachrichtigt. Wir ändern entsprechend die `city.component.ts`:

=== "cities.component.ts"
	```js linenums="1" hl_lines="20"
	import { Component, OnInit } from '@angular/core';
	import { ActivatedRoute, RouterLink } from '@angular/router';
	import { City } from '../shared/city';
	import { DataService } from '../shared/data.service';

	@Component({
	  selector: 'app-cities',
	  standalone: true,
	  imports: [RouterLink],
	  templateUrl: './cities.component.html',
	  styleUrl: './cities.component.css'
	})
	export class CitiesComponent implements OnInit {
	  id: string | null = "";
	  
	  staedte: City[] = [];
	  city: {id: number; jahr: number; stadt: string; link: string; bild: string } | null = null;
	  
	  constructor(private route: ActivatedRoute, private service: DataService) {
	    this.route.paramMap.subscribe( params => this.ngOnInit())
	    this.service.getAll()
	    .then( response => this.staedte = response)
	    .then( staedte => console.log('staedte geladen', staedte))

	    this.service.getOne(1)
	    .then( response => console.log('stadt geladen : ', response ))
	  }

	  ngOnInit(): void {
	    this.id = this.route.snapshot.paramMap.get('id');
	    if(this.id) {
	        this.service.getOne(Number(this.id))
	        .then( response => this.city = response[0])
	        .then( stadt => console.log('city geladen', stadt))
	    }
	    else console.log('ohne Parameter');
	  }
	}


	```

Wir haben den Code also nur um eine Zeile ergänzt. Wenn sich jetzt der Parameter der Route ändert, wird die `ngOnInit()`-Funktion einfach erneut aufgerufen. Nun funktioniert auch das Blättern zwischen den Städten.  


--- 

***der folgende Abschnitt muss noch überarbeitet werden; kommt in Kürze***

---

## Routen absichern mit Guards

*Guards* sind Funktionen, die entscheiden, ob ein Navigationsschritt ausgeführt werden darf oder nicht. Diese Entscheidung wird durch den Rückgabewert der Funktion ausgedrückt. Es gibt drei verschiedene Varainten für den Rückgabewert: 

- `true`: der Navigationsschritt wird ausgeführt, 
- `false`: der Navigationsschritt wird nicht ausgeführt, 
- Rückgabe vom Typ `URLTree`: die Navigation wird abgebrochen und eine Navigation zu einer anderen Route gestartet. 

*Guards* werden immer als Eigenschaft einer Route definiert, also bereits bei der Definition der Route im `routes`-Array in `app.routes.ts`. Es gibt vier verschiedene Guard-Typen:

- `CanAvtivate`: entscheidet, ob eine Route aktiviert werden darf,
- `CanAvtivateChild`: entscheidet, ob die Kind-Routen einer Route aktiviert werden dürfen (Kind-Routen haben wir uns bis jetzt noch nicht angeschaut),
- `CanDeaktivate`: entscheidet, ob eine Route deaktiviert werden darf,
- `CanLoad`: entscheidet, ob ein Module (asynchron) geladen werden darf. 

Uns genügt es, `CanActivate` zu betrachten. Damit wollen wir regulieren, dass nur eine bestimmte *Rolle* von Nutzern eine bestimmte Komponente verwenden darf. Wir erstellen uns einen solchen Guard mithilfe des Angular CLI und nennen den Guard `authguard`:

```bash
ng g guard authguard --implements CanActivate
```

Dadurch entsteht eine Datei `authguard.guard.ts` mit folgendem Inhalt:

=== "authguard.guard.ts"
	```js linenums="1"
	import { Injectable } from '@angular/core';
	import { ActivatedRouteSnapshot, CanActivate, RouterStateSnapshot, UrlTree } from '@angular/router';
	import { Observable } from 'rxjs';

	@Injectable({
	  providedIn: 'root'
	})
	export class AuthguardGuard implements CanActivate {
	  
	  canActivate(
	    route: ActivatedRouteSnapshot,
	    state: RouterStateSnapshot): Observable<boolean | UrlTree> | Promise<boolean | UrlTree> | boolean | UrlTree {
	    return true;
	  }
	  
	}

	```

Um dieses Beispiel etwas realistischer zu gestalten, erstellen wir noch einen `auth`-Service, der später unserer Nutzer- und Rollenverwaltung dient. Wir nennen ihn `auth` und erstellen ihn ebenfalls im `shared`-Ordner:

```bash
ng g service shared/auth
```

In diesen Service fügen wir nur eine dummy-Funktion `isAuthenticated()` ein, die ein `true` oder `false` zurückliefert:

=== "shared/auth.service.ts"
	```js linenums="1" hl_lines="10-12"
	import { Injectable } from '@angular/core';

	@Injectable({
	  providedIn: 'root'
	})
	export class AuthService {

	  constructor() { }

	  isAuthenticated(): boolean {
	    return false;
	  }
	}
	```

Diesen Service und davon insbesondere die `isAuthenticated`-Funktion verwenden wir in unserem `auth`-Guard:


=== "authguard.guard.ts"
	```js linenums="1"
	import { Injectable } from '@angular/core';
	import { ActivatedRouteSnapshot, CanActivate, Router, RouterStateSnapshot, UrlTree } from '@angular/router';
	import { AuthService } from './shared/auth.service';

	@Injectable({
	  providedIn: 'root'
	})
	export class AuthguardGuard implements CanActivate {

	  constructor(
	    private as: AuthService,
	    private router: Router
	  ) {}

	  canActivate(
	    route: ActivatedRouteSnapshot,
	    state: RouterStateSnapshot): boolean | UrlTree {
	    return this.as.isAuthenticated()
	      ? true
	      : this.router.parseUrl('/login');
	  }

	}
	```

Erläuterungen der Anpassungen:

- Zunächst haben wir die Rückgabetypen der `canActivate()`-Funktion auf `boolean` und `UrlTree` reduziert. Die anderen möglichen Rückgabetypen `Observable<boolean | UrlTree> | Promise<boolean | UrlTree>` haben wir gelöscht (und somit auch `import { Observable } from 'rxjs';`) - siehe Zeile `17`.
- Dann haben wir den `AuthService` und auch das `Router`-Modul per *dependency injection* in den Konstruktor der `AuthGuard`-Klasse eingefügt, um Beides verwenden zu können (Zeilen `10-13`). 
- Dann haben wir die Berechnung des Rückgabewertes der `canActivate`-Funktion ergänzt. Der Rückgabewert ist abhängig vom Rückgaewert der `isAuthenticated()`-Funktion des `AuthServices`. Liefert diese Funktion ein `true` zurück, dann gibt auch die `canActivate()`-Funktion ein `true` zurück (Zeile `19`). Ist der Rückgabewert jedoch `false`, dann liefert die `canActivate()`-Funktion ein `UrlTree` in der Form zurück, dass die Navigation auf die Route `/login` umgeleitet wird. 

Jetzt können wir diesen Guard verwenden und passen dafür die `app.routes.ts` an. Wir wollen hier exemplarisch demonstrieren, dass die `/cities`- und `/cities/:id`-Routen nur dann aktiviert werden können, wenn die `canActivate()`-Funktion des `AuthGuard`s ein `true` zurückliefert. Dazu sind folgende Änderungen in der `app.routes.ts` notwendig: 

=== "app.routes.ts"
	```js linenums="1" hl_lines="5"
	import { AuthguardGuard } from './authguard.guard';
	import { CityComponent } from './cities/city/city.component';
	import { HomeComponent } from './home/home.component';
	import { LoginComponent } from './login/login.component';
	import { AboutComponent } from './about/about.component';
	import { NgModule } from '@angular/core';
	import { RouterModule, Routes } from '@angular/router';
	import { CitiesComponent } from './cities/cities.component';

	const routes: Routes = [
	  {
	    path: "",
	    component: HomeComponent,
	    pathMatch: 'full'
	  },
	  {
	    path: "about",
	    component: AboutComponent
	  },
	  {
	    path: "login",
	    component: LoginComponent
	  },
	  {
	    path: "cities",
	    component: CitiesComponent,
	    canActivate: [AuthguardGuard]
	  },
	  {
	    path: "cities/:id",
	    component: CityComponent,
	    canActivate: [AuthguardGuard]
	  }
	];

	@NgModule({
	  declarations: [],
	  imports: [
	    RouterModule.forRoot(routes)
	  ],
	  exports: [RouterModule],
	  providers: []
	})
	export class AppRoutingModule { }

	```


Wenn wir nun auf `/cities` navigieren wollen, dann werden wir direkt auf die `/login`-Route umgeleitet. Die `CitiesComponent` und auch die `CityComponent` bleiben gesperrt solange `isAuthenticated()` ein `false` zurückliefert. 

!!! success
	Wir haben die wesentlichsten Konzepte des Routing kennengelernt. Darüber hinaus gibt es noch Themen für Fortgeschrittene, wie z.B. lazy-loading von Modulen (Module erst dann laden, wenn man sie wirklich erst aufruft), Routen für Kindkomponenten, mehrere outlets usw. Aber uns genügen die hier erläuterten wesentlichen Konzepte. 