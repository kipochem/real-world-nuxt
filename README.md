# real-world-nuxt

# Table of Contents
1. [Example](#example)
2. [Example2](#example2)
3. [Third Example](#third-example)
4. [Fourth Example](#fourth-examplehttpwwwfourthexamplecom)


## Example
## Example2
## Third Example
## [Fourth Example](http://www.fourthexample.com) 

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

# 6 Universal mode

see explanation 0:31 - 4:11

- build the nuxt app with 'npm run build' for production mode.
  nuxt creates a js-file for each page, splitting them this way into chunks and making initial load faster
  because only the needed js file will be loaded
- start the production level app with 'npm start'
  -- when loading the page with JS disabled, the pages will load anyway, because the HTML was rendered serverside and sent to the browser
  -- once JS gets enabled. js gets loaded, vue instantiated and the page hydrated
- smart prefetching: nuxt-links (in the template) only get loaded when they are visible on the page in the viewport, mean
  when the page is scrolled somewhere where the link is not visible, the correponding page is not fetched. once the page scrolls
  so the link is visible, it will automatically fetch the correponding page from the server

# 7 SEO in Nuxt with vue meta

https://vue-meta.nuxtjs.org/

INFO: vue components do not provide adding meta tags. With the vue-meta library they can be added

- in pages/index.vue, add a head() function returning the title and the meta tags (03:35)
- in pages/inde.vue, copy the whole script tag and paste it into pages/create.vue and adapt the title and description (04:01)
  = eliminate title duplication on each page
- in pages/index.vue, first copy the whole head() method, then adapt the title string and delete the meta completely (05:20)
- in layouts/default.vue, paste in the head() method (05:26)
  = make meta of index.vue the default one. this way, when no meta is added to another page, it takes the default one automatically
- in layouts/default.vue, adapt the title to titleTemplate which every page should use. %s takes in the title from each page (05:42)
- in pages/create.vue, adapt the title, so that only the individual part stays (06:14)
  INFO:thanks to universal mode, the meta tags for each page are rendered serverside, so even if js is turned off, the meta tags will still be displayed

<figure class="video_container">
  <video controls="true" allowfullscreen="true">
    <source src="test1.mp4" type="video/mp4">
  </video>
</figure>

# 8 File-based Routing

- run the dev server 'npm run dev'
###  <u>automatic router path update (showcase)</u>
- open .nuxt/router.js and go to the /pages folder
- inside /pages create a new folder 'create'
- move the create.vue component inside the create folder and watch __the routes update their paths automatically__
- adapt the path in the component NavBar.vue manually

###  <u>creating dynamic routes in nuxt</u>
- dynamic routes in nuxt start with an underscore: inside pages/event create a dynamic page '_id'. This will create automatically a dynamic route in .nuxt/router.js

###  <u>Adding SEO to a dynamic route</u> (03:19 - 04:19)
- copy/paste the script section from create.vue to _id.vue

### <u>Default page when dynamic route path doesn't contain id</u> (04:19 - 04:35)
- create a _index.vue for the dynamic route path

### <u>How to create root dynamic route</u> (04:35 - 05:06)
- create _username.vue at the root route

### <u>Nested dynamic routes</u> (05:06 - 05:38)
- create a folder with an leading underscore
- place in the index.vue without underscore when no parameter
- place in the following.vue for the dynamic route

### <u>Customize Error page</u> (05:38 - )
- when a route doesn't exist, nuxt shows a default error page
- in folder layouts, create new layout error.vue
- copy/paste the code of error.vue from the template finishing code
- script part: component takes in the error Object via prop. the computed properties 'statusCode' and 'message' take the error Object and return parts of its inside. The head() method takes the error message and puts it in the title
- tempalte part: svg to show an exclamation mark, div to print the error message, conditional p tag which only appears if the status code is 404 and shows in this case the link to the homepage
- SPA normally don't give back proper status codes, they always load up the index.html, nuxt does, it gives back 404 if the page doesn't exist through server side rendering (SSR)

# 9 API calls with Axios in Nuxt

## install necessary packages
- install json server __npm install -g json-server__
- download db.json from resources
- turn on the API server __json-server --watch db.json__
- if not already installed, install axios for nuxt: __npm install @nuxtjs/axios__, then in the nuxt.config.js add it as a module (03:00)
- check out doc for nuxtjs/axios: www.axios.nuxtjs.org

## implement API call
- the API call should be done from the default page index.vue. normally API calls get triggered via the created() lifecycle hook. nuxt has a few own lifecycle hook, here we use __asyncData()__
- in pages/index.vue, add the lifecycle hook asyncData(context). The context uses the axios getrequiest to call the db and when the response arrives, it should just return the object with the events. This object will be __automatically__ merged with the component data, so it can be read from within the template. no data has to be declared like in vue (05:52)
- the context can be simplified by using just $axios thanks to ES6 destructuring (06:00)

## display API data on the page
- in components folder, create EventCard.vue
- copy paste the code for the component from the resources
- in pages/index.vue, use the EventCard.vue component: add the EventCard in the template with a loop (07:36), import EventCard (07:41) and register it (07:45)

## adding error handling when data caanot be fetched
- per default, a nuxt error appears
- in pages/index.vue, add the error argument to asyncData() (08:25)
- catch the error by setting the statusCode and message and will redirect automatically to the previously created error page (08:44)

# 10 async/await and progress bar in Nuxt

## Replacing classic promises (.then) with async/await promises
 - problem with Promises: multiple nested promises create complexity
 - avoid nesting with async/await
 - in pages/index.vue, cut out error handling for now
 - in pages/index.vue, add async in front of the function and create a const which awaits the response of axios. Once the promise is resolved via await, get the db entries. once the response is saved in the const 'response', return the events objectwhich gets automatically merged into data() and is this available for the template
 - further simplification through ES6 destructuring: replace response with the data object. this way the return event is just the data object
 - add back the error handling: wrap the body of asyncData into a try block and add a catch block adding the error logic which was cut out before

 ## Adding API call when viewing a single event
 - copy the asyncData() method from pages/index.vue into pages/event/_id.vue
 - add a params property as we need access to the id
 - adapt the API call to use the params.id
 - adapt the events response to event
 - remove the id() computed property
 - in the head() method, the title and meta-content should display the event title instead of the id
 - adapt the template by printing out now the event.title instead of the id

 ## Adding a progress bar
 - add the progress bar color in the nuxt.config.js file. It is already working, it is just invisible. Now by changing the color we just make it visible
 - add a delay of 2secs in they json-server to see the progress bar: stop the json-server and restart with <br>
 __json-server --watch db.json --delay 2000__

 # 11 Using Vuex with Nuxt

 ## Reorganizing API calls

 ### create API calls
 - create folder 'services' in root and inside a new file EventService.js (01:17)
 - in services/EventService.js, import axios and add basic axios configuration, saving it in a const (01:25)
 - in services/EventService.js, create two getter methods, one calling all events, the other calling a specific event by id (01:44)

 ### use created API calls
 - in pages/index.vue, import the EventService (02:02)
 - in pages/index.vue, replace in asyncData() the axios call by the EventService.getEvents() (02:12) and remove the axios argument from asyncData
- in pages/_id.vue, import the EventService (02:24)
 -  in pages/_id.vue, replace in asyncData() the axios call by the EventService.getEvent() sending in the params id (02:35) and remove the axios argument from asyncData

 ## use Vuex on Event List Page
 - in the store folder, create a new module 'events.js'
 - in store/events.js, import EventService and create a state of 'events' initializing it with an empty array, wrapping it into an anonymous function to avoid to share that state all over the app (04:59)
- in store/events.js, create a mutation which sets the events in the state (05:07)
- in store/events.js, create an action which fetches the events via the EventService and commits the response to the mutation (05:25)
- in pages/index.vue, remove the EventService import (05:35) and import mapState instead (05:37)
- in pages/index.vue, replace the asyncData hook by the fetch hook (05:44)
- in pages/index.vue, send in as new first argument the store (05:49) and remove all the return values as fetch in contrary to asyncData doesn't return anything (05:55) and call from the events module the fetchEvents action (06:00)
- in pages/index.vue, add the computed property mapState to get the events state property from the events.js module (06:20)

## use Vuex on Event Show Page
- in store/events.js, create an empty event object (07:02)
- in store/events.js, create a SET_EVENT mutation (07:11)
- in store/events.js, create a fetchEvent action sending in the id of the event we want to fetch (07:31)
- in pages/_id.vue, replace EventService import with mapState (07:41)
- in pages/_id.vue, replace the asyncData hook by the fetch hook, sending in additionally the store (07:49)
- in pages/_id.vue, in fetch, remove the return values (07:56) and dispatch the fetchEvent action sending in the id parameter (08:03)
- in pages/_id.vue, add the computed property mapState to get the event state property from the events.js module (08:13)

### flesh out Event Show Page
- in pages/_id.vue, add the template code and CSS from the resources

# 12 Universal Mode Deployment

## 12.1 Creating an API Server(moving the local json-server) 

### Using remote db.json instead of the local one
- json from the following link: <br> 
https://github.com/Code-Pop/real-world-nuxt/blob/master/db.json

- remote json-server which gets served up with the remote db.json: <br>
http://my-json-server.typicode.com/Code-Pop/real-world-nuxt/

- link remote db.json instead local one: <br>
in services/EventService.js, update just the baseURL (02:50)

- start up development server to check: <br>
__npm run dev__

## 12.2 Ensure that production mode works locally
- build for production mode: <br>
__npm run build__ <br>
__ATTENTION__: after the build no changes can be made. if changes are made, afterwards a new build has to be done
- in .nuxt folder, we can now find a 'client' folder and a 'server' folder.
- run the app in production mode: <br>
__npm run start__

## 12.3 Deploying on server (Heroku)
__INFO__: Nuxt can be deployed on any server __that can run Node__
- server needs to be able to run the following commands: <br>
__npm install__ to install the dependecies <br>
__npm run build__ to build the app <br>
__npm run start__ to start the node server <br>

__INFO__: here we use __Heroku__ as it supports the node server and is for free

### Steps to deploy
- create the app on Heroku: <br>
__heroku create__ <br>
this will give the URL to access the application and the Git repo where the code has to be pushed
- config Heroku: enable heroku to __build__ the project: <br>
__heroku config:set NPM_CONFIG_PRODUCTION=false__
- config Heroku: set ip where Heroku can listen for requests: <br>
__heroku config:set HOST=0.0.0.0