# ES2015 et + 
## L'ECMAScript c'est quoi ?
Wikipédia : 

> ECMAScript est un ensemble de normes concernant les langages de programmation de type script et 
> standardisé par Ecma International dans le cadre de la spécification ECMA-262. Il s'agit donc d'un standard,
> dont les spécifications sont mises en œuvre dans différents  langages de script, comme JavaScript ou ActionScript,
> ainsi qu'en C++ (norme 2011). C'est un langage de programmation orienté  prototype.

Ce qu'il faut surtout retenir à propos de l'ecmaspript:

* L'ES5 date de 2009
* L'ES6 date de 2015
* Aujourd'hui, on ne dit plus ES6 mais ES2015, ES2016, ES2017... Oui parce que maintenant ceux qui gérent les normes ECMAScript ont décidé de sortir une mise à jour par an. Et ce n'est pas plus mal comme ça.

Les différences entre l'ES2016 et 2015 sont minimes, même chose avec l'ES2017. (L'ES2018 n'est pas encore sorti à l'heure où j'écris ces lignes). Par contre les différences entre l'ES5 (ou 2009) et l'ES2015 sont majeures. 

![Es2015](http://egorsmirnov.me/assets/berlin-angular-meetup-26/images/es2015.jpg)

## let, var & const

### let VS var 

Quelle est la différence entre un let et var ? La réponse est simple: il s'agit du scope de la variable. Si tu utilises un ```let```, la variable sera locale, c'est à dire qu'elle sera uniquement accessible dans le bloque où tu l'as déclarée. Par bloque comprends, une fonction, une condition, une boucle ou un script dans le cas où tu la déclares en début de script. Pour le  ```var```, c'est une autre histoire. Si tu déclares le ``` var ``` au sein d'une boucle ou d'une condition, la variable sera globale ... Auparavant, cela  pouvait créer quelques bizzareries et l'on devait nommer ses variables comme ceci  : var i, var i2, var i3 etc ... 

```javascript


// En ES5

var hello ="Bonjour";
function getHello(args){
	if (args) {
		var hello = "Salut";
		return hello;
	}
	return hello;
}
getHello(); // retourne "undefined"


// En ES6 

let hello ="Bonjour";
function getHello(args){
	if (args) {
		let hello = "Salut";
		return hello;
	}
	return hello;
}
getHello(); // retourne "Bonjour"

```
Pourquoi en ES5 on reçoit un "undefined" ? 
Quand tu déclares la variable dans une condition comme ceci :

```javascript
	if (args) {
		var hello = "Salut";
		return hello;
	}
```
Le moteur de javascript recrée automatiquement une variable ``` var hello ``` en début de script (peu importe que la condition soit remplie ou pas). Ce qui reviendrait à faire  :

```javascript
var hello = "Bonjour";
var hello;

function getHello(args){
	if (args) {
		var hello = "Salut";
		return hello;
	}
	return hello;
}
getHello();

```
C'est pour ça qu'on reçoit un "undefined". L'utilisation du mot ```let``` règle ce problème.

Mets ce code dans la console de ton navigateur et observe la différence de comportement entre ces deux boucles :

```javascript 

for (var i = 0; i <= 10; i++) {
	for ( var i = 0; i <= 10; i++) {
		console.log(i);
	} 
}

```

```javascript 

for (let i = 0; i <= 10; i++) {
	for ( let i = 0; i <= 10; i++) {
		console.log(i);
	} 
}

```
### const

Les constantes sont des variables ... invariables. Comme son nom l'indique les valeurs des constantes ne changent jamais. Elles ont pour but de réduire l'utilisation de la memoire de ton ordinateur, mais aussi d'éviter des erreurs dans ton script. Par convention, on peut les écrire en majuscules. Ce n'est ps une obligation, mais ça permet de différencier en coup d'oeil les constantes et les variables.

```javascript
const URL = "http://monsite/assets/img/monfichier.jpg";

if (url) {
	URL = "Je change l'adresse url mais ca ne fonctionnera pas"
} 
//retourne : Uncaught TypeError: Assignment to constant variable.
    at <anonymous>:4:6
```

## Les objets.
Pour les objets, l'unique différence entre l'ES5 et l'ES2015 est sémantique. 

**Les méthodes**

Ici on ne fait que simplifier la syntaxe. 

```javascript
//En ES5

var hero = {
	name : name,
	score : score,
	attaque : function() {
		// Ici votre fonction attaque
	} 
}

//En ES2015 

let hero = { 
	name : name,
	score : score,
	attaque() {
		// Ici votre fonction attaque
	}
}
```

Comme je le disais, il n'y a que la sémantique qui soit différente.

**Les clés et valeurs**

D'ailleurs, puisqu'on y est... On simplifie également l'écriture des clés et leur valeur. 

```javascript 
//En ES5 

var hero = {
	name : name,
	score : score,
	xp : xp
}

// En ES2015 
let hero = {
	name,
	score,
	xp
}
```
On en a fini avec les objets.

## Les fonctions fléchées.
Il existe de nouvelles manières d'écire les fonctions. La nouvelle syntaxe se rapproche plus de la syntaxe du C#, java 8 ou encore le coffeescript.

```javascript
// En ES5

var getText = function () {
	console.log(argument);
}

// En ES6

let getText = (argument) => {
	console.log(argument);
} 

// Avec un seul argument, on peut se passer des parenthèses.

let getText = argument => {
	console.log(argument);
}

// S'il n'y a qu'une seule instruction on peut également se passer des accolades et mettre la fonction sur une ligne.

let getText = argument => console.log(argument);

```

La syntaxe pour écrire une fonction peut être déconcertante à première vue, mais on s'y fait vite. Surtout quand on prend conscience du gain de temps qu'elle permet. S'il n'y a qu'un seul argument, on peut même se passer des parenthèses. Et s'il n'y a qu'une seule instruction, on peut se passer des accolades moustaches. Si on ecrit la function en une seule ligne l'instruction return est automatique, pas besoin de l'écrire. 

**/!\ Avec les fonctions fléchées, il n'y a pas de ```this```.**

Quand tu écris une fonction à l'ancienne (```function (){ }```), que tu le veuilles ou non, la fonction retourne automatiquement un ```this``` et cela peut poser des soucis de scope. On se retouve à faire ```let self = this;```  ou à utiliser un ```bind(this)``` pour régler le problème. Avec les fonctions fléchées ce n'est plus le cas. Quand tu utilises un this dans une fonction fléchée, le this fait référence au this du bloque parent. 

## Template string (ou interpollation)
Eh oui, le javascript s'inspire maintenant des langages de templating. Plus besoin de concaténer avec des + les chaînes de caratères.

```javascript
// Oldschool
 var hello = function(name){
 	return "Your welcome " + name;
 }
 hello("Jean");

// Newschool
let hello = (name) => {
	return `Your welcome ${name}`;
}
hello("Jean");
```
(Comme vu précédemment, on aurait pu écrire cette dernière fonction en une seule ligne )
```javascript 
let hello = name => `Your Welcom ${name}`;
``` 

## Les paramètres 
### Les paramètres par défaut
Il est désormais possible de définir directement les paramètres par défaut. Avant on était obligé de faire ceci : 
```javascript
// Sans paramètre 
var hello = function(name) {
	return "Your welcom " + name;
}
hello(); // return "Your welcom undefined"


//On était donc obligé de faire
var hello = function(name) {
	if (name === "undefined") {
		name = "Inconnu";
	}

	return "Your welcom " + name;
}

hello() // return "Your welcom inconnu"
```

Maintenant, on peut l'écrire comme ceci : 

````javascript 
let hello = (name="inconnu") => {
	return "Your welcom " + name;
}
````

### Spread operator 
citation MDN 
> Cette syntaxe permet de représenter un nombre indéfini d'arguments sous forme d'un tableau

Pour les fonctions, on peut définir donc un nombre illimité d'arguments.

```javascript
let createPersonne = () => (...personne) {
  // personne devient un tableau avec toutes les valeurs.
	console.log(personne[0]); // Return "Jean"
	console.log(personne[1]); // Return 25
	console.log(personne[2]); // Return "Célibataire" 
	// ... 
}

createPersonne("Jean", 25, "Célibataire", "Coiffeur");
```

Pour les tableaux, on peut faire comme ceci : 
````javascript 
let ingredients = ["Tomate", "Poivron", "Farine"];
let recette = [...ingredients, "Poisson", "Sel"]; // Le tableau contiendra "Tomate", "Poivron", "Farine", "Poisson", "Sel".
````
On récupère donc les valeur du tableau ``ingredients`` et on peut en rajouter. 

Et depuis l'**es2018** on peut le faire aussi avec des objets : 
````javascript
let hero =  {
	name : "Moriarty",
	vie : 97,
	xp : 11,
	attaque(id) {
		//...
	}
}

let hero2 = { ...hero }
````




## Les class
Javascrpit permet désormais la création de ```class```. Toutefois, la POO en JS reste limitée et s'apparente plutôt à du prototypage amélioré. Il y a des notions de POO inéxistantes pour le moment en javascript comme la notion de ``public`` ou ``private``. Il n'est pas possible également de définir directement des propriétés dans une class, on est obligé de passer un ```constructor```pour les définir (Contrairement à d'autres langages orienté objet). 

````javascript
class Hello {
	constructor(name ="Inconnu") {
		this.name = name,
	}
	
	getHello () {
		return `Your welcom ${this.name}`
	}
}


let say = new Hello("Jean");
console.log(say.getHello()); //return  "Your welcom Jean"
````
### L'héritage de class 

On peut également faire de l'héritage de class. La fonction ``Super()`` récupère les propriétés de la class parente.

````javascript
class SayHello extends Hello {
	constructor() {
		super();
	}
	
	getHello2 () {
		return `Bienvenue ${this.name}`
	}
}

let say = new sayHello("Jean");
console.log(say.getHello()); //return  "Your welcom Jean"
console.log(say.getHello2()); //return  "Bienvenue Jean"
````

## Les promesses, async et await
Les promesses seront vues au prochain chapitre.  


Ceci n'est pas une liste exhaustive des nombreuses nouveautés de l'es2015/es2018. Ceci n'est qu'une petite base. N'hésite à fouiner sur MDN et à suivre des devs sur twitter ou reddit àafin de tenir informé. 





