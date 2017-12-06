# Les différences entre l'ES5 et l'ES6

À la pointe de la technologie, tu as appris à coder en ES6. Oui mais voilà, tu te rends rapidement compte que la majorité des tutos sur le net sont eux, écrit en ES5. Et tu voudrais comprendre les différences. Ou au contraire tu as appris à coder en ES5 et tu ne comprends rien à la nouvelle syntaxe proposé par l'ES6 ? Alors ce petit tuto est fait pour toi. :) 

## L'ECMAScript c'est quoi ?
On va pas s'embêter, on va citer gentillement wikipédia : 

> ECMAScript est un ensemble de normes concernant les langages de programmation de type script et 
> standardisées par Ecma International dans le cadre de la spécification ECMA-262. Il s'agit donc d'un standard,
> dont les spécifications sont mises en œuvre dans différents  langages de script, comme JavaScript ou ActionScript,
> ainsi qu'en C++ (norme 2011). C'est un langage de programmation orienté  prototype.

En gros, ce sont des normes qui régissent tous les languages se terminant par "script" comme le javascript ou l'ActionScript (RIP l'ActionScript <3 ). Ce qu'il faut surtout retenir à propos de l'ecmaspript.

* L'ES5 date de 2009
* L'ES6 date de 2015
* Aujourd'hui, on ne dit plus ES6 mais ES2015, ES2016, ES2017... Oui par ce que maintenant ceux qui gérent les normes ECMAScript ont décidé sortir une mise à jour par an. Et c'est pas plus mal comme ça.

Alors, je te vois venir toi, au fond de la classe. On est en 2018, et je parle de l'ES2015. J'aurais donc 3 ans retard ? Je te répondrais que non ! Tout d'abord beaucoup de codeurs codent encore avec l'ES2009.  Et puis je te dirais que les différennces entre l'ES2016 et 2015 sont minimes, même chose avec l'ES2017. (L'ES2018 n'est pas encore sorti à l'heure où j'écris ces lignes). Par contre les différences entre l'ES5 (ou 2009) et l'ES2015 sont majeures. 

Donc du coup, je dois renommer le titre...

# Les différences entre l'ES5 (ou 2009) et l'ES2015

Voilà qui est mieux. On peut donc maintenant passer au vif du sujet. 

## let, var & const

### let VS var 

Quelle est la différence entre un let et var ? La réponse est simple. Il s'agit du scope de la variable. Si tu utilises un ```let```, la variable sera locale, c'est à dire qu'elle sera uniquement accessible dans le bloque où tu l'as déclaré. Par bloque j'entends, une fonction, une condition, une boucle ou un script dans le cas où tu la déclares en début de script. Pour le  ```var```, c'est une autre histoire. Si tu déclares le ``` var ``` au sein d'une fonction, la variable sera globale ... Auparavant, cela  pouvait créer quelques bizzareries et on se retrouvait devoir nommer ses variables comme ceci  : var i, var i2, var i3 etc ... 

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
Le moteur de javascript recréé automatiquement une variable ``` var hello ``` en début de script (peu importe que la condition soit remplie ou pas). Ce qui reviendrait à faire  :

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
C'est pour ça qu'on reçoit un "undefined". L'utilisation du mot let règle ce problème.

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

Les constantes sont des variables ... invariables. Comme son nom l'indique les valeurs des variables constantes ne changent jamais. Elles ont pour but de réduire l'utilisation de la memoire de votre ordinateur, mais aussi d'éviter des erreurs dans votre script. 

```javascript
const url = "http://monsite/assets/img/monfichier.jpg";

if (url) {
	url = "Je change l'adresse url mais ca ne fonctionnera pas"
} 
//retourne : Uncaught TypeError: Assignment to constant variable.
    at <anonymous>:4:6
```

### Les objets.
Pour les objets, la seule différence entre l'ES5 et l'ES2015 est sémantique. 

**Les méthodes**
Ici on ne fait que simplifier la syntaxe. 

```
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

D'ailleus puisqu'on y est... On simplifie également l'écriture des clés et leurs valeurs. 

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
C'est tout en ce qui concerne les objets.

### Les fonctions fléchées.
Plusieurs nouvelles manières d'écire les fonctions. La nouvelle syntaxe se rapproche plus de la syntaxe du C#, java 8 ou encore le coffeescript.

```javascript
En ES5

var getText = function () {
	console.log(argument);
}

En ES6

let getText = (argument) => {
	console.log(argument);
} 

// Avec un seul argument, on peut se passer des parenthèse.

let getText = argument => {
	console.log(argument);
}

// S'il n'y a qu'une seule propriété on peut également se passer des accolades et mettre la fonction sur une ligne.

let getText = argument => console.log(argument);

```

La syntaxe pour écrire une fonction peut être déconcertante à première vue, mais on s'y fait vite. Surtout quand on voit le gain de temps. Plus besoin d'écrire le mot ```function```, ni dans les méthodes, ni dans les fonctions. Sans compter toutes les fois où j'écris ```functuin``` et que je dois corriger. S'il n'y a qu'un seul argument, on peut se passer des parenthèses également. Et s'il n'y a qu'une propriété, on peut se passer des accolades moustaches.

**/!\ Avec les fonctions fléchées, il n'y a pas de this.**
Quand vous écrivez une fonction à l'ancienne (```function (){ }```), que vous le vouliez ou non, la fonction retourne automatiquement un this et cela pouvait poser des soucis de scope. On se retouvait à faire ```let self = this;```  ou à utiliser un ```bind(this)``` pour régler le problème. Avec les fonctions fléchées ce n'est plus le cas. Quand vous utilisez un this dans une fonction fléchée, le this fait référence au this du bloque parent. 

*C'est quoi un this ?*
Difficile à expliquer.
Pour savoir quel est la valeur de votre this,vous pouvez utiliser la fonction ```debugger```, une fonction native de javascipt qui est semblable au die() du php.

### Template string 
Eh oui, le javascript s'inspire maintenant des languages de templating. Plus besoin de concaténer avec des + les chaîne de caratères.

```
// Oldschool
 var hello = function(name){
 	return "Your welcom " + name;
 }
 hello("Jean");

// Newschool
let hello = (name) => {
	return `Your welcom ${name}`;
}
hello("Jean");
```

(Comme vu précédement, on aurait pu écrire cette dernière fonction en une seule ligne ```let hello = name => `Your Welcom ${name}`;```).

### Les tableaux 


### Les class



