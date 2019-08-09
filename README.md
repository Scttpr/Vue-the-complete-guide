# Vue.js the complete guide by M.Schwarzmuller

__NOTES PROVENANT DU COURS UDEMY "VUEJS 2 - THE COMPLETE GUIDE (incl. VUE ROUTER & VUEX) by M.SCHWARZMULLER__

## Our first Vue application

> https://vuejs.org/v2/guide/installation.html

* Il est possible de télécharger Vue.js ou d'utiliser un lien CDN à ajouter dans une balise script en début de fichier

### HTML

```html
<!-- Il est possible d'enlever le @2.6.10 pour systématiquement chargé la dernière version -->
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.10/dist/vue.js"></script>

<div id="app">
  <!-- Ajouter v:on crée un listener sur la balise, elle exécute le code référencé dans la string (ici changeTitle) -->
  <input type="text" v-on:input="changeTitle">
  <!-- Pour intégrer la data double accolade et  clé de la data ! -->
  <p>{{ title }}</p> 
</div>
```

### JS

```js
// Crée une instance de vue
new Vue({
  el: '#app', // el est reconnu par Vue, il prend une string en value et décide de quel élément HTML (et de ses enfants) sera controlé par cette instance de vue
  data: {
    title: 'Hello world !',
  }, // Les datas du composant sont stockées dans un objet
  methods: {
    changeTitle: (evt) => {
      this.title = evt.target.value; // this fait référence aux datas et méthodes de l'objet instancié
    },
  }, // Toutes les méthodes nécessaire dans le composant
})
```

## Plan du cours

* Interaction avec le DOM (templates)
* Comprendre les instances VueJS
* Vue CLI
* Les composants
* Gérer les formulaires
* Directives, filtres & mixins
* Animations & transitions
* Travailler avec HTTP
* Routing
* Gestion du state
* Déploiement d'une application VueJS

## Installer VueJS en local

Il est possible d'installer VueJS en local en téléchargeant le script depuis le site.
Ensuite il faut l'ajouter dans le <head> du html pour importer le script