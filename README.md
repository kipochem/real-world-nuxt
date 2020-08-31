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
