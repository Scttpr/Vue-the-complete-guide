# What is Nuxt ?

C'est un outil de développement qui facilite les projets VueJS, notamment côté Server Side Rendering (rendre les pages côté serveur et les servir ensuite au client). Il se configure via son architecture.

## Server side rendering ?

* La page index.html servie par VueJS peut-être générée côté serveur pour servir une page déjà rendue (mieux pour le SEO). Nuxt crée et optionellement rend l'application VueJS et facilite donc grandement le SSR.

## Créer une app Nuxt

```bash
# Nécessite Node.js & Yarn || NPM
npm install -g create-nuxt-app
create-nuxt-app <my-app>
# Suivre la procédure d'installation

# Lancer le serveur de développement
npm run dev
```

## Architecture

* Pages === Nuxt configure le projet via les dossiers (on ne peut pas modifier le nom des dossiers)
    * Les pages correspondent aux routes, index.vue est la racine
