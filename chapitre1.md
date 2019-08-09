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

* `<button v-on:nomEvent="eventHandler"></button>` == Permet d'ajouter des events listeners dans les templates