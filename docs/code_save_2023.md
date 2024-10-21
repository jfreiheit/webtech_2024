# Code aus der Vorlesung


??? question "Code Vorlesung 14.11.2023"
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
	            <li><a href="https://www.ecma-international.org/publications-and-standards/standards/ecma-262/">ECMA-262</a>
	            </li>
	            <li><a href="https://dom.spec.whatwg.org/">Document Object Model (DOM)</a></li>
	            <li><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide">JavaScript Guide</a></li>
	            <li><a href="https://www.w3schools.com/js/default.asp">JavaScript Tutorial</a></li>
	            <li><a href="https://learnjavascript.online/">Learn JavaScript</a></li>
	            <li><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference">JavaScript Reference</a>
	            </li>
	            <li><a href="https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeType?retiredLocale=de">Objekttypen im DOM</a>
	            </li>
	        </ul>
	        <h4>Ergebnisliste</h4>
	        <ul id="ulresult">
	            <li id="liresult1"></li>
	        </ul>
	        <input onchange="inputToList()" type="text" id="input"  placeholder="Name" />
	        <button type="button">Klick Mich!</button>
	    </main>
	    <script>
	        function helloFIW(name = 'World') {
	            console.log('Hello ' + name)
	        }

	        function inputToList() {
	            let input = document.getElementById('input');
	            let inputValue = input.value;
	            console.log('value :', inputValue)
	            let output = document.querySelector('#liresult1');
	            if(output.innerHTML == "") {
	                output.innerHTML = inputValue;
	                output.style.color = 'red';
	            } else {
	                let newLi = document.createElement('li');
	                let liste = document.querySelector('#ulresult');
	                console.log('ul : ', liste);
	                let newText = document.createTextNode(inputValue);
	                newLi.appendChild(newText);
	                liste.appendChild(newLi);
	            }
	            input.value = "";
	        }
	    </script>
	</body>

	</html>
	```


??? question "Code Vorlesung 21.11.2023"
	```html
	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <meta name="viewport" content="width=device-width, initial-scale=1.0">
	    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet"
	        integrity="sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN" crossorigin="anonymous">
	    <title>Asynchron</title>
	</head>
	<body class="container">
	    <h1>Themen</h1>
	<div class="list-group">
	   <a class="list-group-item list-group-item-action" href="https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing">asynchron</a>
	    <a class="list-group-item list-group-item-action" href="https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch">fetch-API</a>
	    <a class="list-group-item list-group-item-action" href="https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Basics">Objekte</a>
	    <a class="list-group-item list-group-item-action" href="https://www.json.org/json-de.html">JSON</a>
	    <a class="list-group-item list-group-item-action" href="https://angular.io/">Angular</a>
	</div>
	<script>
	    function asyncBehaviour() {

	        let a = 1;
	        let b = 1;

	        setTimeout(  () => {
	            console.log('timeout a = ', a)
	        }, 100)

	        fetch('https://jsonplaceholder.typicode.com/posts')
	        .then( response => {
	            console.log(response)
	            return response.json() // Rueckgabe des body unserer Response
	        })
	        .then ( body => {
	            console.log('body', body)
	            return body[0]
	        })
	        .then( obj0 => console.log(obj0))

	        console.log("a = ", a)
	        console.log("b = ", b)

	        a = 10;
	    }

	    let person = {
	        name: "Musterfrau",
	        vorname: "Maria",
	        adresse: {
	            strasse: "Wilhelminenhofstr.",
	            nummer: 75,
	            plz: 12459,
	            stadt: "Berlin"
	        },
	        getName: () => `${person.vorname} ${person.name}` 
	    }

	    person.alter = 42

	    console.log('person', person)
	    console.log('name', person.name)
	    console.log('strasse', person.adresse?.strasse)
	    console.log('name + vorname', person.getName())

	    let personJSON = JSON.stringify(person)
	    console.log(personJSON)
	    let personObj = JSON.parse(personJSON)
	    console.log(personObj)

	    asyncBehaviour();
	</script>
	</body>
	</html>
	```


??? question "Code Vorlesung 28.11.2023"
	Angulat-Projekt `first` - siehe [hier](https://github.com/jfreiheit/WT23)


??? question "Code Vorlesung 05.12.2023"
	=== "shared/my.service.ts"
	```js
	import { Injectable } from '@angular/core';
	import { Member } from 'member';

	@Injectable({
	  providedIn: 'root'
	})
	export class MyService {

	  async getAllMembers(): Promise<Member[]> {
	    let response = await fetch('..assets/members.json')
	    let membersArray = response.json();
	    return membersArray;
	  }
	}
	```

	=== "shard/member.ts"
	```js
	export interface Member {
	  firstname: string;
	  lastname: string;
	  email: string;
	  ipaddress: string;
	}
	```

	=== "table.component.ts"
	```js
	import { Component, OnInit, inject } from '@angular/core';
	import { CommonModule } from '@angular/common';
	import { MyService } from '.shared/my.service';
	import { Member } from '.shared/member';
	import { FormControl, ReactiveFormsModule } from '@angular/forms';

	@Component({
	  selector: 'app-table',
	  standalone: true,
	  imports: [CommonModule, ReactiveFormsModule],
	  templateUrl: 'table.component.html',
	  styleUrl: 'table.component.css'
	})
	export class TableComponent implements OnInit{

	  members: Member[] = [];
	  filterMem: Member[] = [];
	  search = new FormControl('');
	  private myservice = inject(MyService);


	  async ngOnInit(): Promise<void> {
	    this.members = await this.myservice.getAllMembers();
	    this.filterMem = this.members;
	    console.log('members', this.filterMem)
	  }

	  filterMembers(): void{
	    let searchstring = this.search.value ? this.search.value : "";
	    console.log(searchstring)
	    this.filterMem = this.members.filter( (member) =>
	      member.firstname.toLowerCase().includes(searchstring) );
	    console.log(this.filterMem)
	  }
	}
	```

	=== "table.component.html"
	```html
	<h1>Alle Teilnehmerinnen</h1>
	<input type="text" placeholder="Filtern" [formControl]="search" (input)="filterMembers()"/>
	<table>
	  <thead>
	    <tr>
	      <th>Nr</th>
	      <th>Vorname</th>
	      <th>Nachname</th>
	      <th>E-Mail</th>
	      <th>IP-Adresse</th>
	    </tr>
	  </thead>
	  <tbody>
	    <tr *ngFor="let member of filterMem; let i = index;">
	      <td>{{ i }}</td>
	      <td>{{ member.firstname }}</td>
	      <td>{{ member.lastname }}</td>
	      <td>{{ member.email }}</td>
	      <td>{{ member.ipaddress }}</td>
	    </tr>
	  </tbody>
	</table>
	```

??? hint "Video aus Vorlesung 05.12.2023"
	<iframe src="https://mediathek.htw-berlin.de/media/embed?key=bb3c140407d5a0b09e4379af729c3c01&width=720&height=405&autoplay=false&controls=true&autolightsoff=false&loop=false&chapters=false&playlist=false&related=false&responsive=false&t=0&loadonclick=true&thumb=true" data-src="https://mediathek.htw-berlin.de/media/embed?key=bb3c140407d5a0b09e4379af729c3c01&width=720&height=405&autoplay=false&controls=true&autolightsoff=false&loop=false&chapters=false&playlist=false&related=false&responsive=false&t=0&loadonclick=true" class="" width="720" height="405" title="10_Services" frameborder="0" allowfullscreen="allowfullscreen" allowtransparency="true" scrolling="no" aria-label="media embed code" style=""></iframe>



??? question "Code Vorlesung 12.12.2023"
	=== "server.js"
		```js
		const express = require('express');
		const cors = require('cors');
		require('dotenv').config();
		const routes = require('routes');
		const init = require('initdb')

		const app = express();
		const PORT = 4000;

		app.use(express.json());
		app.use(cors());
		app.use('/init', init)
		app.use('/', routes);

		app.listen(PORT, (error) => {
		    if(error) {
		        console.log('error! ', error)
		    } else {
		        console.log(`server running on port ${PORT} ...`)
		    }
		})
		```

	=== "routes.js"
		```js
		const express = require('express');
		const client = require('db')
		const router = express.Router();

		// CRUD

		// get all members
		router.get('/members', async(req, res) => {
		    const query = `SELECT * FROM public.members `;

		    try {
		        const result = await client.query(query)
		        console.log(result)
		        res.send(result.rows);
		    } catch (err) {
		        console.log('error - select' , err.stack)
		    }
		});

		module.exports = router;
		```

	=== "db.js"
		```js
		const pg = require('pg')
		require('dotenv').config();

		const client = new pg.Client({
		    user: process.env.PGUSER,
		    host: process.env.PGHOST,
		    database: process.env.PGDATABASE,
		    password: process.env.PGPASSWORD,
		    port: process.env.PGPORT
		})

		client.connect( (err) => {
		    if(err) {
		        console.log('database NOT connected', err)
		    } else {
		        console.log('database connected ...')
		    }
		})

		module.exports = client;	/* hier fehlte ein s hinter export im Video */
		```

	=== "initdb.js"
		```js
		const express = require('express');
		const client = require('db');
		const initdb = express.Router();
		const format = require('pg-format');


		initdb.get('/', async(req, res) => {

		    // Anlegen der Tabelle members
		    let query = `
		            DROP TABLE IF EXISTS members;
		            CREATE TABLE members(id serial PRIMARY KEY, firstname VARCHAR(50), lastname VARCHAR(50), email VARCHAR(50));
		            `;

		    try {
		        await client.query(query)
		        console.log("Table created successfully ...")
		    } catch (err) {
		        console.log(err)
		    }

		    // Befüllen der Tabelle members mit 50 Einträgen
		    const values = [
		        ["Catherine", "Williams", "cwilliamsl@360.cn"],
		        ["Adam", "Anderson", "aanderson8@google.fr"],
		        ["Susan", "Andrews", "sandrewsn@google.co.jp"],
		        ["Catherine", "Andrews", "candrewsp@noaa.gov"],
		        ["Alan", "Bradley", "abradley1c@globo.com"],
		        ["Anne", "Brooks", "abrooks16@bravesites.com"],
		        ["Russell", "Brown", "rbrownq@nifty.com"],
		        ["Ryan", "Burton", "rburton18@foxnews.com"],
		        ["Roy", "Campbell", "rcampbell1@geocities.com"],
		        ["Russell", "Campbell", "rcampbell17@eventbrite.com"],
		        ["Bonnie", "Coleman", "bcoleman11@fc2.com"],
		        ["Ernest", "Coleman", "ecoleman15@businessweek.com"],
		        ["Richard", "Cruz", "rcruz7@unc.edu"],
		        ["Sean", "Cruz", "scruz10@answers.com"],
		        ["Rebecca", "Cunningham", "rcunninghamd@mac.com"],
		        ["Margaret", "Evans", "mevansh@pcworld.com"],
		        ["Jeffrey", "Ford", "jford14@cnet.com"],
		        ["Andrea", "Gardner", "agardnerv@woothemes.com"],
		        ["Deborah", "George", "dgeorge6@furl.net"],
		        ["Sean", "Gibson", "sgibsony@alexa.com"],
		        ["Virginia", "Graham", "vgrahamk@aol.com"],
		        ["Steven", "Hamilton", "shamiltonu@state.tx.us"],
		        ["Virginia", "Hawkins", "vhawkinsf@ehow.com"],
		        ["Edward", "Hicks", "ehicksc@pcworld.com"],
		        ["Mark", "Johnson", "mjohnsonj@hostgator.com"],
		        ["Ruth", "Jordan", "rjordan1a@smugmug.com"],
		        ["Antonio", "Kim", "akim4@odnoklassniki.ru"],
		        ["Jennifer", "Marshall", "jmarshallt@gnu.org"],
		        ["Eric", "Matthews", "ematthews5@independent.co.uk"],
		        ["Raymond", "Mcdonald", "rmcdonald2@ihg.com"],
		        ["Eric", "Miller", "emillere@creativecommons.org"],
		        ["Jonathan", "Morales", "jmoralesa@ovh.net"],
		        ["Marie", "Morgan", "mmorganb@cloudflare.com"],
		        ["Amanda", "Nelson", "anelson13@indiatimes.com"],
		        ["Lisa", "Olson", "lolsonr@telegraph.co.uk"],
		        ["Alice", "Ortiz", "aortizw@histats.com"],
		        ["Peter", "Phillips", "pphillipss@1688.com"],
		        ["Matthew", "Porter", "mporter9@europa.eu"],
		        ["Tammy", "Ray", "trayx@weather.com"],
		        ["Mark", "Richardson", "mrichardson1d@ihg.com"],
		        ["Joan", "Roberts", "jroberts12@alibaba.com"],
		        ["Kathleen", "Rose", "kroseg@pinterest.com"],
		        ["Steve", "Sanders", "ssanders1b@wikispaces.com"],
		        ["Shirley", "Scott", "sscottm@macromedia.com"],
		        ["Lillian", "Stephens", "lstephens19@hugedomains.com"],
		        ["Nicole", "Thompson", "nthompson3@admin.ch"],
		        ["Marie", "Thompson", "mthompsonz@yelp.com"],
		        ["Alan", "Vasquez", "avasquezo@miibeian.gov.cn"],
		        ["Mildred", "Watkins", "mwatkins0@miibeian.gov.cn"],
		        ["Eugene", "Williams", "ewilliamsi@deliciousdays.com"]
		    ];
		    const paramquery = format('INSERT INTO members(firstname, lastname, email) VALUES %L RETURNING *', values);


		    try {
		        const result = await client.query(paramquery)
		        console.log("50 members inserted ...")
		        res.status(200)
		        res.send(result.rows)
		    } catch (err) {
		        console.log(err)
		    }

		});


		module.exports = initdb;
		```

	=== ".env (Anpassen!)"
		```
		PGUSER=ihr_username
		PGHOST=psql.f4.htw-berlin.de
		PGPASSWORD=ihr_passwort
		PGDATABASE=ihre_datenbank
		PGPORT=5432
		```

	=== "package,json"
		```
		{
		  "name": "backend1",
		  "version": "1.0.0",
		  "description": "Backend mit PostgreSQL",
		  "main": "server.js",
		  "scripts": {
		    "start": "nodemon server.js",
		    "test": "echo \"Error: no test specified\" && exit 1"
		  },
		  "author": "",
		  "license": "ISC",
		  "dependencies": {
		    "cors": "^2.8.5",
		    "dotenv": "^16.3.1",
		    "express": "^4.18.2",
		    "nodemon": "^3.0.2",
		    "pg": "^8.11.3",
		    "pg-format": "^1.0.4"
		  }
		}

		```


??? hint "Video aus Vorlesung 12.12.2023"
	<iframe src="https://mediathek.htw-berlin.de/media/embed?key=1622721f44d0a01a63ceaff2514405e7&width=720&height=405&autoplay=false&controls=true&autolightsoff=false&loop=false&chapters=false&playlist=false&related=false&responsive=false&t=0&loadonclick=true&thumb=true" data-src="https://mediathek.htw-berlin.de/media/embed?key=1622721f44d0a01a63ceaff2514405e7&width=720&height=405&autoplay=false&controls=true&autolightsoff=false&loop=false&chapters=false&playlist=false&related=false&responsive=false&t=0&loadonclick=true" class="" width="720" height="405" title="11_backend_postgresql" frameborder="0" allowfullscreen="allowfullscreen" allowtransparency="true" scrolling="no" aria-label="media embed code" style=""></iframe>


??? hint "Video aus Vorlesung 19.12.2023"
	<iframe src="https://mediathek.htw-berlin.de/media/embed?key=4d3b91dff946a0efb441c10c1e1ede53&width=720&height=405&autoplay=false&controls=true&autolightsoff=false&loop=false&chapters=false&playlist=false&related=false&responsive=false&t=0&loadonclick=true&thumb=true" data-src="https://mediathek.htw-berlin.de/media/embed?key=4d3b91dff946a0efb441c10c1e1ede53&width=720&height=405&autoplay=false&controls=true&autolightsoff=false&loop=false&chapters=false&playlist=false&related=false&responsive=false&t=0&loadonclick=true" class="" width="720" height="405" title="Webtech_Backend2" frameborder="0" allowfullscreen="allowfullscreen" allowtransparency="true" scrolling="no" aria-label="media embed code" style=""></iframe>



??? question "Code Vorlesung 2.1.2024"
	=== "register.component.html"
		```html
		<div class="container">
		  <h1 class="mt-5">Registrierung</h1>

		    <div class="mb-3 row">
		      <label for="idUsername" class="col-sm-2 col-form-label">Username</label>
		      <div class="col-sm-10">
		        <input type="text" class="form-control" id="idUsername" placeholder="username" [formControl]="usernameFC" [class]="usernameFC.valid ? 'is-valid' : 'is-invalid'">
		      </div>

		    </div>

		    <div class="mb-3 row">
		      <label for="staticEmail" class="col-sm-2 col-form-label">Email</label>
		      <div class="col-sm-10">
		        <input type="email" class="form-control" id="staticEmail" placeholder="email@example.com" [formControl]="emailFC" [class]="emailFC.valid ? 'is-valid' : 'is-invalid'">
		      </div>
		    </div>

		    <div class="mb-3 row">
		      <label for="inputPassword" class="col-sm-2 col-form-label">Password</label>
		      <div class="col-sm-10">
		        <input type="password" class="form-control" id="inputPassword" [formControl]="passwordFC" [class]="passwordFC.valid ? 'is-valid' : 'is-invalid'">
		      </div>
		    </div>

		    <div class="mb-3 row">
		    <label for="roleID" class="col-sm-2 col-form-label">Role</label>
		    <div class="col-sm-10">
		    <select class="form-select" id="roleID" [formControl]="roleFC" [class]="roleFC.valid ? 'is-valid' : 'is-invalid'">
		      <option value="admin">Admin</option>
		      <option value="user">User</option>
		      <option value="reader">Reader</option>
		    </select>
		    </div>
		    </div>

		    <div class="mb-3 row">
		      <button type="button" class="offset-2 col-10 btn btn-success" (click)="register()">Register</button>
		    </div>
		</div>
		```

	=== "register.component.ts"
		```js
		import { Component } from '@angular/core';
		import { FormControl, ReactiveFormsModule, Validators } from '@angular/forms';

		@Component({
		  selector: 'app-register',
		  standalone: true,
		  imports: [ReactiveFormsModule],
		  templateUrl: 'register.component.html',
		  styleUrl: 'register.component.css'
		})
		export class RegisterComponent {
		  usernameFC = new FormControl('', Validators.required);
		  passwordFC = new FormControl('', Validators.required);
		  emailFC = new FormControl('', [Validators.required, Validators.email]);
		  roleFC = new FormControl('', Validators.required);

		  register() {
		    console.log('button geklickt')

		    if(this.usernameFC.valid) {
		      console.log('valid')
		    }
		    else {
		      console.log('invalid');
		      if(this.usernameFC.errors?.['required']) console.log('username required')
		    }
		    let usernameValue = this.usernameFC.value;
		    let passwordValue = this.passwordFC.value;
		    let emailValue = this.emailFC.value;
		    let roleValue = this.roleFC.value;

		    let user = {
		      username: usernameValue,
		      password: passwordValue,
		      email: emailValue,
		      role: roleValue
		    }

		    console.log('user : ', user)
		  }
		}
		```


??? hint "Video aus Vorlesung 2.1.2024"
	<iframe src="https://mediathek.htw-berlin.de/media/embed?key=361e14872bb0d3da49435d2bcb6d77d1&width=720&height=405&autoplay=false&controls=true&autolightsoff=false&loop=false&chapters=false&playlist=false&related=false&responsive=false&t=0&loadonclick=true&thumb=true" data-src="https://mediathek.htw-berlin.de/media/embed?key=361e14872bb0d3da49435d2bcb6d77d1&width=720&height=405&autoplay=false&controls=true&autolightsoff=false&loop=false&chapters=false&playlist=false&related=false&responsive=false&t=0&loadonclick=true" class="" width="720" height="405" title="Webtech_Formulare" frameborder="0" allowfullscreen="allowfullscreen" allowtransparency="true" scrolling="no" aria-label="media embed code" style=""></iframe>


??? question "Code Vorlesung 9.1. und 16.1.2024"
	siehe [GitHub-Repo Frontend](https://github.com/jfreiheit/frontend_bs_23) und [Backend](https://github.com/jfreiheit/backend_23)

??? hint "Video aus Vorlesung 16.1.2024"
	<iframe src="https://mediathek.htw-berlin.de/media/embed?key=0253a00e5afe7b184ab31ca3a2881664&width=720&height=405&autoplay=false&controls=true&autolightsoff=false&loop=false&chapters=false&playlist=false&related=false&responsive=false&t=0&loadonclick=true&thumb=true" data-src="https://mediathek.htw-berlin.de/media/embed?key=0253a00e5afe7b184ab31ca3a2881664&width=720&height=405&autoplay=false&controls=true&autolightsoff=false&loop=false&chapters=false&playlist=false&related=false&responsive=false&t=0&loadonclick=true" class="" width="720" height="405" title="WebTech_Vorl0116" frameborder="0" allowfullscreen="allowfullscreen" allowtransparency="true" scrolling="no" aria-label="media embed code" style=""></iframe>

