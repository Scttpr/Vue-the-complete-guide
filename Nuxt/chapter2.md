# Pages, Routing & views

* https://academind.com/learn/css/understanding-css/flexbox-basics-container
* https://nuxtjs.org/guide/routing
* https://nuxtjs.org/guide/views

## Des dossiers aux routes

* Il faut créer un dossier avec un fichier dedans === `/signup` avec `index.vue` à l'intérieur
    * Cela marche en créant un fichier `signup.vue` à la racine ou le faire dans le dossier avec le nom `index.vue`

* Param dynamique === Dans le dossier concerné, créer un fichier `_id.vue` (ou un dossier _id avec un fichier `index.vue`)
    * Pour récupérer le param dans le template : `{{ $route.params.id }}` id car le fichier s'appelle `_id.vue`

* Ajouter les liens pour naviguer :

```html
<template>
    <!-- Un lien classique force la page à se recharger, ce n'est pas le comportement d'une SPA -->
    <nuxt-link to="/users">Users</nuxt-link>
</template>
```

```html
<template>
   <input type="text" v-model="userId">
   <button @click="onLoadUser">Load user</button>
</template>

<script>
    export default {
        data() {
            return {
                userId: ''
            }
        },
        methods: {
            onLoadUser() {
                // Permet de naviguer avec du code VueJS dans Nuxt
                this.$router.push('/users/' + this.userId);
            }
        }
    }
</script>
```

## Valider les params

* Les composants Pages ont des props spécifiques (notamment la validation de routes)
    * Valider un param dynamique :
    ```js
    export default {
        // Méthode spéciale fournie par Nuxt
        validate (data) {
            // Pour limiter le param dynamique à 1 (ATTENTION, TOUT CE QUI VIENT DE L'URL EST DE TYPE STRING)
            // Il est possible de tester avec des REGEX !
            return data.params.id == 1;
        }
    }
    ```

## Nested routes

* Pour créer des nested routes il faut ajouter un fichier `mon_chemin.vue` à côté du dossier `mon_chemin` puis ajouter le contenu :
```html
<template>
    <!-- Le contenu que je veux répéter dans les différentes routes -->

    <!-- Le contenu spécifique -->
    <nuxt-child />
</template>
```

## Un peu de théorie

* Layouts === Les Pages sont rendues dans le layout
* Pages === Peuvent avoir des nested Pages et/ou des composants
* Components === Les composants sont des composants :D

## Ajouter un layout

* De base il existe un fichier `default.vue`, un bon endroit pour faire le style général de l'app
* On peut créer un layout pour des pages spécifiques (les utilisateurs, le back-office, etc.)
    * Pour cela il faut ajouter la prop layout à la page :
    ```js
    export default {
        ...,
        layout: 'users',
    }
    ```

## La 404

* Dans les layouts créé `error.vue` (nom réservé), Nuxt fait la magie !

## Ajouter du style

* Pour ajouter un style global on peut utiliser le dossier assets et ajouter un fichier css, il faut ensuite ajouter le fichier à la configuration nuxt dans l'array css !
* Sinon on peut ajouter aux layouts
* Ou dans les pages ou les composants !