# Vers un workflow avec webpack et Vue CLI

* Guide sur les single file components : http://vuejs.org/guide/single-file-components.html
* Méthode Render : http://vuejs.org/guide/render-function.html
* Doc Vue CLI : https://github.com/vuejs/vue-cli
    * __Pour avoir un CSS Loader & Sass, utiliser le template webpack__


## Utiliser Vue CLI pour créer un projet

* Vue CLI a pour principale fonction de fetch des VueJS project templates :
    * simple (index.html + Vue CDN import)
    * webpack-simple (Basic Webpack Workflow)
    * webpack (Complex Webpack (incl. testing))
    * browserify / browserify-simple (browserify workflow)

```bash
# Installer Vue CLI
npm install -g vue-cli

# Créer & installer mon projet
vue init webpack-simple nom-du-projet
cd nom-du-projet
npm install
npm run dev
```

## L'architecture du template Webpack

* Un dossier `src` qui contient le code source
* `index.html` === Page servie par l'application qui importe une version build de notre application

## Les fichiers .vue

* `main.js` === "Front Controller", porte d'entrée des composants.
    * Localise `el` et render un template VueJS à l'endroit du `el`, ici notre template est App du fichier App.vue
    * Il est aussi possible de "monter" son application avec deux autres méthodes (sans le render) :
```js
// 1- Using the ES6 Spread Operator (for that, you need to add babel-preset-stage-2 as a Dependency and to your .babelrc File):
// npm install --save-dev babel-preset-stage-2 
// .babelrc:

{
    "presets": [
    ["es2015", { "modules": false }],
    ["stage-2"]
    ]
}

// main.js
import Vue from 'vue'
import App from './App.vue'
    
new Vue({
    el: '#app',
    ...App
});

// 2- Using mount() :
// Also install the stage-2 preset as described above.

import Vue from 'vue'
import App from './App.vue'
    
const vm = new Vue({
    ...App
});
    
vm.$mount('#app');
```

* `App.vue` === Composant principal :
```html
<!-- Single file template qui sera compilée en JS au moment du build et importé dans index.html -->
<template>
    <h1>Hello world</h1>
</template>

<script>
    export default {
        // Cet objet se comporte comme une instance VueJS
    }
</script>

<style>

</style>
```

## Build l'application pour la production

```bash
# Build l'application pour le déploiement
npm run build
```

