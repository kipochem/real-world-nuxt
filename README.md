# real-world-nuxt

## Build Setup

```bash
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm run start

# generate static project
$ npm run generate
```

For detailed explanation on how things work, check out [Nuxt.js docs](https://nuxtjs.org).

# 3 project added to GitHub

# 4 Nuxt Component Folder Structure

- no /src directory anymore, folders are directly in root

## Basic folders

### layouts: contains yours layouts

- contains per default always the default layout default.vue

### pages: contains the top level views (used to generate routes)

- contains per default always a default page index.vue which gets rendered inside the default layout

### components: contains reusable Vue components

- contains per default always a default component Logo.vue which gets rendered inside the default index.vue page

### store: contains vuex store files

### static: files that should appear exactly as they are

- e.g. robots.txt, favicon

### assets: uncompiled assets

- css, Sass, images, fonts

### JS plugins which load before vue app is loaded

- helpers, libraries

### middleware: custom functions to run before rendering a layout page

### nuxt.config.js Used to modify the default nuxt configuration

INFO: nuxt adds component functionality based on which directory the component is in

# 5 Creating first pages and routes

INFO: Every time a page gets created, nuxt creates automatically a route based on the file name of the page in the router file in the '.nuxt' folder

## Fix settings in VS Code - not necessary in Atom

## Copy/paste some global styles into layouts/default.vue

INFO: the <nuxt /> tag plays the same role as </router-view>

- in layouts/default.vue, add an id to the root div and replace the default styles with the styles from the starter code template in lesson 2

## Simplify pages/index.vue

- delete eveything a scaffold a new component

## startup dev server to check if everything works

npm run dev

## create second page in pages/create.vue

- add a new page create.vue and copy paste the code from the page index.vue adapting the title

## create new comnponent in components/NavBar.vue

- delete the default logo.vue
- create a new component NavBar.vue
- - inside NavBar.vue, create a few links called nuxt-link (same as router-link)
- - inside NavBar.vie, paste in the styles from the start code in lesson 2

## user NavBar.vue component inside the layout/default.vue

- in layout/default.vue, import the NavBar
- in layout/default.vue, register the NavBar
- in layout/default.vue, use the NavBar by adding it to the template
