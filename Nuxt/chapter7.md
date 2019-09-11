# Middleware & Authentification

## Qu'est-ce qu'un middleware ?

* Un middleware est une fonction qui reçoit le context en param, le code est éxécuté avant qu'une page soit chargée
    * /!\ Un code asynchrone doit renvoyer une promesse !
    * Le niveau le plus bas pour l'attacher est à l'échelle d'une page, sinon il faut le configurer dans l'objet router du fichier nuxt-config :
    ```js
    export default {
        middleware: 'log', // Le fichier du middleware doit être  dans le dossier middleware
    }
    ```

* Voir le code directement pour le login et signup

## Stocker le token

* Utiliser le store en créant une mutation `setToken()` qui doit commit le token au state, si on return une promesse on peut utiliser then pour éxécuter du code asynchrone dans les pages, composants

* Faire persister le token :
    * Dans une SPA on stocke le token dans le localstorage, ici on recharge sur le serveur et donc on n'a pas accès au localstorage
    * Ajouter le token au localstorage à l'initialisation du token avec son expiration
    * Créer une action initAuth qui récupère le token son timestamp d'expiration avant le chargement de l'app, si le token est valide, alors on commit setToken !
    * Créer un middleware checkAuth et l'ajouter partout où il y en a besoin (avant le auth middleware, ils s'éxécutent dans l'ordre !) :
    ```js
    export default function (context) {
        if (process.client) {
            context.store.dispatch('initAuth');
        }
    }
    ```
    * Pour accéder au token côté serveur il faut utiliser les cookies : `npm install --save js-cookie` >> `import Cookie from 'js-cookie'`
        * Si je suis sur le serveur, je récupère dans les cookies, sinon j'exécute mon code classique, cf code dans le store

* Créer un middleware qui redirige l'utilisateur s'il est auth ou pas et si non, le redirigé :
```js
// dans le store créer un getter
getters : {
    isAuth(state) {
        return state.token != null;
    }
}

// Dans le fichier du middleware et ajouter au layout ou aux pages concernées
export default function (context) {
    if (!context.store.getters.isAuth) {
        context.redirect('admin/login');
    }
}
```

* Invalider un token :
    * Ajouter une mutation qui clearToken();
    * Créer une action qui prend un setTimeout après une duration définie et commit clearToken à la fin du timer
    * Exécuter l'action à l'initialisation du token
