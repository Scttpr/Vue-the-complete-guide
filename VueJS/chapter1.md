# Interaction avec le DOM

* `{{ }}` == interpolation, permet de servir les datas & methods provenant de l'instance VueJS
  * `{{ data }}` == utiliser une data
  * `{{ method() }}` == utiliser une méthode

* VueJS crée un HTML en interne et génère du "vrai" HTML à la demande, la mécanique se fait dans l'instance VueJS
* Dans le code JS, `this` fait référence à toutes les propriétés et méthodes de l'instance. VueJS fait donc office de proxy pour éviter l'utilisation de `this.data.myData`
* __/!\ Il est impossible d'utiliser l'interpolation dans une balise HTML, on utilise `v-bind` à la place :__

```js
// Ici on utilise une directive : v-bind:refDeMonAttribut="maData" pour rendre l'intérieur de la balise dynamique
<p> {{ title }} - <a v-bind:href="link">Mon lien</a>
```
* `<p v-once>{{ data }}</p>` == Permet de rendre un contenu une seule fois, il ne sera pas update par la suite (permet de conserver une valeur initiale par exemple)

* `<p v-html="monHTMLBrut"></p>` == Permet de rendre du HTML brut dans le template

* `<button v-on:nomEvent="eventHandler"></button>` == Permet d'ajouter des events listeners dans les templates, passe automatiquement l'objet event au handler
  * Il est possible de faire passer son propre argument et/ou de faire passer son argument et l'objet event via `$event` :
    * `<button v-on:nomEvent="eventHandler(arg1, $event)"></button>`
    * `<span v-on:nomEvent.stop=""></span>` == Permet de modifier un event, ici de faire un `stopPropagation()` sur le span (il existe aussi prevent pour `preventDefault()`)
    * `<input type="text" v-on:keyup.enter.space="myMethod">` == Un modifier qui permet de spécifier la touche sur laquelle l'event doit se lancer, les modifiers peuvent être chainés !

* __Dans tous les endroits où il est possible d'écrire du code relatif à l'instance de VueJS, on peut écrire du JS natif (calcul, ternaire, etc) tant qu'il n'est pas complexe (pas de condition et de boucle pour le moment)__

* `<input type="text" v-model="name">` == Permet de faire un binding réciproque, la propriété name sera mise à jour par l'input et servie également (v-bind + v-on en quelque sorte)

* L'instance VueJS utilise également les propriétés computed & watch :
```js
new Vue({
  el: #app,
  data: {
    title: 'myTitle',
  },
  computed: {
    // Toutes les propriétés computed sont utilisées comme les data, même si ce sont des fonctions
    output: function() {
      // Le code ici est éxécuté uniquement si la propriété concernée est updatée
      // Cela permet d'éxécuté du code uniquement lorsque cela est nécessaire !!!
    },
  },
  watch: {
    // Ici il faut faire match une data avec un watch
    title: function(value) {
      // Le code que je veux éxécuter quand cette data est modifiée
      // Computed est plus optimal donc il faut le préférer au maximum
      // Watch permet de gérer facilement la mise à jour d'une data de façon asynchrone
    }
  },
  methods: {
    myMethod: function() {
      // Le code ici est forcément éxécuté même si on en a pas besoin
      return 'toto';
    }
  }
})
```

* __Des raccourcis :__
  * `<button @click="myMethod">Click</button>` === `<button v-on:click="myMethod">Click</button>`
  * `<a :href="myLink">Link</a>` === `<button v-bind:href="myLink">Link</button>`

## Le CSS

* Pour gérer dynamiquement des classes il faut :
  * Créer une propriété booleenne pour la classe
  * bind la class et lui donner un objet avec le nom de la classe et la propriété booleenne

HTML

```html
<!-- Ici la div .standardClass prendra la class .red si la propriété isActive est true .blue si elle est fausse, en cliquant dessus on peut toggle la valeur -->
<div id="app">
  <div
    class="standardClass"
    @click="isActive = !isActive"
    :class="{ 'red': isActive, 'blue': !isActive }"
  ></div>
</div>
```
JS

```js
new Vue({
  el: '#app',
  data: {
    isActive: false,
  }
})
```

* Il est possible d'utiliser les propriétés computed pour paramétrer un objet et le bind comme un param dans le HTML :

HTML

```html
<!-- Ici la div .standardClass prendra la class .red si la propriété isActive est true .blue si elle est fausse, en cliquant dessus on peut toggle la valeur -->
<div id="app">
  <div
    class="standardClass"
    @click="isActive = !isActive"
    :class="myClasses"
  ></div>
</div>
```
JS

```js
new Vue({
  el: '#app',
  data: {
    isActive: false,
  }
  computed: {
    myClasses: function() {
      return {
        red: this.isActive,
        blue: !this.isActive,
      }
    }
  }
})
```

* C'est également possible d'attaché un nom de classe directement dans le bind de class et d'attaché plusieurs classes grâce à un array :
```html
<!-- Ici l'exemple est redondant mais il montre qu'on peut attacher plusieurs classes via plusieurs format : objet ou string, ici color vaut une string qui correspond à une classe CSS -->
<div id="app">
  <div
    class="standardClass"
    @click="isActive = !isActive"
    :class="[color, myClasses, { 'red': isActive }]"
  ></div>
</div>
```

* __La mécanique est la même pour l'attribut style !!!__

## Documentation

* Official Docs - Getting Started: http://vuejs.org/guide/
* Official Docs - Template Syntax: http://vuejs.org/guide/syntax.html
* Official Docs - Events: http://vuejs.org/guide/events.html
* Official Docs - Computed Properties & Watchers: http://vuejs.org/guide/computed.html
* Official Docs - Class & Style Binding: http://vuejs.org/guide/class-and-style.html