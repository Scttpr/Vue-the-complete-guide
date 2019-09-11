# Se connecter au backend

* Firebase : https://firebase.google.com/docs/database/
* Axios : https://github.com/axios/axios

* Le cours se connecte au backend via Firebase, je passe la partie de configuration.

* `this.$emit('eventName', this.maData)` === Créer un event personnalisé

```js
// Dans le script de la page
import axios from 'axios';
import AdminPostForm from '...';

export default {
    layout: 'admin',
    components: {
        AdminPostForm,
    },
    methods: {
        // Post data to the server
        onSubmitted: (postData) => {
            axios.post('URL', postData)
                .then(result => console.log(result))
                .catch(err => console.log(err));
        }
    }
}
```

```js
// Dans le store
actions: {
    nuxtServerInit(vuexContext, context) {
        return axios.get('URL')
            .then(response => {
                // Pour transformer la réponse en array
                const postArray = [];
                for (const key in response.data) {
                    postsArray.push({ ...response.data[key], id: key })
                }
                vuexContext.commit('setPosts', postsArray);
            })
            .catch(err => console.log(err))
    }
}
```

