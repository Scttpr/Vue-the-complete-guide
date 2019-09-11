# L'instance Vue.js (chapitre théorique)

* La doc officielle : https://vuejs.org/v2/guide/instance.html
* Le code sur l'instance : https://jsfiddle.net/smax/9a2k6cja/2/
* Le code sur les cycles de vie : https://jsfiddle.net/smax/jcgw7ak8/

## Utiliser plusieurs instances

Il est possible d'utiliser plusieurs instances Vue.js. Toutefois, dans une instance on ne peut pas accéder aux propriétés d'une instance avec une autre. Pour parsemer un site de Vue.js c'est donc possible.

## Accéder à l'instance depuis une autre instance

On stocke l'instance dans une variable et on utilise cette variable dans la seconde :
```js
var vm1 = new Vue({...});
var vm2 = new Vue({
    // vm1.props sont disponibles ici ! Attention, le proxy fonctionne également ici donc pas de vm1.data.props
});
```

## Comment Vue.js gère les datas et methods

Au moment de l'instanciation, Vue.js copie les props dans l'objet. Une prop ajoutée après n'a pas de getter et setter et donc n'est pas reactive

## $el, $data

Toutes les propriétés avec des `$`sont utilisables dans l'instance.
* `$el` fait référence à l'élément parent.
* `$data`permet d'accéder aux datas depuis l'extérieure === `console.log(vm1.$data.title);

Vue.js peut donc interagir du JS Vanilla ! Il est parfaitement possible de mélanger Vue.js à un projet classique !

## $refs

* `<button ref="myButton">Bouton</button>` === Ajoute une clé reconnue par Vue.js à une balise, celles-ci sont accessibles dans et hors de l'instance Vue.js !
* `console.log(this.refs.myButton.innerText)` === Permet d'aller chercher des références dans le DOM et de travailler dessus !

## Monter un template

* Vue.js crée un template interne et le met à jour et re-render le DOM
* `vm1.$mount('#app)` === Permet de monter l'élément dans l'instance, pratique si on ne sait pas où monter l'instance avant de la paramétrer !

```js
// Il est possible de créer un template au moment de l'instanciation
const vm3 = new Vue({
    template: '<h1>Hello</h1>',
})

// On monte ensuite l'instance
vm3.mount();
document.getElementById('app3').appendChild(vm3.$el);
```

ATTENTION : Cette façon de faire n'est pas optimale et peu courante !

## Utiliser un composant

```js
// Création d'un composant basique
Vue.component('hello', {
    template: '<h1>Hello</h1>'
});
```

```html
<!-- Insertion du composant dans l'HTML -->
<hello></hello>
```

## Quelques limites au template

Ce n'est pas pratique d'écrire le template et donc les balises dans une string.

Il y a deux versions de Vue.js, une qui compile dans le navigateur (celle vu jusque là), l'autre qui précompile l'application pour build une SPA.

## Comment Vue.js met à jour le DOM

Vue.js crée un DOM virtuel qui représente le DOM réel en JS, Vue.js écoute les changements et recrée le DOM virtuel. Si le DOM virtuel a changé il update le DOM réel.

## Cycles de vie

`new Vue()` > `beforeCreate()` > Initialise les datas & events > instance créée (`created()`) > Compile les templates ou el > `beforeMount()` > Remplace el avec le template compilé > Monté dans le DOM > Les données changent > `beforeUpdate()` > Re-render DOM > `updated()` > On veut détruire > `beforeDestroy()` > Destroyed > `destroyed()`