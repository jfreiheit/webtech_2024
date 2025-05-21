# Web-Technologien

Herzlich willkommen zur WebTech-Veranstaltung im Sommersemester 2025! 

### Grober Inhalt

In dieser Veranstaltung lernen Sie, was das World Wide Web ist und wie man eigene Webseiten und -anwendungen realisiert. Sie lernen die Protokolle und Sprachen ``http``, ``HTML``, ``CSS``, ``JavaScript`` und `TypeScript` kennen und machen sich mit ``Angular``, ``Node.js`` und ``REST`` vertraut. Zentrales Thema ist der sogenannte [MEAN](https://www.ibm.com/cloud/learn/mean-stack-explained)-Stack, d.h. Sie lernen die Entwicklung mithilfe von <b>M</b>ongoDB, <b>E</b>xpress.js, <b>A</b>ngular und <b>N</b>ode.js kennen. Allerdings verwenden wir statt `MongoDB` hier als Datenbank `PostgreSQL`, um dichter an unserem Datenbankmodul im Studiengang zu sein. Der Stack heißt komischerweise trotzdem `MEAN` (und nicht `PEAN`). 

Nachfolgend der vorläufige Wochenplan (wird eventuell angepasst). 

| | Woche | Themen (Vorlesung) | Übung | Aufgabe (Stand) | Abgabe Übung bis | 
|-|-------|--------------------|-------|-----------------|------------------|
| 1. | 07.-11.04.2025 | [Einführung](einfuehrung.md#webtechnologien-einfuhrung) und [Organisatorisches](#organisatorisches) | [Übung 0](uebungen.md#ubung-0) | - | - | 
| 2. | 14.-18.04.2025 | [HTML](html.md) | [Übung 1](uebungen.md#ubung-1) | Idee | 22.04.2025 | 
| 3. | 21.-25.04.2025 | [CSS (Eigenschaften und Selektoren](css.md#css) | [Übung 2](uebungen.md#ubung-2) | - | 29.04.2025 | 
| 4. | 28.-02.05.2025 | [CSS (Grid)](css.md#grid) | [Übung 3](uebungen.md#ubung-3) | Konzept | 06.05.2025 | 
| 5. | 05.-09.05.2025 | [RWD (responsive Webdesign)](rwd.md#responsive-web-design) | [Übung 4](uebungen.md#ubung-4) | - | 13.05.2025 | 
| 6. | 12.-16.05.2025 | [JavaScript (DOM)](javascript.md#javascript) | [Übung 5](uebungen.md#ubung-5) | Datenmodell | 20.05.2025 | 
| 7. | 19.-23.05.2025 | [Angular (Einführung und Komponenten)](angular.md#angular) | [Übung 6](uebungen.md#ubung-6) | Schnittstelle | 27.05.2025 | 
| 8. | 26.-30.05.2025 | [Templates (Bindings)](templates.md#templates-bindings) | [Übung 7](uebungen.md#ubung-7) | Frontend (c+r)| 03.06.2025 | 
| 9. | 02.-06.06.2025 | [Angular (Routing und Services)](routing.md#routing-und-services) | [Übung 8](uebungen.md#ubung-8) | Frontend (u+d)| 10.06.2025 | 
| 10. | 09.-13.06.2025 | [Node.js + Express (REST-Server PostgreSQL)](backend_pg.md#rest-api) |  [Übung 9](uebungen.md#ubung-9)| Frontend fertig | 17.06.2025 | 
| 11. | 16.-20.06.2025 | [Angular (Anbindung ans Backend)](fe-be-anbindung.md#frontend-backend-anbindung) | [Übung 10](uebungen.md#ubung-10) | Backend ( c ) | 24.06.2025 | 
| 12. | 23.-27.06.2025 | [Nutzerverwaltung und Material](guards.md#subject-observable-observer-und-guards) | - | Backend (r + u) | 01.07.2025 |
| 13. | 30.-04.07.2025 | Signals  | - | Backend (d + fertig)| 08.07.2025 |
| 14. | 07.-11.07.2025 | Wiederholung | - | fertig stellen | 15.07.2025 |
| 15. | 14.-18.07.2025 | - | Fragen | - | - |
| 16. | 21.-25.07.2025 | - | Fragen | Abgabe 1.PZ 23.7.2025, Gespräche 24.7.2025  |
|  |  |  |  |Abgabe 2.PZ 23.9.2025, Gespräche 24.9.2025 (evtl. auch 25.9.2025)| - |


Die Erfahrung zeigt, dass die Mehrheit der Abgeben im 2.PZ erfolgt. Sie sollten allerdings bedenken, dass es zwischen dem 1. und dem 2.PZ keine Konsultationen gibt. 

### Organisatorisches 

Zur erfolgreichen Durchführung der Veranstaltung müssen Sie die Übungen lösen und zu den jeweiligen Fristen per Git auf einen Server (GitHub oder GitLab) laden. Am Ende des Semesters ist eine Aufgabe abzugeben. Diese Aufgabe wird bewertet. Die Bewertung entspricht dann der Modulnote. 

[Hier](uebungen.md#ubungen) sind die Übungen beschrieben, die Sie in jeder Woche ausführen sollen. Damit Sie dies erfolgreich erledigen können, ist jeweils angegeben, welche Themen Sie dafür durcharbeiten müssen. Das Durcharbeiten der jeweiligen Themen entspricht jeweils einer Vorlesung. Diese wird also selbständig durchgeführt. 

Für die Kommunikation untereinander verwenden wir [**Slack**](https://slack.com/intl/de-de/). Dort können Sie alle inhaltlichen und organisatorischen Fragen stellen. Ich fände es gut, wenn ich dort möglichst wenig Fragen - zumindest die inhaltlichen - beantworten müsste, sondern eine Art internes Diskussionsforum entsteht. Es ist sehr gewünscht, dort Fragen zu stellen und noch mehr gewünscht, diese von Ihnen dort beantwortet zu sehen. Damit wäre allen geholfen und ich kann besser erkennen, wo noch Nachhol- bzw. Erläuterungsbedarf bei den meisten besteht.  

## Code aus der Vorlesung

??? question "Code aus HTML-Vorlesung"
	=== "index.html"
		```html
		<!DOCTYPE html>
		<html lang="en">
		<head>
		  <meta charset="UTF-8">
		  <meta name="viewport" content="width=device-width, initial-scale=1.0">
		  <title>Erste HTML-Seite</title>
		</head>
		<body>
		  <header>
		    <h1>Willkommen zu meiner ersten HTML-Seite!</h1>
		    <h2>etwas kleinere Überschrift</h2>
		    <h3>noch kleiner</h3>
		    <h6>am kleinsten</h6>
		  </header>

		  <main>
			<p id="p1" class="rotHG gelbFont kursiv">hier ist ein Absatz. </p>
			<a href="https://www.htw-berlin.de">HTW Berlin</a>
			<a href="./html/seite1.html">Seite 1</a>
			<img src="./images/fiw.jpg" alt="FIW-Logo" width="200" />
			<!--  
			  kommentar 
			  

			  kommentar
			-->
			<ul>
			  <li>erster Punkt</li>
			  <li>zweiter Punkt</li>
			</ul>
			<ol>
			  <li><h1>eins</h1></li>
			  <li>zwei</li>
			  <li>drei
			    <ul>
			      <li>Unterpunkt 1</li>
			      <li>Unterpunkt 2</li>
			    </ul>
			  </li>
			  <li>vier</li>
			</ol>

			<table>
			  <thead>
			    <tr>
			      <th>Spalte 1</th>
			      <th>Spalte 2</th>
			      <th>Spalte 3</th>
			    </tr>
			  </thead>
			  <tbody>
			    <tr>
			      <td>eins eins</td>
			      <td>eins zwei</td>
			      <td>eins drei</td>
			    </tr>
			    <tr>
			      <td>zwei eins</td>
			      <td>zwei zwei</td>
			      <td>zwei drei</td>
			    </tr>
			    <tr>
			      <td>drei eins</td>
			    </tr>
			    <tr>
			      <td></td>
			      <td>vier zwei</td>
			      <td>vier drei</td>
			    </tr>
			  </tbody>
			</table>
		  </main>
		  <footer>
		    <input type="text" />
		    <input type="password" />
		    <input type="checkbox" />
		    <input type="radio" />
		    <input type="button" value="Login" />
		    <input type="datetime-local" />
		    <input type="range" min="0" max="100" value="10" />
		    <input type="color">
		  </footer>
		</body>
		</html>
		```
	=== "html/seite1.html"
		```html
		<!DOCTYPE html>
		<html lang="en">
		<head>
		  <meta charset="UTF-8">
		  <meta name="viewport" content="width=device-width, initial-scale=1.0">
		  <title>Seite</title>
		</head>
		<body>
		  <h4>Seite 1</h4>
		  <a href="../index.html">zurück zur index.html</a>
		  <img src="../images/htw.jpg" alt="HTW-Logo" width="200"/>
		</body>
		</html>
		```

??? question "Code aus CSS-Vorlesung"
	=== "01_cascading.html"
		```html
		<!DOCTYPE html>
		<html lang="en">
		<head>
		    <meta charset="UTF-8">
		    <meta http-equiv="X-UA-Compatible" content="IE=edge">
		    <meta name="viewport" content="width=device-width, initial-scale=1.0">
		    <title>Cascading</title>
		    <!-- Einbinden von CSS per externer css-Datei-->
		    <link rel="stylesheet" href="../styles/mystyles.css">
		    <style>
		       h1 {
		        text-transform: lowercase;  /* CSS-Kommentare */
		        font-style: italic;
		       }
		       
		       ol {
		        color: blue;
		       }

		       .fgYellow {
		        color: yellow;
		       }

		       /*
		       .bgBrown {
		        background-color: brown;
		       }
		        */

		       .freigewaehlt {
		        font-size: 2em;
		       }

		       #firstH2 {
		        text-decoration: underline;
		       }

		       article p {
		        color: red;
		       }

		       section>p {
		        color: green;
		       }

		       a {
		        text-decoration: none;
		       }

		       a:hover {
		        background-color: blue;
		        color: white;
		       }

		       p::first-letter {
		        font-size: 3em;
		       }

		    </style>
		</head>
		<body>
		    <header>
		        <h1 style="background-color: rgb(50, 140, 140); color: rgb(249, 245, 245);">Cascading Style Sheets - CSS</h1>
		    </header>
		    <main>
		        <section>
		            <h2 id="firstH2">Section 1</h2>
		            <article>
		                <p class="fgYellow bgBrown freigewaehlt">Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam, quae.</p>
		                <p class="fgYellow bgBrown">Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam, quae.</p>
		            </article>
		            <article class="bgBrown">
		                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam, quae.</p>
		                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam, quae.</p>
		            </article>
		            <p>direktes Kind einer section</p>
		        </section>
		        <section>
		            <h2>Section 2</h2>
		            <article>
		                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam, quae.</p>
		                hallo ballo
		                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam, quae.</p>
		            </article>
		            <article>
		                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam, quae.</p>
		                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam, quae.</p>
		            </article>
		        </section>
		        <ol>
		            <li>item 1
		                <ul>
		                    <li>subitem</li>
		                    <li>subitem</li>
		                    <li>subitem</li>
		                </ul>
		            </li>
		            <li>item 2</li>
		            <li>item 3</li>
		            <li>item 4</li>
		            <li>item 5</li>
		        </ol>
		    </main>
		    <aside>
		        <h2>Aside</h2>
		        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam, quae.</p>
		        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam, quae.</p>
		    </aside>
		    <footer>
		        <p>
		            <a href="./02_boxmodel.html">Boxmodel</a>&nbsp;&middot;&nbsp;
		            <a href="./03_rangfolge.html">Rangfolge</a>
		            <a href="https://www.htw-berlin.de">HTW Berlin</a>

		        </p>
		    </footer>

		</body>
		</html>
		```
	=== "02_boxmodel.html"
		```html
		<!DOCTYPE html>
		<html lang="en">
		<head>
		    <meta charset="UTF-8">
		    <meta http-equiv="X-UA-Compatible" content="IE=edge">
		    <meta name="viewport" content="width=device-width, initial-scale=1.0">
		    <title>Box-Model</title>
		    <style>
		      * {
		        box-sizing: content-box;  /* Standard */
		      }

		      img {
		        border: 1px solid black;
		        margin: 100px;
		    }
		      div {
		          width: 322px;
		          padding: 30px;
		          border: 5px solid gray;
		          margin: 0;
		      }
		    </style>
		</head>
		<body>
		    <header>
		        <h1>Box-Model</h1>
		    </header>
		    <main>
		        <img src="../images/fiw.jpg" alt="fiw logo" style="width:350px"/>
		        <div>Das FIW-Logo hat eine Breite von 350px (width:350px).
		            Der Inhalt dieser Box hat eine Breite von 320px.
		            Dazu kommt padding von 10px (auf beiden Seiten)
		            und ein Rahmen mit der Breite von 5px. Macht zusammen
		            350px.
		        </div>
		    </main>
		    <footer>
		        <p><a href="./01_cascading.html">Einführung</a>&nbsp;&middot;&nbsp;<a href="./03_rangfolge.html">Rangfolge</a></p>
		    </footer>

		</body>
		</html>
		```
	=== "03_rangfolge.html"
		```html
		<!DOCTYPE html>
		<html lang="en">
		<head>
		    <meta charset="UTF-8">
		    <meta http-equiv="X-UA-Compatible" content="IE=edge">
		    <meta name="viewport" content="width=device-width, initial-scale=1.0">
		    <title>Reihenfolge Selektoren</title>
		    <style>
		      a:link {
		        color: blue; 
		      }

		      .link {
		        color: green;
		      }
		      #navigation a {
		        color: red;
		      }

		      li a {
		        color: magenta;
		      }
		    </style>
		</head>
		<body>
		    <header>
		        <h1>Reihenfolge Wirkung Selektoren</h1>
		    </header>
		    <main>
		        <h4>Test</h4>
		        <ul id="navigation">
		            <li><a href="./01_cascading.html" class="link">Einführung</a></li>
		            <li><a href="./02_boxmodel.html" class="link">Boxmodel</a></li>
		        </ul>
		        <h4>Prinzip</h4>
		        <dl>
		            <dt><em>Kategorie A</em></dt>
		            <dd>erhält den Wert 1, wenn CSS-Definitionen direkt im style-Attribut eines HTML-Elementes notiert sind</dd>
		            <dt><em>Kategorie B</em></dt>
		            <dd>erhält den Wert 1 bei Selektoren für Elemente mit id-Attributen</dd>
		            <dt><em>Kategorie C</em></dt>
		            <dd>Anzahl der von einem Selektor betroffenen Klassen und Pseudoklassen</dd>
		            <dt><em>Kategorie D</em></dt>
		            <dd>Anzahl der von einem Selektor betroffenen Elementnamen und Pseudo-Elemente</dd>
		        </dl>
		        <ol>
		            <li>Bei der Reihenfolge der Sortierung gilt: A > B > C > D, also z.B. 1 0 0 0 vor (größer als) 0 1 2 2.</li>
		            <li>Bei Gleichheit gilt die letzte Definition</li>
		        </ol>
		    </main>
		    <footer>
		        <p><a href="./02_boxmodel.html">Boxmodel</a>&nbsp;&middot;&nbsp;<a href="./01_cascading.html">Einführung</a></p>
		    </footer>

		</body>
		</html>
		```
	=== "04_display.html"
		```html
		<!DOCTYPE html>
		<html lang="en">
		<head>
		    <meta charset="UTF-8">
		    <meta name="viewport" content="width=device-width, initial-scale=1.0">
		    <title>display</title>
		    <style>
		      p {
		            color: red;
		      }

		    p.ex1 {
		        display: none;
		    }

		    p.ex2 {
		        display: inline;
		    }

		    p.ex4 {
		        display: inline-block;
		    }
		    </style>
		</head>
		<body>
		<header>
		    <nav>
		<ul>
		    <li><a href="./02_boxmodel.html">Boxmodel</a></li>
		    <li><a href="./01_cascading.html">Cascading</a></li>
		    <li><a href="#">Display</a></li>
		    <li><a href="./05_grid">Grid</a></li>
		</ul>
		    </nav>
		</header>
		<main>
		<h1>The display Property</h1>

		<h2>display: none:</h2>
		<div>
		Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam semper diam at erat pulvinar, at pulvinar felis blandit. <p class="ex1">none!</p> Vestibulum volutpat tellus diam, consequat gravida libero rhoncus ut.
		</div>

		<h2>display: inline:</h2>
		<div>
		Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam semper diam at erat pulvinar, at pulvinar felis blandit. <p class="ex2">inline!</p> Vestibulum volutpat tellus diam, consequat gravida libero rhoncus ut.
		</div>

		<h2>display: block:</h2>
		<div>
		Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam semper diam at erat pulvinar, at pulvinar felis blandit. <p class="ex3">block!</p> Vestibulum volutpat tellus diam, consequat gravida libero rhoncus ut.
		</div>

		<h2>display: inline-block:</h2>
		<div>
		Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam semper diam at erat pulvinar, at pulvinar felis blandit. <p class="ex4">neue Zeile und dann inline!</p> Vestibulum volutpat tellus diam, consequat gravida libero rhoncus ut.
		</div>   

		<ul>
		    <li><a href="https://developer.mozilla.org/en-US/docs/Web/CSS/display?retiredLocale=de">Gibt noch sehr viele andere</a></li>
		    <li><a href="./index.html">Zurück</a></li>
		</ul>
		</main>
		    <footer>

		    </footer>
		</body>
		</html>
		```


??? question "Code aus der Layout/RWD-Vorlesung"
	=== "05_grid.html"
		```html
		<!DOCTYPE html>
		<html lang="en">
		<head>
		    <meta charset="UTF-8">
		    <meta http-equiv="X-UA-Compatible" content="IE=edge">
		    <meta name="viewport" content="width=device-width, initial-scale=1.0">
		    <title>CSS-Grid</title>
		    <style>

		        .orange {
		            background-color: orange;
		            opacity: 0.5;
		            border: 2px solid gray;
		            border-radius: 5px;
		            padding: 30px;
		        }

		        .wrapper {
		            display: grid;
		            grid-template-columns: repeat(3, 1fr);
		            grid-template-rows: repeat(4, 1fr);
		        }

		        .one {
		            /* grid-column-start: 1;
		            grid-column-end: 3; */
		            grid-column: 1/3;
		            /* grid-row-start: 2;
		            grid-row-end: 4; */
		            grid-row: 2 / 4;
		        }

		        .two {
		            grid-column: 2;
		            grid-row: 2;
		        }




		    </style>
		</head>
		<body>
		    <header>
		        <h1>CSS-Grid</h1>
		    </header>
		    <main class="wrapper">
		        <div class="one orange">One</div>
		        <div class="two orange">Two</div>
		        <div class="three orange">Three</div>
		        <div class="four orange">Four</div>
		        <div class="five orange">Five</div>
		        <div class="six orange">Six</div>
		    </main>
		    <footer>
		        <p><a href="https://www.w3schools.com/cssref/pr_grid.php">grid</a></p>
		        <p><a href="https://www.w3schools.com/cssref/pr_grid-template-columns.php">grid-template-columns</a></p>
		        <p><a href="https://css-tricks.com/introduction-fr-css-unit/">fr - fraction</a></p>
		        <p><a href="./index.html">Zurück</a></p>
		    </footer>

		</body>
		</html>
		```
	=== "rwd1.html"
		```html
		<!DOCTYPE html>
		<html lang="en">

		<head>
		    <meta charset="UTF-8">
		    <meta http-equiv="X-UA-Compatible" content="IE=edge">
		    <meta name="viewport" content="width=device-width, initial-scale=1.0">
		    <title>Document</title>
		    <style>

		        div {
		            width: 100vw;
		            height: 100vh;
		            text-align: center;
		            background-color: red;
		            padding-top: 20%;
		            padding-bottom: 20%;
		            font-size: medium;
		        }

		        @media (min-width: 800px) {
		            div {
		                background-color: blue;
		                color: white;
		            }
		        }



		        @media (min-width: 1200px) {
		            div {
		                background-color: green;
		                color: yellow;
		                font-style: italic;
		            }
		        }


		    </style>
		</head>

		<body>
		    <div>Ändern Sie die Breite des Browsers, um den Effekt zu sehen.</div>
		</body>

		</html>
		```
	=== "rwd2.html"
		```html
		<!DOCTYPE html>
		<html lang="en">

		<head>
		    <meta charset="UTF-8">
		    <meta name="viewport" content="width=device-width, initial-scale=1">
		    <title>Responsive Webdesign</title>
		    <style>
		        .small {
		            display: grid;
		            grid-template-columns: 1fr;
		            column-gap: 2%;
		            row-gap: 2%;
		        }

		        @media (min-width: 800px) {
		            .medium  {
		                display: grid;
		                grid-template-columns: 1fr 1fr;
		            }
		        }

		        @media (min-width: 1200px) {
		            .large  {
		                display: grid;
		                grid-template-columns: repeat(4, 1fr);
		            }
		        }
		    </style>
		</head>

		<body>
		    <main class="small medium large">
		        <p>
		            Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata
		            sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et
		            ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua.
		            At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore
		            eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi. Lorem ipsum dolor sit amet,
		        </p>
		        <p>
		            Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata
		            sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et
		            ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua.
		            At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore
		            eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi. Lorem ipsum dolor sit amet,
		        </p>
		        <p>
		            Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata
		            sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et
		            ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua.
		            At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore
		            eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi. Lorem ipsum dolor sit amet,
		        </p>
		        <p>
		            Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata
		            sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et
		            ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua.
		            At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore
		            eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi. Lorem ipsum dolor sit amet,
		        </p>
		    </main>
		</body>

		</html>

		```


??? question "Code aus der Bootstrap-Vorlesung"
	=== "bootstrap.html"
		```html
		<!DOCTYPE html>
		<html lang="en">

		<head>
		    <meta charset="UTF-8">
		    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
		    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.6/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-4Q6Gf2aSP4eDXB8Miphtr37CMZZQ5oXLH2yaXMJ2w8e2ZtHTl7GptT4jmndRuHDT" crossorigin="anonymous">
		    <title>Bootstrap</title>
		    <style>
		        .my-bg {
		            background-color: red;
		        }
		    </style>
		</head>

		<body>
		    <main role="main">
		        <div class="p-5 mb-4 bg-warning rounded-3">
		            <div class="container-fluid py-5">
		                <h1 class="display-5 fw-bold">Jetzt mit Bootstrap!</h1>
		                <p class="col-md-8 fs-4">Wir verwenden jetzt Bootstrap und schauen uns mal die Anwendung ein wenig genauer an. Das Grundprinzip besteht darin, HTML-Elementen Klassen zuzuordnen. </p>
		                <p><a class="btn btn-secondary btn-lg" href="https://getbootstrap.com/docs/5.3/examples/" role="button">Bootstrap Beispiele &raquo;</a></p>
		            </div>
		        </div>

		        <a class="btn btn-secondary my-bg">Hallo</a>

		        <div class="container">
		            <h2>Formular mit Validierung, ob Eingabe erfolgte (nur mit CSS - kein JavaScript!)</h2>
		            <p>Hier wird z.B. die Klasse <code>.was-validated</code> verwendet, um zu überprüfen, ob in den Textfeldern und der Checkbox eine Eingabe erfolgt ist.</p>
		            <form class="was-validated">
		                <div class="form-group">
		                    <label for="uname">Username:</label>
		                    <input type="text" class="form-control" id="uname" placeholder="Enter username" name="uname" required>
		                    <div class="valid-feedback">Korrekt</div>
		                    <div class="invalid-feedback">Feld bitte ausfüllen!</div>
		                </div>
		                <div class="form-group">
		                    <label for="pwd">Password:</label>
		                    <input type="password" class="form-control" id="pwd" placeholder="Enter password" name="pswd" required>
		                    <div class="valid-feedback">Korrekt</div>
		                    <div class="invalid-feedback">Feld bitte ausfüllen!</div>
		                </div>
		                <div class="form-group form-check">
		                    <label class="form-check-label">
		                    <input class="form-check-input" type="checkbox" name="remember" required> Ich habe die Datenschutzerklärung gelesen und stimme ihr zu.
		                    <div class="valid-feedback">Korrekt</div>
		                    <div class="invalid-feedback">Hier bitte bestätigen!</div>
		                </label>
		                </div>
		                <button type="submit" class="btn btn-primary">Login</button>
		            </form>
		        </div>
		    </main>
		</body>

		</html>
		```
	=== "bs_grid.html"
		```html
		<!DOCTYPE html>
		<html lang="en">

		<head>
		    <meta charset="UTF-8">
		    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
		    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.6/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-4Q6Gf2aSP4eDXB8Miphtr37CMZZQ5oXLH2yaXMJ2w8e2ZtHTl7GptT4jmndRuHDT" crossorigin="anonymous">
		    <title>Grid</title>
		    <style>
		        div div {
		            padding: 10px;
		        }
		    </style>
		</head>

		<body>
		    <main class="container pt-5 ">
		        <h2>Wichtig ist, dass die Spaltenanzahl in einer Zeile 12 ergibt</h2>
		        <div class="row">
		            <div class="col-1" style="background-color: lightgrey;">
		                <h3>col-3</h3>
		                <p>Diesem &lt;div&gt; wurde die Klasse <code>col-3</code> zugewiesen</p>
		            </div>
		            <div class="col-6" style="background-color: darkgrey;">
		                <h3>col-4</h3>
		                <p>Diesem &lt;div&gt; wurde die Klasse <code>col-4</code> zugewiesen</p>
		            </div>
		            <div class="col-1" style="background-color: grey;">
		                <h3>col-5</h3>
		                <p>Diesem &lt;div&gt; wurde die Klasse <code>col-5</code> zugewiesen</p>
		            </div>
		        </div>
		    </main>
		</body>

		</html>
		```
	=== "bs_responsive.html"
		```html
		<!DOCTYPE html>
		<html lang="en">

		<head>
		    <meta charset="UTF-8">
		    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
		    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.6/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-4Q6Gf2aSP4eDXB8Miphtr37CMZZQ5oXLH2yaXMJ2w8e2ZtHTl7GptT4jmndRuHDT" crossorigin="anonymous">
		    <title>Grid</title>
		    <style>
		        div div {
		            padding: 10px;
		            margin-top: 5px;
		            margin-bottom: 5px;
		        }

		        .row div:nth-child(odd) {
		            background-color: lightgrey;
		            color: black;
		        }

		        .row div:nth-child(even) {
		            background-color: grey;
		            color: white;
		        }
		    </style>
		</head>

		<body>
		    <main class="container pt-5 ">
		        <h2>Jetzt responsiv - ändern Sie die Monitorbreite</h2>
		        <div class="row">
		            <div class="col-12 col-sm-6 col-md-4 col-lg-3 col-xl-2">
		                <ul>
		                    <li>xs: <code>col-12</code> 1/1</li>
		                    <li>sm: <code>col-sm-6</code> 1/2</li>
		                    <li>md: <code>col-md-4</code> 1/3</li>
		                    <li>lg: <code>col-lg-3</code> 1/4</li>
		                    <li>xl: <code>col-xl-2</code> 1/6</li>
		                </ul>
		            </div>
		            <div class="col-12 col-sm-6 col-md-4 col-lg-3 col-xl-2">
		                <ul>
		                    <li>xs: <code>col-12</code> 1/1</li>
		                    <li>sm: <code>col-sm-6</code> 2/2</li>
		                    <li>md: <code>col-md-4</code> 2/3</li>
		                    <li>lg: <code>col-lg-3</code> 2/4</li>
		                    <li>xl: <code>col-xl-2</code> 2/6</li>
		                </ul>
		            </div>
		            <div class="col-12 col-sm-6 col-md-4 col-lg-3 col-xl-2">
		                <ul>
		                    <li>xs: <code>col-12</code> 1/1</li>
		                    <li>sm: <code>col-sm-6</code> 1/2</li>
		                    <li>md: <code>col-md-4</code> 3/3</li>
		                    <li>lg: <code>col-lg-3</code> 3/4</li>
		                    <li>xl: <code>col-xl-2</code> 3/6</li>
		                </ul>
		            </div>
		            <div class="col-12 col-sm-6 col-md-4 col-lg-3 col-xl-2">
		                <ul>
		                    <li>xs: <code>col-12</code> 1/1</li>
		                    <li>sm: <code>col-sm-6</code> 2/2</li>
		                    <li>md: <code>col-md-4</code> 1/3</li>
		                    <li>lg: <code>col-lg-3</code> 4/4</li>
		                    <li>xl: <code>col-xl-2</code> 4/6</li>
		                </ul>
		            </div>
		            <div class="col-12 col-sm-6 col-md-4 col-lg-6 col-xl-2">
		                <ul>
		                    <li>xs: <code>col-12</code> 1/1</li>
		                    <li>sm: <code>col-sm-6</code> 1/2</li>
		                    <li>md: <code>col-md-4</code> 2/3</li>
		                    <li>lg: <code>col-lg-6</code> 1/2</li>
		                    <li>xl: <code>col-xl-2</code> 5/6</li>
		                </ul>
		            </div>
		            <div class="col-12 col-sm-6 col-md-4 col-lg-6 col-xl-2">
		                <ul>
		                    <li>xs: <code>col-12</code> 1/1</li>
		                    <li>sm: <code>col-sm-6</code> 2/2</li>
		                    <li>md: <code>col-md-4</code> 3/3</li>
		                    <li>lg: <code>col-lg-6</code> 2/2</li>
		                    <li>xl: <code>col-xl-2</code> 6/6</li>
		                </ul>
		            </div>
		        </div>
		    </main>
		</body>

		</html>

		```



??? question "Code aus der JavaScript-Vorlesung"
	=== "01_index.html"
		```html
		<!DOCTYPE html>
		<html lang="en">
		<head>
		    <meta charset="UTF-8">
		    <meta name="viewport" content="width=device-width, initial-scale=1.0">
		    <title>JavaScript</title>

		</head>
		<body>
		    <h1>JavaScript</h1>
		    <main>
		        <h4>Eigenschaften</h4>
		        <ul>
		            <li>Skriptsprache (aus Performanzgründen aber compiliert - z.B. V8 in Chrome, SpiderMonkey in Firefox)</li>
		            <li>dynamische Typisierung</li>
		            <li>keine unterschiedlichen Referenztypen</li>
		            <li>Vererbung durch <code>prototype</code></li>
		            <li>Objekteigenschaften und -funktionen können einfach dem Objekt hinzugefügt werden</li>
		        </ul>
		        <h4>Nützliche Links</h4>
		        <ul>
		            <li><a href="https://www.ecma-international.org/publications-and-standards/standards/ecma-262/">ECMA-262</a></li>
		            <li><a href="https://dom.spec.whatwg.org/">Document Object Model (DOM)</a></li>
		            <li><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide">JavaScript Guide</a></li>
		            <li><a href="https://www.w3schools.com/js/default.asp">JavaScript Tutorial</a></li>
		            <li><a href="https://learnjavascript.online/">Learn JavaScript</a></li>
		            <li><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference">JavaScript Reference</a></li>
		        </ul>
		        <h4>Ergebnisliste</h4>
		        <ul id="ulresult">
		            <li id="liresult1"></li>
		        </ul>
		        <input type="text" id="input" oninput="inputFunc()" onfocus="changeColor('yellow')" onblur="changeColor('white')" placeholder="Name"/>
		        <button type="button" onclick="helloFIW()">Klick Mich!</button>
		    </main>
		    <script>
		        function changeColor(color) {
		            let inputElement = document.querySelector('#input')
		            console.log('changeColor() : ', inputElement)
		            inputElement.style.backgroundColor = color
		        }

		        function inputFunc() {
		            let inputElement = document.getElementById('input')
		            console.log(inputElement.value)
		            let li1 = document.getElementById('liresult1')
		            li1.textContent = inputElement.value
		            li1.style.color = "red"
		        }

		        function helloFIW(name='World') {
		            const mark = "!"
		            console.log(`Hello ${name}${mark}`)
		        }

		        function test(a, b) {
		            return a + b;
		        }

		        let test2 = (a, b) => a + b

		        let test1 = test;

		        console.log("3+4=" + test(3,4));
		        console.log("3+4=" + test1(3,4));
		        console.log("3+4=" + test2(3,4));
		    </script>
		</body>
		</html>
		```
	=== "02_object.html"
		```html
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
		                <input type="range" class="form-range" min="0" max="360" id="hueIP" oninput="setNewColor()" value="50">
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
		                <input type="range" class="form-range" min="0" max="100" id="satIP" oninput="setNewColor()" value="50">
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
		                <input type="range" class="form-range" min="0" max="100" id="lightIP" oninput="setNewColor()" value="50">
		            </div>
		        </div>
		    </div>
		   <script>
		    function setBackgroundColorDiv() {
		        let colorHSL = {
		            hue: 50,
		            saturation: 50,
		            lightness: 50,
		            getColor: () => `hsl(${colorHSL.hue}, ${colorHSL.saturation}%, ${colorHSL.lightness}%)`
		        }

		        let div = document.getElementById('output');

		        
		        let cHSLJSON = JSON.stringify(colorHSL) ;
		        console.log('json : ', cHSLJSON);

		        let cHSLObj = JSON.parse(cHSLJSON);
		        console.log('objekt : ', cHSLObj);
		        
		        
		        div.style.backgroundColor = colorHSL.getColor();
		    }

		    function setNewColor() {
		        let colorHSL = {
		            hue: document.querySelector('#hueIP').value,
		            saturation: document.querySelector('#satIP').value,
		            lightness: document.querySelector('#lightIP').value,
		            getColor: () => `hsl(${colorHSL.hue}, ${colorHSL.saturation}%, ${colorHSL.lightness}%)`
		        }
		        document.getElementById('hueOP').value = colorHSL.hue;
		        document.getElementById('satOP').value = colorHSL.saturation;
		        document.getElementById('lightOP').value = colorHSL.lightness;
		        let div = document.getElementById('output');
		        div.style.backgroundColor = colorHSL.getColor();
		    }
		   </script>
		</body>
		</html>
		```
	=== "03_create.html"
		```html
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
		<body class="container">
		    <h1>Formular auslesen</h1>
		    <h4>Kommentare</h4>

		    <form id="form" onsubmit="return false;"> 

		        <div class="form-floating mb-3">
		            <input type="text" class="form-control" id="input1" placeholder="Kommentar 1" onchange="fixeInput()" />
		            <label for="input1">Kommentar 1</label>
		        </div>

		    </form> 
		    <script>
		        let nr = 1;

		        function fixeInput() {
		            /*
		            let curInputId = "input" + nr;
		            let curInputElement = document.getElementById(curInputId);
		            console.log(curInputElement.value);
		            curInputElement.disabled = "true";

		            let newDiv = document.createElement('div');
		            newDiv.classList.add("form-floating", "mb-3");
		            nr++;
		            let newInputId = "input"+nr;
		            let newInput = document.createElement('input');
		            newInput.classList.add("form-control");
		            newInput.placeholder = "Kommentar " + nr;
		            newInput.id = newInputId;
		            newInput.addEventListener("change", fixeInput);
		            let newLabel = document.createElement('label');
		            newLabel.for = newInputId;
		            newLabel.textContent = "Kommentar " + nr;
		            newDiv.appendChild(newInput);
		            newDiv.appendChild(newLabel);
		            let form = document.getElementById('form');
		            form.appendChild(newDiv);

		            newInput.focus();
		            */

		            nr++;
		            let curInputId = "input" + nr;
		            let kommentar = "Kommentar " + nr;
		            let form = document.getElementById('form');
		            form.innerHTML += `
		            <div class="form-floating mb-3">
		                <input class="form-control" id=${curInputId} placeholder=${kommentar} onchange="fixeInput()" />
		                <label for=${curInputId}>${kommentar}</label>
		            </div> `
		            document.querySelector(`#${curInputId}`).focus()

		        }
		    </script>

		</body>
		</html>
		```



## Semesteraufgabe

Am Ende des Kurses geben Sie eine Webanwendung ab. Diese wird bewertet und bildet die Modulnote für "WebTech" (es gibt also keine Klausur o.ä.). Überlegen Sie sich früh, was Sie implementieren wollen. Ihrer Kreativität sind keine Grenzen gesetzt. Es können 2 Studentinnen gemeinsam ein Projekt durchführen und abgeben. Sie erhalten dann (höchstwahrscheinlich) die gleiche Note. Es muss an den Commits erkennbar sein, welchen Anteil am Ergebnis jede der beiden Studentinnen hatte. Beachten Sie auch dringend die Regeln zum Umgang mit KI in den folgenden Mindestanforderungen!

!!! question "Mindestanforderungen"
	Folgende Anforderungen werden an Ihr Projekt gestellt:

	* das Frontend soll mit Angular entwickelt werden,
	* das Backend mit Node.js,
	* es soll eine Datenbank (MongoDB, kann aber auch MySQL oder PostgreSQL oder MariaDB - aber **nicht** Firebase) verwendet werden,
	* es soll CRUD implementiert sein, d.h. Sie benötigen 
	    * eine Komponente zur Erstellung und Speicherung eines Datenbankeintrages (<b>C</b>reate),
	    * eine Komponente zur Änderung eines Datenbankeintrages (<b>U</b>pdate),
	    * eine Komponente zur Anzeige *aller* Datenbankeinträge (<b>R</b>ead),
	    * eine Komponente zum Löschen eines Datenbankeintrages (<b>D</b>elete).
    * wenn Sie die Anwendung alleine umsetzen, dann genügen 3 der 4 CRUD-Funktionalitäten
    * wenn Sie die Anwendung zu zweit entwickeln, dann
    	* sollen alle 4 CRUD-Funktionalitäten umgesetzt werden und
    	* Login (Username + Passwort) und
    	* ich schaue mir die Commit-Hiostorie im Git genauer an, um sicherzugehen, dass beide Studentinnen gleich viel an der Anwendung mitentwickelt haben

	Datenbankeinträge können Bücher, CDs, ToDos, Einkaufslisten, Vorlesungen, Kühlschrankinhalte usw. sein - wie gesagt, Ihrer Kreativität sind keine Grenzen gesetzt. Backend, Frontend und Datenbank müssen sich schon von dem unterscheiden, was wir in der Vorlesung und in der Übung gemacht haben (und somit vom Skript). 

	Die Anwendung soll in einem Git-Dienst (GitHub, GitLab, ...) verfügbar sein. 

	Verwenden Sie ein CSS-Framework, wie z.B. Materialize, Bootstrap o.ä.! Ihre Anwendung soll "modern" aussehen und responsive sein. 

	Erstellen Sie eine **informative (ausführliche) README**-Datei (`README.md`). Diese Datei sollte beinhalten:

	 - Eine Beschreibung Ihrer Anwendung. Am besten mit Screenshots, so dass sie Ihren Kommilitoninnen aus den nächsten Jahren hilft, ein Verständnis dafür zu entwickeln, was mögliche Semesteraufgaben sein können.
	 - Eine Anleitung zur Installation Ihrer Anwendung. 

	Super wäre es, wenn Sie die Datenbank, die Sie verwenden, per Skript vorausfüllen, d.h. es wäre schön, wenn zum Testen der Anwendung nur das Frontend und das Backend gestartet werden müssten und alles andere automatisch passieren würde. Super wäre es auch, wenn Sie Ihre Anwendung deployen würden. 

	Wenn alle Anforderungen kritiklos erfüllt sind, ist die Note schonmal eine `1.7` (bei leichter Kritik `2.0`). Es zeigte sich jedoch in den letzten Jahren, dass es wirklich herausragende Lösungen gab, die dann auch mit einer `1.3` und einige (wenige) sogar mit einer `1.0` bewertet werden konnten. Die Erwartungen für solche Lösungen lassen sich nicht formulieren, denn sie gehen ja "über die Erwartungen hinaus" ;-). 
	
	Nach Abgabe vereinbaren wir ein Online-Meeting, in dem Sie mir Ihre Anwendung nochmal zeigen können und ich Ihnen Fragen zu Ihrem Code stellen werde. Ist keine Prüfung, sondern eher ein fachliches Gespräch.  

	**Beachten Sie folgende Regeln zum Umgang mit KI :** <br/>

	1. Die Nutzung von KI bei der Erstellung der Semesterabgabe ist grundsätzlich erlaubt.
	2. In der `README.md` muss es ein Verzeichnis der verwendeten KI-Werkzeuge geben (stichpunktartig, wofür welche KI verwendet wurde).
	3. Ihren Code müssen Sie erklären und einfache Änderungen und Ergänzungen durchführen können. Wenn Sie mehrere/alle Fragen im Gespräch nicht beantworten können, gilt die Arbeit als Täuschungsversuch.

## Abgabe- und Gesprächstermine

Die Lösung für die Semesteraufgabe pushen Sie in Ihr Respository. In einem Gespräch führen Sie die Lösung vor und wir unterhalten uns über Ihre Lösung. Dafür stehen verschiedene Termine zur Verfügung. 

- 1. Prüfungszeitraum: 23.7.2025 Abgabe und 24.7.2025 Gespräch
- 2. Püfungszeitraum: 23.9.2025 Abgabe und 24.9.2025 (evtl. auch 25.9.2025) Gespräch

Bitte tragen Sie sich in [Moodle](https://moodle.htw-berlin.de/mod/wiki/view.php?id=1938265) in den von Ihnen gewünschten Gesprächstermin ein! Wenn Sie im 1.PZ abgeben, tragen Sie sich im LSF zum ersten PZ zur Prüfung ein, ansonsten im 2.PZ. 



