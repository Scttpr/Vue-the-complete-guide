# List & conditions

## Conditions

* `<p v-if="myCondition">Hello</p>` == Directive de condition
* `<p v-else="myCondition">Hello</p>` == Lié au v-if le plus proche
* La directive `v-else-if` est disponible à partir de la version 2.1 de VueJS

* `<template></template>` == Template est une balise non rendue, permet d'ajouter du contenu conditionnel à l'intérieur (organise le code côté templating)

* `v-show="myCondition"` == Cache le contenu de la balise selon la condition plutôt que de le supprimer complètement du rendu final

## Boucles

* `<li v-for="(item, index) in items" :key="uniqueKey">{{ item }} - {{ index }}</li>` == Directive de boucle, il faut bind une key pour optimiser les performances et produire un code plus sûr
* Il est aussi possible de placer le v-for sur le template pour générer une liste depuis un groupe de balise

* Boucler sur un array d'objets :
```html
<!-- Une boucle sur un objet peu utilisé la syntaxe ci-dessous pour parcourir l'intérieur de l'objet et mobilisé ses valeurs et ses clés -->
<li v-for="item in items">
  <span v-for="(value, key, index) in item">{{ value }} - {{ key }} - {{ index }}</span>
</li>
```

* `<li v-for="n in 10">{{ n }}</li>` == Boucler jusqu'à 10

## Documentation

* Official Docs - Conditionals: http://vuejs.org/guide/conditional.html* 
* Official Docs - Lists: http://vuejs.org/guide/list.html