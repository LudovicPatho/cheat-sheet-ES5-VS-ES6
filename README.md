# Les différences entre l'ES5 et l'ES6

À la pointe de la technologie, tu as appris à coder en ES6. Oui mais voilà, tu te rends rapidement compte que la majorité des tutos sur le net sont eux, écrit en ES5. Et tu voudrais comprendre les différences. Ou au contraire tu as appris à coder en ES5 et tu ne comprends rien à la nouvelle syntaxe proposé par l'ES6 ? Alors ce petit tuto est fait pour toi. :) 

## let, var & const

### let VS var 

Quelle est la différence entre un let et var ? La réponse est simple. Il s'agit du scope de la variable. Si tu utilises un ```let```, la variable sera locale, c'est à dire qu'elle sera uniquement accessible dans le bloque où tu l'as déclarez. Par bloque j'entends, une fonction, une condition, une boucle ou un script dans le cas où tu la déclares en début de script. Pour le  ```var```, c'est une autre histoire. Si tu déclares le ``` var ``` au sein d'une fonction, la variable sera globale ... Auparavant, cela  pouvait créer quelques bizzareries et on se retrouvait devoir nommer ses variables comme ceci  : var i, var i2, var i3 etc ... 

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
Quand vous déclarez votre variable dans la condition comme ceci :

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
C'est pour ça qu'on reçoit un "undefined".

Copie-colle ce code dans votre console et observe la différence de comportement entre ces deux boucles :

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
