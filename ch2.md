# 📋 Chapter 2: Build a pet gallery

| **Project&nbsp;Goal** | Learn how to manipulate data in a web app                                                                                                                                   |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **What&nbsp;you’ll&nbsp;learn**       | Using static data, you'll build a card interface to show many adoptable dogs                                                                                             |
| **Tools&nbsp;you’ll&nbsp;need**       | A modern browser like Chrome. If using Chrome, download Chrome DevTools for Vue.js. An account in CodeSandbox.io. If you get lost, import the starting point for this chapter [here](https://github.com/VueVixens/projects/tree/master/chapter-1-end). Instructions on how to do this are in [Appendix 1](appendix_1.md) |
| **Time needed to complete** | 1 hour                                                                                                                                                                                     |

# Instructions
1. Start [here](https://github.com/VueVixens/projects/tree/master/chapter-1-end)
2. Now we have only a home page, but we want to add one more page for containing pet cards. Let's create a single-page application!

  > A single-page application (SPA) is a web application or web site that interacts with the user by dynamically rewriting the current page rather than loading entire new pages from a server (Wikipedia)

3. To create SPA with Vue we need vue-router. So let's first add it to dependencies (click `Add Dependency` button and search for `vue-router`)
4. Switch to `main.js` file and import vue-router:
    ```
    import VueRouter from "vue-router";
    ```
5. Now we need to use the plugin with `Vue.use()` global method:
    ```
    Vue.use(VueRouter);
    ```
6. In our application header and footer will be present on each page and the content between them will change. Component matched by the route will be rendered inside a `<router-view>` tag. Let's create a separate component for all the elements contained in `<div class="wrapper">`
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
16. Looks like nothing changed... but let's add `/pets` to the URL string in the address bae. Now you can see the Pets component instead of Home!
17. To make our navigation easier we will create a simple navigation bar using Vuetify. 
>Vuetify is a semantic component framework for Vue. It aims to provide clean, semantic and reusable components for building your application. You can find full documentation for it [here](https://vuetifyjs.com/en/getting-started/quick-start)
	
	The toolbar component in Vuetify is called `v-toolbar`. Let's add it right below the `h1` tag in our header
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
    Now the array `dogs` is a part of `Pets` component state and can be used in our template
21. Our `dogs` are an array. To render a list of items based on an array Vue has a `v-for` directive, it will iterate through this array and we can render each its item. Let's add this directive to our `v-flex` element:
    ```
     <v-flex xs12 sm4 md3 v-for="pet in dogs" :key="pet.breed">
     ```
     You need to provide a unique key attribute for each item. In our case, dog's breed will be the key.
     You can see now we have 8 `v-card`s with the same text and image.
22. So, inside the `v-for` directive our _current_ dog will be called a `pet` (we choose this name inside the directive; if we write `v-for="dog in dogs"` it will be called `dog`). Checking the `dogs.js` file we can see each dog has 3 properties: name, breed and img. Let's display image inside the `v-card-media` component. But if we simply replace `src` value with `pet.img`...
    ```
    <v-card-media src="pet.img" height="170px">
    ```
    We will have no pictures. Why? Because we're trying to pass static value, some file called `pet.img` and there is no such file. To bind attributes dynamically we need a `v-bind` directive or its shortcut `:`.
    ```
    <v-card-media :src="pet.img" height="170px">
    ```
    >`v-bind` directive dynamically bind one or more attributes, or a component prop to an expression
    Now it works!
23. Now we have to display dog's name. For text Vue uses _"mustache" syntax_ - double curly braces. The mustache tag will be replaced with the value of the binded property.
    ```
    <h3>{{pet.name}}</h3>
    ```
24. The only thing left is dog's breed. Let's add one more `<p></p>` tag right below the name and display breed there
    ```
    <p>{{pet.breed}}</p>
    ```
25. Everything works nice but our template now looks too big. Let's create a `Dog` component and pass current pet to it with a prop
	>Props are custom attributes you can register on a component. When a value is passed to a prop attribute, it becomes a _prop_erty on that component instance. In our case `Dog` component will have a `dog` property, passed from its parent `Pets` component
	
26. Let's create a new folder inside the `src` and name it `components`
27. Inside the components folder we will create a new file and name it `Dog.vue`. Open this file and add `<template></template>` and `<script></script>` tags. Now our file looks this way:
	```
	<template>
	
	</template>
	
	<script>
	
	<script>
	```
28. Copy the whole `v-card` component from `Pets.vue` and paste it inside the template tag.
29. As mentioned above, we will have a `dog` property in our `Dog` component. Let's add a `props` option to our component. First, we need to create an export statement inside our `script` tag (so later we will be able to import our `Dog` component inside the `Pets` one):
	```
	<script>
    export default {
  
    }
	<script>
	```
	Now we can add `props` option to this object and a prop `dog`:
	```
	<script>
	export default {
	  props: {
	    dog: {
	      type: Object
	    }
	  }
	};
	</script>
	```
	Here we are also specifying the type of our dog - it will be a JavaScript object.
30. In our template we should replace `pet` with `dog`, because we don't have any `pet`s inside the `Dog` component, only a passed `dog` property. Now our template should look the following way:
	```
	<template>
	  <v-card color="grey lighten-2">
	    <v-card-media :src="dog.img" height="170px">
	    </v-card-media>
	    <v-card-title>
	      <div>
	        <h3>{{dog.name}}</h3>
	        <p class="breed">{{dog.breed}}</p>
	      </div>
	    </v-card-title>
	  </v-card>
	</template>
	```
31. Now let's move back to our `Pets.vue` component and make some changes. First of all we should import here our newly created `Dog` component. Let's add this string after `Dogs` import statement:
	```
	import Dog from "../components/Dog.vue";
	```
32. Now we have to 'explain' the `Pets` component that it has a child component inside it. Vue uses a `components` option for this. Let's add a component option above the `data()` one:
	```
	export default {
	  components: {
	    appDog: Dog
	  },
	  data() {
	    return {
	      dogs: Dogs
	    };
	  }
	};
	```
	>For each property in the components object, the key will be the name of the custom element, while the value will contain the options object for the component
	
	For component name you can either use a camel-case (`appDog`) or kebab-case (`'app-dog'`). Keep in mind that camel-case one will be 'translated' to kebab-case in HTML tag names. So we will use the HTML custom tag `<app-dog>` and it will render a `Dog` component
33. In `Pets.vue` remove the `v-card` component and all its content and place our custom tag there:
	```
	<v-flex xs12 sm4 md3 v-for="pet in dogs" :key="pet.breed">
      <app-dog></app-dog>
    </v-flex>
	```
34. Now we have to pass a `dog` prop to our `Dog` component. It will be done with the already known `v-bind` directive (to be more precise, with it `:` shortcut:
	```
    <v-flex xs12 sm4 md3 v-for="pet in dogs" :key="pet.breed">
      <app-dog :dog="pet"></app-dog>
    </v-flex>
	```
	
Chapter 2 completed!

# Final result
![](https://i.imgur.com/c1GkkcW.png)