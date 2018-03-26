# 📋 Chapter 2: Build a pet gallery

| **Project&nbsp;Goal** | Learn how to manipulate data in a web app                                                                                                                                   |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **What&nbsp;you’ll&nbsp;learn**       | Using static data, you'll build a card interface to show many adoptable dogs                                                                                             |
| **Tools&nbsp;you’ll&nbsp;need**       | A modern browser like Chrome. If using Chrome, download Chrome DevTools for Vue.js. An account in CodeSandbox.io. If you get lost, import the starting point for this chapter [here](https://github.com/VueVixens/projects/tree/master/chapter-1-end). Instructions on how to do this are in [Appendix 1](appendix_1.md) |
| **Time needed to complete** | 1 hour                                                                                                                                                                                     |

# Instructions
1. Start [here](https://github.com/VueVixens/projects/tree/master/chapter-1-end)
2. Now we have only a home page, but we want to add one more page for containing pet cards. Let's create a single-page application!
    > A single-page application (SPA) is a web application or web site that interacts with the user by dynamically rewriting the current page rather than loading entire new pages from a server
    > (Wikipedia)
3. To create SPA with Vue we need vue-router. So let's first add it to dependencies (click `Add Dependency` button and search for `vue-router`)
4. Switch to `main.js` file and import vue-router:
    ```
    import VueRouter from "vue-router";
    ```
5. Now we need to use the plugin with `Vue.use()` global method:
    ```
    Vue.use(VueRouter);
    ```
6. In our application header and footer will be present on each page and the content between them will change. Component matched by the route will be rendered in a `<router-view>` tag. Let's create a separate component for all the elements contained in `<div class="wrapper">`
7. Go to the `views` folder and create there a file with the name `Home.vue`
8. Add `<template></template>` tag to this new file
9. Go to the `App.vue` file. Copy the `<div class="wrapper">` and all elements inside it and paste it inside template in `Home.vue`
10. Great, now we have a separate component for our content part for the home page! You might have seen also a `Pets.vue` inside the `views` folder - it's a starter template for out pets page. Now let's create routes for them.
11. Let's go back to `main.js`. First, let's import our new components:
    ```
    import Home from "./views/Home";
    import Pets from "./views/Pets";
    ```
12. Now we can create routes. Each route is an object specifying path and a component which will be rendered in this path. Let's add two routes, one is for our homepage and one for pets:
    ```
    const routes = [
      { path: "/", component: Home },
      { path: "/pets", component: Pets }
    ];
    ```
13. Now we have to create a `VueRouter` instance and pass our routes object to it:
    ```
    const router = new VueRouter({ routes });
    ```
14. And, finally, we need to add router to our Vue instance. To do this, just add a `router` right after `template: "<App/>",` string:
    ```
    new Vue({
      el: "#app",
      components: { App },
      template: "<App/>",
      router
    });
    ```
15. Now we can switch back to our App.vue. Replace the whole `<div class="wrapper">` with a `<router-view></router-view>` tag.
16. Looks like nothing changed... but let's add `/pets` to the URL. Now you can see the Pets component instead of Home!
17. To make our navigation easier we will create a simple navigation bar using Vuetify. Let's add this code right below the `h1` tag in our header
    ```
    <v-toolbar>
        <v-toolbar-items>
            <v-btn to="/" flat>Home</v-btn>
            <v-btn to="/pets" flat>Pets</v-btn>
        </v-toolbar-items>
    </v-toolbar>
    ```
    You can see here two buttons. Each of them has `to` attribute: it's a router-link to certain route. Now we can easily switch between pages.
18. Ok, fine, but there are no pets... Let's add some! Go to the `data` folder and find a file called `dogs.js`. It exports one const `Dogs` containing all the dogs data we need.
19. Let's import this data into our pets component. Go to the `Pets.vue`, create a `<script></script>` tag and add import statement into it:
    ```
    <script>
        import { Dogs } from "../data/dogs";
    </script>
    ```
20. Now we have to add this data to our component data property.
    ```
    <script>
    import { Dogs } from "../data/dogs";
    export default {
      data() {
        return {
          dogs: Dogs
        };
      }
    };
    </script>
    ```
21. Our `dogs` are an array. To render a list of items based on an array Vue has a `v-for` directive, it will iterate through this array and we can render each its item. Let's add this directive to our `v-flex` element:
    ```
     <v-flex xs12 sm4 md3 v-for="dog in dogs" :key="dog.name">
     ```
     You need to provide a unique key attribute for each item. In our case, name will be the key.
     You can see now we have 8 cards with the same text and image
22. So, inside the `v-for` directive our _current_ dog will be called... well, a `dog` (we choose this name inside the directive; if we write `v-for="pet in dogs"` it will be called `pet`). Checking the `dogs.js` file we can see each dog has 3 properties: name, breed and img. Let's display image inside the `v-card-media` component. But if we simply replace `src` value with `dog.img`...
    ```
    <v-card-media src="dog.img" height="170px">
    ```
    We will have no pictures. Why? Because we're trying to pass static value, some file called `dog.img` and there is no such file. To bind attributes dynamically we need a `v-bind` directive or its shortcut `:`.
    ```
    <v-card-media :src="dog.img" height="170px">
    ```
    Now it works!
23. Now we have to display dog's name. For text Vue uses _"mustache" syntax_ - double curly braces. The mustache tag will be replaced with the value of the binded property.
    ```
    <h3>{{dog.name}}</h3>
    ```
24. The only thing left is dog's breed. Let's add one more `<p></p>` tag right below the name and display breed there
    ```
    <p>{{dog.breed}}</p>
    ```
    Chapter 2 completed!

# Final result
![](https://i.imgur.com/c1GkkcW.png)