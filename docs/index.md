# Web-Technologien

Herzlich willkommen zur WebTech-Veranstaltung im Wintersemester 2024/25! 

### Grober Inhalt

In dieser Veranstaltung lernen Sie, was das World Wide Web ist und wie man eigene Webseiten und -anwendungen realisiert. Sie lernen die Protokolle und Sprachen ``http``, ``HTML``, ``CSS``, ``JavaScript`` und `TypeScript` kennen und machen sich mit ``Angular``, ``Node.js`` und ``REST`` vertraut. Zentrales Thema ist der sogenannte [MEAN](https://www.ibm.com/cloud/learn/mean-stack-explained)-Stack, d.h. Sie lernen die Entwicklung mithilfe von <b>M</b>ongoDB, <b>E</b>xpress.js, <b>A</b>ngular und <b>N</b>ode.js kennen. Neben `MongoDB` lernen wir aber auch kennen, wie Sie `PostgreSQL` als Datenbank in Ihre Anwendung einbinden. 

Nachfolgend der vorläufige Wochenplan (wird eventuell angepasst). 

| | Woche | Themen (Vorlesung) | Übung | Aufgabe (Stand) | Abgabe Übung bis | 
|-|-------|--------------------|-------|-----------------|------------------|
| 1. | 07.-11.10.2024 | [Einführung](einfuehrung.md#webtechnologien-einfuhrung) und [Organisatorisches](#organisatorisches) | [Übung 0](uebungen.md#ubung-0) | - | - | 
| 2. | 14.-18.10.2024 | [HTML](html.md) | [Übung 1](uebungen.md#ubung-1) | Idee | 21.10.2024 | 
| 3. | 21.-25.10.2024 | [CSS (Eigenschaften und Selektoren](css.md#css) | [Übung 2](uebungen.md#ubung-2) | - | 28.10.2024 | 
| 4. | 28.-01.11.2024 | [CSS (Grid)](css.md#grid) | [Übung 3](uebungen.md#ubung-3) | Konzept | 04.11.2024 | 
| 5. | 04.-08.11.2024 | [RWD (responsive Webdesign)](rwd.md#responsive-web-design) | [Übung 4](uebungen.md#ubung-4) | - | 11.11.2024 | 
| 6. | 11.-15.11.2024 | [JavaScript (DOM)](javascript.md#javascript) | [Übung 5](uebungen.md#ubung-5) | Datenmodell | 18.11.2024 | 
| 7. | 18.-22.11.2024 | [Angular (Einführung und Komponenten)](angular.md#angular) | [Übung 6](uebungen.md#ubung-6) | Schnittstelle | 25.11.2024 | 
| 8. | 25.-29.11.2024 | [Angular (Bindings und Direktiven) + JSON](angular2.md#json-und-direktiven) | [Übung 7](uebungen.md#ubung-7) | Frontend (c+r)| 02.12.2024 | 
| 9. | 02.-06.12.2024 | [Angular (Routing und Services)](routing.md#routing-und-services) | [Übung 8](uebungen.md#ubung-8) | Frontend (u+d)| 09.12.2024 | 
| 10. | 09.-13.12.2024 | [Node.js + Express (REST-Server + MongoDB)](backend.md#rest-api-mongodb) |  [Übung 9](uebungen.md#ubung-9)| Frontend fertig | 16.12.2024 | 
| | | | | | | |
| 11. | 16.-20.12.2024 | [Angular (Anbindung ans Backend)](fe-be-anbindung.md#frontend-backend-anbindung) | [Übung 10](uebungen.md#ubung-10) | Backend ( c ) | 06.01.2025 | 
| 12. | 06.-10.01.2025 | [Nutzerverwaltung und Material](guards.md#subject-observable-observer-und-guards) | - | Backend (r + u) | 13.01.2025 |
| 13. | 13.-17.01.2025 | Signals  | - | Backend (d + fertig)| 20.01.2025 |
| 14. | 20.-24.01.2025 | Wiederholung | - | fertig stellen | 27.01.2025 |
| 15. | 27.-31.01.2025 | - | Fragen | - | - |
| 16. | 03.-07.02.2025 | - | Fragen | Abgabe 1.PZ 5.2.2025, Gespräche 6.2.2025  |
|  |  |  |  |Abgabe 2.PZ 26.3.2025, Gespräche 27.3.2025 (evtl. auch 28.3.2025)| - |


Die Erfahrung zeigt, dass die Mehrheit der Abgeben im 2.PZ erfolgt. Sie sollten allerdings bedenken, dass es zwischen dem 1. und dem 2.PZ keine Konsultationen gibt. 

### Organisatorisches 

Zur erfolgreichen Durchführung der Veranstaltung müssen Sie die Übungen lösen und zu den jeweiligen Fristen per Git auf einen Server (GitHub oder GitLab) laden. Am Ende des Semesters ist eine Aufgabe abzugeben. Diese Aufgabe wird bewertet. Die Bewertung entspricht dann der Modulnote. 

[Hier](uebungen.md#ubungen) sind die Übungen beschrieben, die Sie in jeder Woche ausführen sollen. Damit Sie dies erfolgreich erledigen können, ist jeweils angegeben, welche Themen Sie dafür durcharbeiten müssen. Das Durcharbeiten der jeweiligen Themen entspricht jeweils einer Vorlesung. Diese wird also selbständig durchgeführt. 

Für die Kommunikation untereinander verwenden wir [**Slack**](https://slack.com/intl/de-de/). Dort können Sie alle inhaltlichen und organisatorischen Fragen stellen. Ich fände es gut, wenn ich dort möglichst wenig Fragen - zumindest die inhaltlichen - beantworten müsste, sondern eine Art internes Diskussionsforum entsteht. Es ist sehr gewünscht, dort Fragen zu stellen und noch mehr gewünscht, diese von Ihnen dort beantwortet zu sehen. Damit wäre allen geholfen und ich kann besser erkennen, wo noch Nachhol- bzw. Erläuterungsbedarf bei den meisten besteht.  

## Code aus der Vorlesung

	
## Semesteraufgabe

Am Ende des Kurses geben Sie eine Webanwendung ab. Diese wird bewertet und bildet die Modulnote für "WebTech" (es gibt also keine Klausur o.ä.). Überlegen Sie sich früh, was Sie implementieren wollen. Ihrer Kreativität sind keine Grenzen gesetzt. Es können 2 Studentinnen gemeinsam ein Projekt durchführen und abgeben. Sie erhalten dann (höchstwahrscheinlich) die gleiche Note. Es muss an den Commits erkennbar sein, welchen Anteil am Ergebnis jede der beiden Studentinnen hatte.

??? question "Mindestanforderungen"
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

	Datenbankeinträge können Bücher, CDs, ToDos, Einkaufslisten, Vorlesungen, Kühlschrankinhalte usw. sein - wie gesagt, Ihrer Kreativität sind keine Grenzen gesetzt. 

	Die Anwendung soll in einem Git-Dienst (GitHub, GitLab, ...) verfügbar sein. 

	Verwenden Sie ein CSS-Framework, wie z.B. Materialize, Bootstrap o.ä.! Ihre Anwendung soll "modern" aussehen und responsive sein. 

	Erstellen Sie eine **informative (ausführliche) README**-Datei (`README.md`). Diese Datei sollte beinhalten:

	 - Eine Beschreibung Ihrer Anwendung. Am besten mit Screenshots, so dass sie Ihren Kommilitoninnen aus den nächsten Jahren hilft, ein Verständnis dafür zu entwickeln, was mögliche Semesteraufgaben sein können.
	 - Eine Anleitung zur Installation Ihrer Anwendung. 

	Super wäre es, wenn Sie die Datenbank, die Sie verwenden, per Skript vorausfüllen, d.h. es wäre schön, wenn zum Testen der Anwendung nur das Frontend und das Backend gestartet werden müssten und alles andere automatisch passieren würde. Super wäre es auch, wenn Sie Ihre Anwendung deployen würden. 
	
	Nach Abgabe vereinbaren wir ein Online-Meeting, in dem Sie mir Ihre Anwendung nochmal zeigen können und ich Ihnen Fragen zu Ihrem Code stellen werde. Ist keine Prüfung, sondern eher ein fachliches Gespräch. 

## Abgabe- und Gesprächstermine

Die Lösung für die Semesteraufgabe pushen Sie in Ihr Respository. In einem Gespräch führen Sie die Lösung vor und wir unterhalten uns über Ihre Lösung. Dafür stehen verschiedene Termine zur Verfügung. 

- 1. Prüfungszeitraum: 5.2.2025 Abgabe und 6.2.2025 Gespräch
- 2. Püfungszeitraum: 26.3.2025 Abgabe und 27.3.2025 Gespräch

Bitte tragen Sie sich in [Moodle](https://moodle.htw-berlin.de/course/view.php?id=49991) in den von Ihnen gewünschten Gesprächstermin ein! Wenn Sie im 1.PZ abgeben, tragen Sie sich im LSF zum ersten PZ zur Prüfung ein, ansonsten im 2.PZ. 

### Einige Beispiele

#### Mieter- und Zahlungsinformationen verwalten

- ![projekte](files/224_projekte1.png)
- ![projekte](files/225_projekte1.png)
	

#### ToDo-Liste

- ![projekte](files/226_projekte2.png)
- ![projekte](files/227_projekte2.png)
- ![projekte](files/228_projekte2.png)	

- ![projekte](files/229_projekte2.png)
- ![projekte](files/230_projekte2.png)


#### Dog-O-Mat

- ![projekte](files/231_projekte3.png)


#### Reiseplaner

- ![projekte](files/232_projekte3.png)
- ![projekte](files/233_projekte3.png)

