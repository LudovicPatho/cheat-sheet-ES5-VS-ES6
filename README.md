# Les différences entre l'ES5 et l'ES6

À la pointe de la technologie, tu as appris à coder en ES6. Oui mais voilà, tu te rends rapidement compte que la majorité des tutos sur le net sont eux, écrit en ES5. Et tu voudrais comprendre les différences. Ou au contraire tu as appris à coder en ES5 et tu ne comprends rien à la nouvelle syntaxe proposé par l'ES6 ? Alors ce petit tuto est fait pour toi. :) 

## let, var & const

Quelle est la différence entre un let et var ? La réponse est simple. Il s'agit du scope de la variable. Si vous utilisez un ```let```, la variable sera locale, c'est à dire qu'elle sera uniquement accessible dans le bloque où vous l'avez déclarez. Par bloque j'entends, une fonction, une condition, une boucle ou un script dans le cas où vous la déclarez en début de script. Pour le  ```var```, c'est une autre histoire. Si vous déclarez votre ``` var ``` au sein d'une fonction, la variable sera globale ... Cela  pouvait amener à quelques bizzareries et on se retrouvait devoir nommer ses variables comme ceci  : var i, var i2, var i3 etc ... 

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
Le moteur de javascript recréé automatiquement une variable ``` var hello ``` en début de script. Ce qui reviendrait à faire  :
```
var hello = "Bonjour";
var hello;
```
C'est pour ça qu'on reçoit un "undefined".

Copiez-collez dans votre console et observez également la différence de comportement entre ces deux boucles :

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
