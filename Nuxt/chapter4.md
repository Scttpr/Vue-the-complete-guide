# Premier projet

*  Ajouter des liens dans le `head` via le fichier de configuration Nuxt !
* `nuxt-link :to="'/tata/' + 1"` === Pour rendre un lien réactif

* Passer des props :
```js
// L'export du composant
export default {
    name: 'PostPreview',
    props: {
        {
            title: String,
            required: true
        },
        {
            content: String,
            required: true
        }
    }
}
```

```html
<!-- Utilisation du composant -->
<PostPreview title="tata" content="tutu" />
```

* `'~assets/images/my-img.jpg'` === lien vers le dossier assets
* `nuxt-link-active`=== Lien actif sous nuxt, possible d'y faire référence en CSS

* `v-bind="$attrs" @click="$listeners" @input="$emit('input', $event.target.value)` === Pour attribuer des valeurs de props aux composants