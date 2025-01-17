# Introduction

JS première version 1995, auteur Brendan Eich.

Rappelons que JS est un langage interprété dont le typage est faible. Mais attention, cela ne veut pas dire que JS ne définit pas un type à ses variables.

Un typage faible permet les convertions de type implicites :

```js
let foo = 1 + "2";
```

Et JS a un typage dynamique, le type est déterminé à l'exécution :

```js
// Le type de a sera défini à l'exécution de cette ligne
let a = 1;
```

Un langage interprété utilise le code source pour le compiler puis l'exécuter, il n'y a pas de création d'exécutable. Pour chaque exécution, JS repartira du code source.

Le moteur JS de compilation peut taguer du code qui se répète et créer, pour ces parties uniquement, un exécutable. 

JS est un langage de script, orienté objet.

JS suit la norme **ECMAScript**, standard que suivent certains langages de script comme Javascript. Cette norme évolue en permance. Les principaux navigateurs Web mettent à jour leur moteur d'exécution pour suivre les évolutions de ce langage.

Une version majeure d'ECMAScript est celle qui a été définie en 2015 : ES2015 que l'on appelle ES6 ... Le nom de la version étant déterminé par la dernière version du standard en cours donc ES6 pour 2015 ... Aujourd'hui la dernière version officielle est EMACScript 2020.

## Typage

Bien que JS soit un langage faiblement typé, JS type toutes ses variables.

Le type d'une variable en JS est déterminé lorsqu'on la définit et qu'on lui assigne une valeur particulière. Ce dernier peut changer si on ré-assigne un valeur d'un autre type.

```js
let n = 10;
console.log(typeof n); // number

// ré-assignation
n = "Hello";

console.log(typeof n); // string
```

Dans l'exemple ci-dessus le type de la variable n a changé, il est passé du type number au type string (ré-assignation).

Notons que lorsque vous définissez une variable sans lui affecter une valeur particulière, celle-ci est de type "undefined" :

```js
let username;
console.log(typeof username); // undefined
```

## Les différents types en JS

On distingue les types suivants en Javascript. Attention tous les types primitifs définissent des valeurs non modifiables (immuables).

### 1. Types primitifs

- boolean

```js

// On ne peut modifier un "true" ...
let flag = true;
```

- null

```js
// On ne peut modifier un "null" ...
let flag = null;
```

- undefined

- number

- bigInt (big integer)

Il faut ajouter l'opérateur **n** pour définir des BigInt

```js
const x = 2n ** 100n;
console.log(x);
// 1267650600228229401496703205376n
```

- string

```js
let message = "Hello World";
```

