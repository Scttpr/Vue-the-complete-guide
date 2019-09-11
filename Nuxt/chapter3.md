# Gérer les données & VueX

```js
export default {
    props: {
        posts: {
            type: Array,
            required: true,
        }
    }
}
```

```html
<template>
    <!-- Mon composant avec son array de datas -->
    <PostList :posts="loadedPosts" />
</template>

<script>
import PostList from '@/components/PostList';

export default {
    data() {
        return {
            loadedPosts: [
                { /* mon post avec toutes ses props */},
                { /* idem */ }
            ]
        }
    }
}
</script>
```

* Dans une app VueJS on charge les data dans le `created()` lifecycle, ça fonctionne sur Nuxt mais le code est lancé sur le client, ce n'est pas idéal car on voit les temps de chargement (la page est rerendue, etc, etc.).
    * Pour fetch les données sur le serveur pour ensuite servir la page (UNIQUEMENT SUR LES PAGES) :
    ```js
    export default {
        asyncData(context, cb) {
            // Charge sur le serveur et rends ensuite
            // ATTENTION, dans ce contexte, this n'est pas utilisable pour accéder à l'instance de VueJS
            // Il faut fournir une idée du temps que ça va prendre, via une promesse par exemple ou via l'utilisation du cb

            // S'il y a une error, elle est throw grâce à context.error()
            cb(null, {/* Mes datas */})

            // Avec une promesse, pas besoin de cb :
            return new Promise((resolve, reject) => {
                resolve({/* mes datas */})
            })
            .then(data => data)
            .catch(err => context.error(err))
        }
    }
    ```

    * Une fois que la page est chargée une fois, on passe sur le même fonctionnement qu'une SPA, on passe donc côté client et le code se lance dans le client ! (Pour les requêtes asynchrones, Nuxt rend la barre de chargement en haut et se comporte comme au chargement de la page)

* L'objet `context` Contient toutes les infos de l'instance VueJS qui permet d'aller chercher les datas (comme les params) depuis la fonction `asyncData()`

## VueX

* Le store est déjà built-in, il y a deux méthodes :
    * Ajouter index.js dans store/
    * Un seul store pour toute l'application
    * Définie les mutations, les actions, getters dans un seul fichier

    * Sinon deuxième méthode, créer des fichiers multiples dans le store/
    * Chaque fichier devient un namespace
    * On sépare le code dans les différents fichiers

```js
import Vuex from 'vuex';

const createStore = () => {
    return new Vuex.Store({
        state: {
            loadedPosts: []
        },
        mutations: {
            setPosts(state, posts) {
                state.loadedPosts = posts;
            }
        },
        actions: {
            setPosts(vueContext, posts) {
                vuexContext.commit('setPosts', posts);
            }
        },
        mutations: {}
    });
}

// Pour accéder au store il suffira d'utiliser $store.maData ou $store.dispatch('ma fonction', this.monParam);
export default createStore;
```

* On peut également initialiser le store à la place de `asyncData()` grâce à `fetch()`. Fonctionne comme asyncData, à la place on ne retourne pas de data mais on dispatch ou commit via `context.store.commit()`

* `nuxtServerInit(vuexContext, context) { return new Promise( cf le code du cours !) }` === Action spéciale dans le store propre aux actions qui sera dispatch par Nuxt