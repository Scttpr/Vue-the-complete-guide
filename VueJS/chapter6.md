# Une introduction aux composants

* http://vuejs.org/guide/components.html
* https://vuejs.org/v2/guide/components-registration.html

```js
// Créer un composant
Vue.component('my-cmp', {
    // On utilise pas d'objet pour ne pas interférer avec l'instance VueJS
    // Vu que les méthodes sont propre à un composant, cela permet de ne pas avoir de conflit sur la data d'un composant réutilisé plusieurs fois !
    data: function() {
        return {
            title: 'Hello world'
        }
    },
    template : '<h1>{{ title }}</h1>',
    methods : {
        // Ici on peut utiliser l'objet car les fonctions sont propres aux composants
    }
});
```

```html
<!-- Utiliser le composant -->
<div id="app">
    <my-cmp></my-cmp>
</div>
```

## Enregistrer un composant localement et globalement

```js
// Pour enregistrer localement
const myComp = Vue.component(...)

new Vue({
    components: {
        'my-cmp': myComp,
    }
})
```

## Le composant Root

```html
<template>
    <h1>{{ title }}</h1>
</template>

<script>
    export default {
        // Fonctionne comme un composant
        data: function() {
            return {
                title: 'Hello world',
            }
        }
    }
</script>

<style>

</style>
```

## Créer & utiliser les composants

```html
<template>
    <h1>{{ title }}</h1>
</template>

<script>
    export default {
        data: function() {
            return {
                title: 'Hello world',
            }
        },
        methods: {
            // On peut utiliser la syntaxe ES6 maintenant que nous travaillons avec le workflow
            changeTitle() {
                this.title: 'Hello Tata';
            }
        }
    }
</script>

<!-- Ajouter le mot clé scoped permet d'appliquer le CSS uniquement au composant et non à la totalité des fichiers -->
<style scoped>
</style>
```

* Pour utiliser un composant localement il faut l'importer dans la balise script et l'ajouter dans l'objet components de l'objet de l'export !
* Pour utiliser globalement il faut utiliser Vue.component('myComp', MyComp)
* On peut ensuite utiliser un composant comme une balise HTML dans VueJS avec les directives.