- symbole (type introduit à partir de la norme ES6, un peu technique pour l'instant ...)


------

### 2. Les types Objects

Ils sont mutables, on peut modifier la valeur d'un objet. Un objet est une valeur conservée en mémoire à l'aide d'une référence unique.

Dans la liste des objets vous avez :

- Les objets classiques les classes et les fonctions

```js
class Model {

  constructor(name) {
    this.name = name;
  }

  get() {
    return this.name;
  }
}

// Création d'un instance (objet)
const myModel = new Model();

function modelFunc(n) {
  let name = n;

  return name;
}
```

- Les objets natifs comme les dates

```js
const now = new Date();
```

- Les collections comme les tableaux, Map, Set, ...

Les déclarations suivantes sont identiques :

```js
let notes = [1, 2, 3];
let newNotes = new Array(1, 2, 4);
```

Un Map est une simple collection de clés/valeurs. 

```js
// création d'un Map
const store = new Map();

store.set("A1", 10.6);
store.set("A2", 8.9);

console.log(store);
// {"A1" => 10.6, "A2" => 8.9}

const ensemble = new Set([1, 2, 3, 4, 5, 5]);
console.log(ensemble);
// [1, 2, 3, 4, 5] il n'y a pas de doublon
```

- Les JSON Javascript Object Notation

## Portée (ou scope en Anglais) des variables en JS

Définition let :
**La variable définie avec let a une portée scopée au niveau du bloc dans lequel elle a été déclarée.**

*Remarque importante : lorsque vous définissez une variable à l'intérieur d'une fonction elle est scopée (portée) dans la fonction elle-même, elle n'a pas d'effet de bord avec le reste du script.*

```js

function foo() {
  let a = 10;
  console.log(a); // affiche 10
}

foo();

// ReferenceError
console.log(a);
```

Si vous définissez une variable **de même nom** à l'extérieur de la fonction alors, elle n'aura pas d'effet sur la variable à l'intérieur de la fonction foo ci-après :

```js
let a = 11;

function foo() {
  let a = 10;
  console.log(a); 
}

// affiche 10
foo();

// affiche 11
console.log(a);
```

### Remonter des scopes 

JS cherche la définition de ses variables dans le scope courant et sinon en remontant les scopes, si la variable n'est définie dans aucun des scopes alors une erreur **ReferenceError** est levée.

```js
// bloc courant pour b
let b = 11;

function baz() {
  // bloc courant pour c
  let c = 9;

  // JS ne trouve pas b dans le bloc courant => il remonte les scopes
  console.log(b, c);
}

// affiche 11 9
baz();

```

Un autre exemple :

```js
// bloc courant
let b = 11;

function baz() {
  console.log(b);

  function foo() {
    console.log("Valeur du symbole b : ", b);
  }

  foo();
}

// affiche 11
baz();
```

## Exercice scope calcul (sans coder)

Est ce que le code qui suit vous semble correcte, répondre sans exécuter le code ? Si ce dernier n'est pas valide modifie-le afin qu'il puisse s'exécuter correctement.

```js

let a = 1;

function calcul() {
  let a = 2 + a;

  console.log(a, "calcul");

  function sub_calcul() {
    let b = a + 1;

    console.log(b, "sub_calcul");
  }

  sub_calcul();
}

calcul();

```

## Exercice TDZ (temporal dead zone) (sans coder)

Est ce que le code suivant est valide ? Répondez sans exécuter le code.

```js
function tdz() {
  console.log(tdz_val);

  let tdz_val = "Temporal Dead Zone";
}

tdz();
```

## Exercice for let (sans coder)

Est ce que le code suivant est valide ? Répondez sans exécuter le code.

```js
let i = 100;

for (let i = 0; i < 10; i++) {
  console.log(i);
}

console.log(i);
```

Est ce que le code suivant est valide ? Répondez sans exécuter le code.
Si ce code est valide qu'affichera-t-il ?

```js
for (let j = 0; j < 10; j++) {}
console.log(j);
```

## Déclaration d'une constante

Définition :
**La variable définie avec const a une portée scopée au niveau du bloc dans lequel elle a été déclarée.**

Le mot réservé du langage JS **const** permet de définir une constante à assignation unique. Notez que vous êtes obligé de lui donner une valeur lors de sa définition. Une constante ne peut être re-définit.

```js
const API_KEY = "ABf#123@";
console.log(API_KEY);
```

Une constante peut contenir tout type de variable. Dans le cas d'un objet comme un tableau par exemple, les valeurs du tableau sont modifiables(...) En effet, une constante bloque la ré-assignation de la variable, mais ne rend pas l'objet non-modifiable.

```js

const STUDENTS = ["Alan", "Bernard", "Jean"];

STUDENTS.push("Sophie");

console.log(STUDENTS);
//["Alan", "Bernard", "Jean", "Sophie"]

STUDENTS.pop();

console.log(STUDENTS);
// ["Alan", "Bernard", "Jean"]

```

Par contre ce qui suit est impossible, l'erreur suivante sera levée :
**TypeError: Assignment to constant variable.**

```js
let newStudents = ["Alice"];
// re-assignation impossible
STUDENTS = newStudents;
```

## Exercice const & for

1. Pouvez-vous utiliser à votre avis le mot réservé const dans la boucle suivante ?

```js
for (const j = 0; j < 10; j++) {}
```

2. Utilisez la syntaxe de boucle for of et const sur l'itérable STUDENTS et affichez (console.log) ses valeurs :

```js
const STUDENTS = ["Alan", "Bernard", "Jean"];
```


### var définition

*Ce mot clé pour définir une variable ne doit plus être utilisé, utilisez let à la place.*

Il permet de définir une variable globale ou locale à une fonction sans distinction de bloc :

```js
function foo() {
  var x = 10; // portée fonction pas bloc comme let
  if (true) {
    var x = 2;  // c'est la même variable !
    console.log(x);  // 2
  }
  console.log(x);  // 2
}
foo(); // 2 2
```

Par comparaison avec le mot clé let :

```js
function bar() {
  let x = 10; // portée fonction pas bloc comme let
  if (true) {
    let x = 2;  // c'est la même variable !
    console.log(x);  // 2
  }
  console.log(x);  // 10
}
bar(); //  2 10
```

## Fonction

Une fonction en JS est un objet.

### Paramètres par défaut

Valeurs par défaut facultatif :

```js
function add(a, sup = 1) {
  return a + sup;
}

add(10); // affiche 11

add(10, 0); // affiche 10

```

### Exercice ttc

1. Créez une fonction qui permet de calculer un prix ttc connaissant un prix HT. Donnez une valeur par défaut pour la tva en paramètre de la fonction, valeur de la tva par défaut : 20%.

2. Vérifiez que le type des variables passées en paramètre ne posent pas de problème. Utilisez **parseFloat** pour la vérification des types. Affichez les résultats avec au plus 2 chiffres après la virgule. 

```js

// 1.
ttc(100, 0.2); // 120
ttc(100.50, 0.2); // 120.6

// 2.
// Gestion du type
ttc("hello", 0.2); // Erreur de type
ttc(100.50, "hello"); // Erreur de type
ttc("100", ".3"); // 130
```

## Syntaxe par décomposition

Si vous avez une fonction avec de nombreux paramètres ou des paramètres variables, utilisez le spread operator pour passer les valeurs à la fonction :

```js
function sum(x, y, z) {
  return x + y + z;
}

let numbers = [1, 2, 3];

sum(...numbers); // sum(1, 2, 3) unpacking
```

### Exercice sum spread ttc

Ecrivez une fonction **sumTTC** qui prend 3 nombres arbitraires de prix HT et retourne la somme de ces prix TTC. La tva est facultative (20%).
Vérifiez que le type des variables passées en paramètre ne posent pas de problème, utilisez **parseFloat**. Affichez les résultats avec au plus 2 chiffres après la virgule.

Les prix HT seront donnés dans un tableau :

```js
const pricesHT = [100, 200, 55];

console.log(sumTTC(...priceHT));
console.log(sumTTC(...priceHT, .3));

// vérifiez le type des variables
const badPriceHT = [100.50, "hello", 55.7];
console.log(sumTTC(...badPriceHT, .3));
```

### littéral pour définir des paramètres

Vous pouvez utiliser la syntaxe suivante pour définir les paramètres d'une fonction, dans ce cas vous n'avez pas à vous soucier de l'ordre des paramètres :

```js
function baz({ a, b }){ 
  console.log(a, b ) 
}

baz({ a: 1, b : 2}); // 1 2
baz({ b: 2, a : 1}); // 1 2

```

## Le point sur le this des objets

Le this d'un objet est déterminé par la manière dont vous allez appeler l'objet "contexte".

L'objet sur lequel vous **appelez** la fonction détermine le this :

**objet.my_function()**

```js
'use strict';

const o1 = {
    f1 : function(){

      return this;
    }
}

console.log(o1.f1()) ; // this de o1

const o2 = {
    f2 : o1.f1
}

console.log(o2.f2()) ; // this de o2

const o3 = o1.f1;

console.log(o3()) ; // undefined car on n'appelle la fonction f1 explicitement
```

De même faite attention dans les fonctions de callback, dans l'exemple qui suit setTimeout fera appel à la fonction sans reprendre le context de l'objet lui-même, this sera, en mode strict, undefined :

```js
'use strict';

setTimeout(o1.f1, 1000); // ici setTimeout appel la fonction f1.
```

Pour corriger ce problème il faut écrire :

```js
setTimeout(() => o1.f1() , 1000); // ici setTimeout appel la fonction f1.
```

## Fonction & fonction fléchée

En JS vous avez des fonctions déclarées et des expressions de fonction.

- fonction déclarée :

```js
function foo(){

}
```

- Expression de fonction

```js
setTimeout( function (){

})
```

### Exercice function & expression

Nommez les types de fonction ci-dessous :

```js
const myFunc = function(){

  function bar(){
    // ...
  }
}
```

Les fonctions déclarées sont définies dès le début du script ou de la fonction qui la contient.

Pour les expressions de fonction elles sont définies après leur évaluation.

### Exercice déclaration

Sans exécuter le code. 

1. Est-ce que à votre avis le code suivant est valide ?

```js
bar();

function bar(){
  console.log("bar");
}
```

2. Est-ce que à votre avis le code suivant est valide ?

```js
myFunc(); 

const myFunc = function(){
    console.log("Expression");
}
```

### Arguments d'une fonction

Vous n'êtes pas obligé de renseigner le nombre d'argument d'une fonction JS. La fonction possède en interne une propriété (objet) arguments qui récupère les paramètres de la fonction, attention arguments n'est pas un tableau :

```js
function sum(){
  let total = 0;
  for(let i =0; i < arguments.length; ++i ) total += arguments[i];

  return total;
}

console.log(sum(1,2,3,4, 5, 6));
```

L'objet arguments peut-être converti en tableau à l'aide de la méthode from sur l'objet Array :

```js
const args = Array.from(arguments);

```

On peut par exemple définir la fonction sum en utilisant la méthode from :

```js
function sum(){
  const args = Array.from(arguments);
  
  return args.reduce( (acc, curr) => acc + curr );
}

console.log( sum(1,2,3,5) ); // 11

```

### Les fonctions fléchées

Les fonctions fléchées (arrow function) permettent d'avoir une syntaxe plus courte pour définir facilement des fonctions de rappel comme map, filter, reducer ...

```js
const power2 = (x) => {
  return x ** 2 ;
};
const numbers = [1, 2, 5];
console.log(numbers.map( power2 ));
// [1, 4, 25]
```

Si vous ne retournez qu'un seul résultat vous pouvez écrire la syntaxe concise suivante :

```js
// syntaxe consise
const sum = (x, y) => x + y ;

// 
const sum2 = (x, y) => {
  return x + y;
};
```

Dans le cas ou vous souhaiteriez retourner un unique littéral, dans des accolades donc ..., utilisez la syntaxe suivante parenthèse :

```js
// syntaxe consise
const model = (x, y) => ({ x, y }) ;
console.log(model(1,2)); // retournera { x : 1, y : 2 }

// Une syntaxe plus longue mais équivalente
const model2 = (x, y) => { 
    return { x : x, y : y }
}
```

Contrairement aux fonctions classiques, les fonctions fléchées ne re-définissent pas de this. Si vous vous référez dans une fonction fléchée au mot clé this, la fonction fléchée **récupérera le this du contexte** de définition de la fonction flèchée :

```js
const School = {
    name: "Alan",
    sayHello() {
        // récupérer le this du context
        const that = this;
        function getName() {
            console.log(that.name); // Alan
            console.log(this.name); // undefined
        }
        getName();
    },

    sayHelloArrowFunc(){
        // La fonction fléchée récupère le context de l'objet courant School
        let func = () => {
            console.log(this.name); // Alan
        }
        func();
    }
}
School.sayHello();
School.sayHelloArrowFunc();
```

Une fonction classique peut définir un constructeur, **pas une fonction flèchée**, dans ce cas par convention la fonction commence par une majuscule :

```js

function User(name){
  // constructeur
  this.name = name;

  console.log(this.name);
}

const u1 = new user("Alan");
const u2 = new user("Alan");

// Le code qui suit produira une erreur 
// pas de constructeur dans ce cas
/*const userArrow = name => {
  this.name = name;

  console.log(this.name);
}

const uA1 = new userArrow("Alan");
const uA2 = new userArrow("Alan");
*/
```

Remarque, sur la fonction user et this. Si vous appelez la fonction constructeur this sans le mode strict prendra la valeur du contexte de la fonction : window par exemple... Si vous mettez le mode strict dans ce cas this est undefined et si vous appelez une propriété comme name ci-dessous une exception sera levée :

```js
'use strict';

function User(name){
  console.log(this);
  this.name = name;
}

User('Alan'); // this undefined
```

Lorsque vous appelez une fonction comme méthode d'un objet, le this est le this de l'objet précédent l'appel de la méthode, dans l'exemple ci-dessous c'est l'objet Model :

```js

const Model = {
    table : "Model",

    subModel:function(){
        console.log(this); // Objet model
    },

    // de manière totalement équivalente vous pour écrire ceci
    // pour définir une méthode/fonction
    subModel2(){
      console.log(this); // Objet model
    }
}

Model.subModel(); // this objet Model
```

### Exercice effet de bord

Comment éviter l'effet de bord sur la propriété this (undefined) dans le code suivant? Proposez une solution.

```js
const log = {
    count : 100,
    save: function () {
        'use strict';
        console.log(this.count);
    }
}
setTimeout(log.save, 500);
```

### prototype d'une fonction 

```js

const Student = {
  name : '',
  average : 17.5,
  situation: function(){
    console.log(`Name ${this.name} average : ${this.average}`);
  }
}
```

Cet objet possède une propriété **prototype**, elle listera l'ensemble des propriétés héritées depuis l'ojet Student. La quasi-totalité des objets JS héritent de l'objet **Object** de JS.

```js
Student.__proto__
```

Vous pouvez dès lors appeler des méthodes, qui ne sont pas directement disponibles (héritées) dans l'objet Student.

### Comment ajouter une propriété sur un constructeur

Reprenons l'exemple précédent, nous allons voir comment ajouter une propriété au constructeur User qui sera partagée par toutes les instances :

```js
'use strict';

function User(name, lastname){
  this.name = name;
  this.lastname = lastname;
}

let u1 = new User('Alan', 'Phi'); 

// On ajoute sur le constructeur lui-même la propriété
User.prototype.fullName = function (){

  return this.name + ' ' + this.lastname;
}

console.log(u1.fullName()); // Alan Phi
```

### Exercice prototype

Ajoutez la possibilité de définir l'age dans la fonction constructeur User et modifiez pour toutes les instances de User la fonction fullName pour qu'elle affiche maintenant : le name le fullName et l'age d'un user.

Créez maintenant les 4 users suivants :

```js 
- Alan Phi age 45 ans notes : 15, 17, 13
- Bernad Lu age 78 ans notes : 11, 12, 9
- Sophie Boo age 56 ans notes : 10, 15, 11
- Alice Car age 45 ans notes : 5, 18, 20
```

Créez un nouveau prototype average dans la fonction constructeur User, cette fonction calculera la moyenne des notes de chaque user.

Ajoutez la possibilité de définir l'age dans la fonction constructeur User et modifiez pour toutes les instances de User la fonction fullName pour qu'elle affiche maintenant : le name le fullName et l'age d'un user.s

Quand JS appelle cette méthode il ne la trouvera pas dans l'instance de User mais dans le prototype de l'instance User. Le this est donc bien le this de l'instance de User. Cette technique permet donc de créer des méthodes partagées par toutes les instances de User. Notez que vous pouvez tout à fait définir la méthode fullName après avoir fait l'instance de User.

JS possède depuis **ES6** un mot clé class pour définir une classe, nous verrons qu'en fait ce mot clé permet de définir, comme dans l'exemple précédent, un constructeur.

## Fonctions fléchées et fonction de rappel dans les tableaux

Vous pouvez utiliser une fonction fléchée sur des collections en utilisant des fonctions comme map, filter ou reduce par exemple :

- map retourne un tableau de même dimension que le tableau parcouru.

```js
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const powerNumber = numbers.map( number => number ** 2);
```

### Exercice puissance 3

Soit numbers une liste de nombres entiers, élevez à la puissance 3 les nombres pairs uniquement.

```js
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
```

*Indications : pour calculer une puissance utilisez l'opérateur suivant*

```js
// opérateur puissance
2**3 // 8
```

- filter, il permet de filtrer des données dans un tableau en fonction d'un critère.

```js
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

numbers.filter(number => number > 4);
// [5, 6, 7, 8, 9, 10]
```

- reduce. Applique un accumulateur de la droite vers la gauche et traite chaque élément de la liste.

Vous pouvez passer une valeur par défaut à la fonction reduce, deuxième paramètre. Cette valeur est facultative et par défaut vaut 0.

```js
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
// première paramètre fonction fléchée, deuxième paramètre val init de acc
const total = numbers.reduce((acc, curr) => curr + acc, 0);
console.log(total); // affiche 55

numbers.reduce((acc, curr) => curr + acc, 100);
// 155
```

### Exercice max

Reprenez l'objet numbers (array) de numériques et utilisez la méthode reduce pour calculer le max.

### Exercice puissance 3 nombres pairs

Soit la liste numbers d'entiers, filtrez les nombres pairs et les élever à la puissance 3.

```js
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
```

### Exercice reduce sum impair

Faites la somme des nombres impairs en utilisant la fonction reduce des valeurs suivantes :

```js
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
```

### Exercice fonction map

Utilisez la fonction map pour calculer le prix TTC des téléphones suivants en utilisant une fonction fléchée :

```js
const phones = [
  { name: "iphone XX", priceHT: 900 },
  { name: "iphone X", priceHT: 700 },
  { name: "iphone B", priceHT: 200 },
];
```

### Exercice counter arrow

Corrigez le code (ES5) suivant afin que le compteur s'incrémente correctement.

```js
// ES5
const CounterV1 = {
  count: 0,
  // la fonction callback function reçoit l'élément courant this
  counter: function() {
    console.log(this.count); // affiche 0
    setInterval(function () {
      this.count++;
      console.log(this.count);
    }, 1000);
  },
};
CounterV1.counter();
```

## Affectation par décomposition

Vous pouvez affecter par décomposition des variables pré-définies comme suit :

```js
let a, b;
[a, b] = [10, 20];
```

Si vous ne souhaitez affecter que quelques variables et récupérer le reste de l'assignation dans un tableau, vous devez utiliser le spread operator :

```js
let a, b, rest;
[a, b, ...rest] = [10, 20, 30, 40, 50];
console.log(rest); // [30, 40, 50]
```

Vous pouvez également sauter des arguments dans l'assignation :

```js
let a, b;
[, , a, b] = [10, 20, 11, 111];

console.log(a, b); // 11 111
```

De même vous pouvez par décomposition assigner des valeurs à des variables en fonction des clés d'un littéral, vous devez cependant dans ce cas utiliser les mêmes noms de variable que les clés du littéral :

```js
const student = { mention: "AB", note: 12 };
const { mention, note } = student;

console.log(mention); // AB
console.log(note); // 12
```

Il est parfois intéressant de renommer les clés, dans ce cas il faudra utiliser la syntaxe suivante :

```js
const student = { mention: "AB", note: 12 };
const { mention: m, note: n } = student;

console.log(m); // AB
console.log(n); // 12
```

On peut également le faire par imbrication :

```js
const st = {
  name: "Antoine",
  family: {
    mother: "Yvette",
    father: "Michel",
    sister: "Sylvie",
  },
  age: 49,
};

const {
  name,
  family: { sister },
} = st;
```

Vous pouvez également destructurer un littéral en argument d'une fonction :

```js
const student = { mention: "AB", note: 12 };
const infoStudent = ({ mention, note }) => "info : " + mention + "note : " + note;

infoStudent(student);

//notez que vous pouvez également définir la fonction infoStudent sans vous souciez de l'ordre des clés :
const infoStudent_bis = ({ note, mention }) => "info : " + mention + "note : " + note;
```

### Exercice permutations

- Permutez les valeurs a et b suivantes :

```js
let a = 1, b = 2;
```

- Soient les trois variables a, b, et c suivantes permutez les valeurs dans l'ordre suivant :

- a <- b
- b <- c
- c <- a

```js
let a = 1, b = 2, c = 4;
```

### Exercice assigner par décomposition

1. Calculez la moyenne des notes de l'étudiant. Modifiez le littéral.

2. Puis assignez les valeurs **name**, **notes** et **average** dans les constantes name, notes et average dans le script courant.

```js
let student = {
  name: "Alan",
  notes: [10, 16, 17],
  average: null,
};

// TODO ...

// constantes
console.log(name, notes, average);
```

### Exercice iterate destructuring

Soient les données suivantes affichez le nom et le nom de la soeur de chaque étudiant en utilisant une boucle for of :

// Nom : Alan soeur : Sylvie

```js
const students = [
  {
    name: "Alan",
    family: {
      mother: "Isa",
      father: "Philippe",
      sister: "Sylvie",
    },
    age: 35,
  },
  {
    name: "Bernard",
    family: {
      mother: "Particia",
      father: "Cécile",
      sister: "Annie",
    },
    age: 55,
  },
];
```

## spread operator

Vous pouvez effectuer un merge de deux tableaux en JS à l'aide de l'opérateur spread :

```js
let numbers1 = [1, 2, 3, 4, 5, 7, 8, 9, 10];
let numbers2 = [11, 12, 13];

let numMerge = [...numbers1, ...numbers2];
```

Vous pouvez également "merger" deux littéraux :

```js
const st1 = { s1: "Alan", s2: "Alice" };
const st2 = { s3: "Bernard", s4: "Sophie" };

const stMerge = { ...st1, ...st2 };
console.log(stMerge);
//{s1: "Alan", s2: "Alice", s3: "Bernard", s4: "Sophie"}
```

Le spread operator peut servir également pour "mettre à jour" une clé dans un littéral :

En reprenant l'exemple précédent :

```js
const st11 = { s1: "Alan", s2: "Alice" };
const st22 = { s2: "Bernard", s4: "Sophie" };

const stMerge = { ...st11, ...st22 };

console.log(stMerge);
// {s1: "Alan", s2: "Bernard",  s4: "Sophie"}
```

Un autre exemple de "mise à jour" avec cette technique 

```js
const state = {
  name: "",
  age: 25,
  email: "alan@alan.fr",
};

const newState = { ...state, email: "sophie@sophie.fr" };
// {name: "", age: 25, email: "sophie@sophie.fr"}
```

## Exercice push value

Soient les données suivantes. Créez un tableau strNumbers et pushez chacune des valeurs de ce tableau sans créer un tableau de tableaux. Rappelez-vous qu'une constante bloque uniquement l'assignation, mais si la constante est un objet vous pouvez toujours le modifier.

```js
const strNumbers = [];
const str1 = ["one", "two"];
const str2 = ["three", "four"];
```

## Nom de propriété calculé et décomposition

Vous pouvez utiliser une variable pour définir une clé d'un littéral, dans ce cas la syntaxe est la suivante, il faut utiliser des crochets pour que JS interprète la variable comme une clé du littéral :

```js
const state = {
  name: "",
  email: "alan@alan.fr",
};

// définition d'une clé dynamique
let name = "email";
const newState = { ...state, [name]: "bernard@bernard.fr" };
```

## Exercice ordre et longueur de mots

Utilisez la fonction sort de JS. Voir la documentation de cette fonction.

1. Ordonnez les students par ordre alphabétique. 

2. Ordonnez par ordre croissant en fonction de la longueur des noms.

```js
const students = [ "Alan", "Philippe", "Tony", "Geraldine", "Michelle", "Phi" ];
```

3. Ordonnez la liste des nombres suivants par ordre croissant :

```js
const numbers = [ 10, 7, 5, 1, 10, 5];
```

## Exercice populations

```js
const populations = [
  { id: 0, name: "Alan" },
  { id: 1, name: "Albert" },
  { id: 2, name: "Jhon" },
  { id: 3, name: "Brice" },
  { id: 4, name: "Alexendra" },
  { id: 5, name: "Brad" },
  { id: 6, name: "Carl" },
  { id: 7, name: "Dallas" },
  { id: 8, name: "Dennis" },
  { id: 9, name: "Edgar" },
  { id: 10, name: "Erika" },
  { id: 11, name: "Isaac" },
  { id: 12, name: "Ian" },
];
```

1. Soit les données suivantes populations, ordonnez-les par ordre croissant par rapport à la longueur des noms.

*Indications : utilisez la méthode **sort**, cette méthode modifie le tableau. Vous pouvez lui passer une fonction (fléchée) pour calculer l'ordre par rapport à une clé du tableau ou un calcul spécifique. Reportez-vous à la documentation : [sort](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/sort).*

2. Ajoutez une clé **lenName** aux éléments du tableau populations vous assignerez la longueur de chaque nom à cette variable.

3. Regroupez maintenant dans un nouveau tableau groupNames les noms de même longueur (même nombre de caractères).

*Indications : Imaginez une structure de données (voir l'exemple ci-après), par exemple un tableau de tableau ou un Map, vous pouvez également utiliser **filter** pour regrouper les noms de même longueur dans le nouveau tableau groupNames*

Présentez les résultats recherchés comme suit par exemple :

```js
[
  [ { id: 12, name: 'Ian', lenName: 3 } ],
  [
    { id: 0, name: 'Alan', lenName: 4 },
    { id: 2, name: 'Jhon', lenName: 4 },
    { id: 5, name: 'Brad', lenName: 4 },
    { id: 6, name: 'Carl', lenName: 4 }
  ],
  [
    { id: 3, name: 'Brice', lenName: 5 },
    { id: 9, name: 'Edgar', lenName: 5 },
    { id: 10, name: 'Erika', lenName: 5 },
    { id: 11, name: 'Isaac', lenName: 5 }
  ],
  [
    { id: 1, name: 'Albert', lenName: 6 },
    { id: 7, name: 'Dallas', lenName: 6 },
    { id: 8, name: 'Dennis', lenName: 6 }
  ],
  [ { id: 4, name: 'Alexendra', lenName: 9 } ]
]
```

4. (Facultatif) Ajoutez une clé relation au tableau population et indiquez pour chaque personne les noms de ses relations. Ordonnez ces relations par ordre croissant de nombre de relation. Affichez la personne qui le plus de relation.

```js
const relations = [
  { id : 0 , relation : [1, 2, 4]},
  { id : 3 , relation : [7, 8]},
  { id : 4 , relation : [2, 7, 8, 11]},
  { id : 5 , relation : [1, 2, 4]},
  { id : 7 , relation : [2, 3, 5, 9]},
  { id : 9 , relation : [1, 2, 4, 8, 11]},
  { id : 11 , relation : [1, 2, 9, 10,]},
]
```

## Interpolation

Vous pouvez écrire des chaînes de caractères sur plusieurs lignes et insérer des expressions JS qui seront évaluées à l'aide de backquotes (accent grave).

Intérêt la concaténation sans l'interpolation donne une expression comme suit :

```js
let a = 51;
let b = 90;
console.log("Somme " + (a + b) + " et\n multiplication " + a * b + ".");
```

Avec les backquotes on aura une expression plus facile à écrire :

```js
let a = 51;
let b = 90;
console.log(`Somme : ${a + b} et \n multiplication : ${a * b}.`);
```

On peut également intégrer des ternaires comme suit avec les cotes couchés :

```js
let isLoading = true;
const message = `Data is ${isLoading ? 'loading...' : 'done!'}`;
```

Remarque sur la syntaxe ternaire, très pratique pour écrire une condition sur une ligne :

```js

console.log( true ? 'yes' : 'no'; ); // yes
console.log( false ? 'yes' : 'no'; ); // no

```

Les ternaires sont très pratiques également pour assigner des valeurs avec une condition :

```js
logged = true ? 'yes' : 'no'; ; // yes

logeed =  false ? 'yes' : 'no'; ; // no

```

Vous pouvez enchâiner les ternaires mais, attention à la lisibilité de ces derniers.

```js
logged = true ? ( true ? 'toujours yes' : 'no' )  : 'no'; ; // toujours yes
```

## Optimisation

**Memory leak**

- JS purge le scope à la sortie de la fonction parente.

- Converse les pp appelées dans les closures.

- y compris les closures qui ne sont plus référencées.

## Ce qui est faux en JS 

0, NaN, undefined, false, "", '', ``, null

- Evaluation courcicuit, par exemple user n'est pas défini, mais ne sera pas évalué :

```js
false && user 
```
Une deuxième évaluation courcicuit, renverra true

```js
true || user
```

## Exercices supplémentaires

### Exercice accumulator

Créez une fonction récursive (qui s'appelle elle-même, elle prendra deux arguments : un tableau de nombres et un accumulateur initialement égale à 0. Cette fonction retournera la somme des valeurs du tableau.

Utilisez la méthode shift() sur le tableau. Il permet de dépiler la première valeur du tableau. Dans votre fonction récursive définissez **une condition d'arrêt**, sinon la fonction continuera de s'appeler indéfiniment (Stack Overflow).

Voyez l'exemple suivant pour vous aider à faire cet exercice :

```js

let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// retourne la première valeur du tableau en la supprimant du tableau
numbers.shift();

function accumulator(numbers, acc = 0) {
  // Une condition d'arrêt et retourner la somme des valeurs du tableau
  // dans la fonction on ré-appelle la fonction elle-même
  // accumulator(numbers, 10);
}

console.log(accumulator(numbers)); // doit retourner 55
```

## Exercice copie profonde

Faites une copie profonde de l'objet suivant :

```js
const students = [
  {
    name: "Alan",
    address : [ {"street" : "Chateau"}, { "street" : "Cholvy"} ],
    family: {
      mother: "Isa",
      father: "Philippe",
      sister: "Sylvie",
    },
    age: 35,
    notes : [11, 12, 15]
  },
  {
    name: "Bernard",
    address : [ {"street" : "La Place"}, { "street" : "Lewis Carrol"} ],
    family: {
      mother: "Particia",
      father: "Cécile",
      sister: "Annie",
    },
    age: 55,
  },
];


```
