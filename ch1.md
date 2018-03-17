# 📋 Vue Vixens Project 1: Introducing the My Pet Shop web site

| **Project Goal**            | Get started with Vue.js by creating a static Pet Shop web site                                                                                                                                   |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **What you’ll learn**       | Setting up your Vue app, CSS Grid, Styling in Vue, code structure in preparation for moving forward.                                                                                             |
| **Tools you’ll need**       | A modern browser like Chrome. If using Chrome, download Chrome DevTools for Vue.js. An account in CodeSandbox.io. |
| **Time needed to complete** | 1/2 hour                                                                                                                                                                                         |

# Instructions

Here, we will include step by step instructions.

1. Start [here](https://codesandbox.io/s/3x309k44op)
2. Familiarize yourself with the project, have a look at the HTML & CSS structure. Try to change classes in markup and watch how will change block colors on the webpage.
3. You might see the `orange-green` class in stylesheet. Let's add it to the `<main>` element and observe how all the colors & background are changed:
    ```
    <main class="orange-green">
    ```
4. Now let's try to change the class using Vue class bindings. Replace simple class in `<main>` with dynamic class binding: `:class="{'orange-green': false}"`. Try to change `false` to `true` and vice versa. You can see how class is applied in Chrome dev tools and how the page color theme is changing.
5. It's time to create your first Vue variable. First, you have to add `data()` to your Vue component. This dfunction  should return an object of our Vue variables. Let's create one:
    ```
    data() {
        return {
          themeSwitched: false
        };
      }
      ```
      So, now ve have a variable called `themeSwitched` and it's default value is `false`.
6. In our `<main>` replace `false` in class binding with our newly created variable. Now we have
   ```
    <main :class="{'orange-green': themeSwitched}">
    ```
7. Let's try to change `themeSwitched` value inside `data` from `false` to `true`. Again, you can see the color change effect.
8. Now we only need a switch to change a theme. First we will create a button (we're using Vuetify so ot will be a Vuetify button component). Let's place it in the `header` right after `h1` tag:
    ```
    <header class="app-header dark-brown">
        <h1>My Pet Store</h1>
        <v-btn>Switch theme</v-btn>
      </header>
      ```
9. Now let's add a click event handler to our button. We can use `v-on` directive or its shortcut `@`. This handler will change `themeSwitched` value to opposite, toggling the color-changing class.
    ```
    <v-btn @click="themeSwitched = !themeSwitched">Switch theme</v-btn>
    ```
10. Congratulations! You've just finished Chapter 1!


# Final result
![](https://i.imgur.com/E7He54K.png)