# Configuration de Nuxt, plugins & modules

* Vue Meta package: https://github.com/declandewet/vue-meta
* Detailed documentation of all settings: https://nuxtjs.org/api/
* Detailed documentation of environment variables: https://nuxtjs.org/api/configuration-env
* All possible settings/configurations router: https://nuxtjs.org/api/configuration-router


* Le fichier est lancé à chaque lancement de l'application
* `head` === Permet de paramétrer le head de toutes les pages, utilise le view-meta package
    * Pour overwrite le head, dans les Pages composants, ajouter une propriété `head` à l'objet exporté

* `loading` === Barre de progression au changement de page, il est possible de la paramétrer (couleur, duration, hauteur, etc.) ou de la supprimer
    * Si travail en SPA, on peut ajouter `loadingIndicator` qui sera affiché lors du premier chargement côté client
* `css`=== array dans lequel on passe des strings avec le chemin vers les fichiers css
* `dev` === (possible de l'ajouter), spécifier si nous sommes en dev mode ou non (est overwrite par les scripts nuxt, build & start le change en false de toute façon)
* `env`=== Permet de paramétrer des variables d'environnement :
```js
env: {
    baseUrl: process.env.BASE_URL || 'mon-url',
}
// On utilise ensuite la variable via process.env.baseUrl
```
* `generate` === Paramétrer la façon dont Nuxt génère les pages statiques
* `rootDir` === Permet de définir la racine du projet (le changer pour src par exemple), cf la doc
* `router`=== Permet de modifier la mécanique du router, cf la doc
    * `extendRoutes(routes, resolve) { routes.push({ path: '*', component: resolve(__dirname, 'pages/index.vue') }) }` === Permet de rediriger vers l'accueil en cas de mauvaises routes

* `srcDir` === Ou sont les documents sources (pages, middlewares, etc.)
* `transition` === Peut être une string ou un objet :

```js
transition: {
    name: 'fade', // Premier mot de la classe qui gère l'animation, param le CSS nécessaire
    mode: 'out-in'
}
```

* `plugins` === Fonctionnalités qui permettent d'éxécuter du code avant que l'application soit montée.
    * Pour monter les composants et les rendre disponible partout dans l'application : Dans le dossier plugins, créé un fichier js où on importe les composants qu'on veut utiliser ainsi que Vue :
    ```js
    // il faut du coup enregistrer le plugin : ~plugins/core-components --- Plus besoin d'enregistrer les composants dans les pages, etc.
    import Vue from 'vue';

    import MyComponent from '@/components/MyComponent';

    Vue.component('MyComponent', MyComponent);
    ```

* Enregistrer un filtre de date pour formater : cf ressources dans le dossier plugins
* `modules`=== Ajouter des fonctionnalités venant de la liste des modules disponibles et compatibles sur NPM/ Github, voir sur awesome-nuxt Github
    * Il est ensuite possible de paramétrer un module dans le fichier de configuration
    * Pas besoin d'importer un module dans les composants, pages
