# Front APP

- Install vue router `npm i vue-router@4` (v.4 compatibile con Vue 3)
- Create a router.js file next a main.js `cd src && touch router.js`
- Inside router.js define the router contant and export it

```js
// 1 Import from vue-router createRouter and createWebHistory
import { createRouter, createWebHistory } from 'vue-router'

// 2 define routes
const router = createRouter({
  history: createWebHistory(),
  routes: [
    /* All routes here */
  ]
})

// 3. export the router
export { router }


```

## Define all routes inside the routes option

```js

routes: [
     {
      path: '/',
      name: 'home',
      component: HomeView
    },
    {
      path: '/about',
      name: 'about',
      component: AboutView
    },
  ]

```

NOTE: import the components for the component property

## Create and import the Router views
  
```bash
cd src
mkdir views
cd views
touch HomeView.vue
touch AboutView.vue
touch ContactsView.vue
touch BlogView.vue

```

Define a HomeView.vue file

```js
<script>

export default {
  name: 'HomeView',


}
</script>

<template>
  
  <div class="container">
    <h1>Home Page</h1>
    <p class="lead">
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Libero, adipisci optio, tempore maiores sit asperiores
      sed est nulla esse quos quam laudantium, voluptatibus minus officiis assumenda. Ex vitae eos earum.
    </p>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Alias iure, eius quo sint explicabo, ratione non eum
      cumque tempora laboriosam aliquam saepe quasi recusandae natus officia voluptate? Perspiciatis quasi laborum enim
      similique obcaecati harum aperiam delectus velit exercitationem! Nobis a natus ullam qui fuga fugit cumque quos
      amet possimus distinctio, pariatur eaque deleniti voluptate corporis illo tempore aspernatur temporibus nesciunt
      iure! Fugit numquam corrupti sit aliquam aspernatur laboriosam odit, vero at culpa laborum error impedit adipisci
      laudantium sint? Voluptatum eaque nostrum sapiente doloribus iste, rerum reiciendis animi, tempora molestias
      libero at nisi dolores quaerat sit officiis mollitia optio numquam. Suscipit autem expedita nesciunt in, dolorem
      nisi libero assumenda repellendus minus itaque! Tempore vitae animi commodi veritatis consectetur quas ad,
      deleniti iure porro quo enim cupiditate quam, laudantium vel illum doloribus, repellendus accusamus aut. Assumenda
      hic rem quidem qui suscipit dolor maxime ab odio voluptatem consectetur velit ipsa numquam, sunt eaque quae
      necessitatibus molestias dolores nobis quia maiores corporis repellat molestiae magnam. Vitae sequi ipsa quod
      similique. Architecto dolores maxime sunt beatae laboriosam. Aliquid ut aut aspernatur minima soluta consectetur
      ipsa magnam, debitis inventore! Neque, temporibus quia, ipsum eveniet tempora sint dolorem officia recusandae
      numquam facilis vel ipsam! Similique, assumenda quidem!</p>
  </div>
</template>


<style lang="scss" scoped>

</style>


```

Repeat for the other pages. Then update the router.js file and import all views components. Your route file should look like the following:

```js
import { createRouter, createWebHistory } from 'vue-router'
/* Import all components to pass to the routes */
import HomeView from './views/HomeView.vue'
import AboutView from './views/AboutView.vue'
import BlogView from './views/BlogView.vue'
import ContactsView from './views/ContactsView.vue'


const router = createRouter({
  history: createWebHistory(),
  routes: [
    {
      path: '/',
      name: 'home',
      component: HomeView
    },
    {
      path: '/about',
      name: 'about',
      component: AboutView
    },
    {
      path: '/blog',
      name: 'blog',
      component: BlogView
    },
    {
      path: '/contacts',
      name: 'contacts',
      component: ContactsView
    }
  ]
})


export { router }

```

Import the router instance in the main.js file and instruct Vue to use vue router

```js
import { createApp } from 'vue'
import App from './App.vue'
/* Import the router  */
import { router } from './router'
/* Tell Vue to use our router */
createApp(App).use(router).mount('#app')
```

## Updata main App.vue component

Use the router-view and rouer-link components

App.vue

```js
<script>
import AppNav from './components/AppNav.vue'

export default {
    components: {
        AppNav

    },


}
</script>

<template>

    <AppNav></AppNav>
    <router-view></router-view>
</template>

<style lang="scss">
@use './styles/general.scss';
</style>


```

Use router-link in your navigation. Edit the AppNav component (or whatever you called it)

```js
 <li class="nav-item">
    <router-link class="nav-link" :to="{ name: 'home' }" aria-current="page">Home <span
        class="visually-hidden">(current)</span></router-link>
  </li>

```

Note: replaced the anchor tag `a` with with the `router-link` component and use these syntax
`:to="{ name: 'home' }"` to point to a route.

## How to add single-posts

continue
