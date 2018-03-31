# 📋 Chapter 4: Create a dog shopping cart

| **Project&nbsp;Goal** | Create a shopping cart for the shop so that you can add and remove a dog from your cart                                                                                                                                   |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **What&nbsp;you’ll&nbsp;learn**       | State management in Vue application with Vuex                                                                                             |
| **Tools&nbsp;you’ll&nbsp;need**       | A modern browser like Chrome. If using Chrome, download Chrome DevTools for Vue.js. An account in CodeSandbox.io. If you get lost, import the starting point for this chapter [here](https://github.com/VueVixens/projects/tree/master/chapter-3-end). Instructions on how to do this are in [Appendix 1](appendix_1.md) |
| **Time needed to complete** | 1 hour                                                                                                                                                                                     |

# Instructions
1. Start [here](https://github.com/VueVixens/projects/tree/master/chapter-3-end)
2. We need a shopping cart component to show the list of selected dogs. Let's create a new file in the `views` folder and name it `Cart.vue`
3. First thing we need in new component is a template. Inside this new file add a `<template></template>` tags.
4. Inside `template` tags create a `<div></div>` tag and att there a simple text 'Cart works!'. Now let's connect our newly created component with the router and check if it's displaying correctly on corresponding route.
5. Go to the `main.js` file. On the top, after importing `Home` and `Pets` components, add one more import statement:
	```
	import Cart from "./views/Cart";
	```
	After that, add one more route to the `routes`:
	```
	{ path: "/cart", component: Cart }
	```
	In the browser address bar try to navigate to `/cart` (simply add `/cart` to the URL of the homepage). You should see the text 'Cart works!` between the header and the footer.
6. Let's add a link to our cart inside our navbar. It will be a shopping cart icon, later we will also show the selected items amount on it. But for now it will be just a plain icon with link. Go to the `App.vue` file and add the following code inside `v-toolbar` right after the closing tag of `v-toolbar-items`:
	```
	<v-spacer></v-spacer>
    <router-link class="cart" to="/cart">
	   <v-icon large>shopping_cart</v-icon>
	</router-link>
	```
	
	>`v-spacer` is a Vuetify component to fill the whole free space between other components. `v-icon` is a component displaying [Material icons](https://material.io/icons/)

	Now when you're clicking on the cart icon you will be navigated to `/cart` route.

7. Let's create a markup for `Cart` component. We will use Vuetify list component to display our dogs. Let's remove our placeholder text from the `<div></div>` tag replace it with `<v-list></v-list` tag. At this moment our template looks like this:
	```
	<div>
		<v-list>
		</v-list>
	</div>
	```
8. We need a name of our list. Vuetify is using a `v-subheader` component for this purpose, let's add one:
	```
	<div>
	  <v-list>
	    <v-subheader>Your cart</v-subheader>
	  </v-list>
	</div>
	```
9. Now let's add a list element with mock data: dog image, name and delete icon. We will need `v-list-tile` component for list item; `v-list-tile-avatar` for dog image; `v-list-tile-content` for name and `v-list-tile-action` plus `v-icon` for delete button. You can check [Vuetify list component docs](https://vuetifyjs.com/en/components/lists) for more details. Now our template is:
	```
	<div>
	  <v-list>
	      <v-subheader>Your cart</v-subheader>
	      <v-list-tile avatar @click="{}">
	        <v-list-tile-avatar>
	          <img src="https://dog.ceo/api/img/husky/n02110185_1469.jpg">
	        </v-list-tile-avatar>
	        <v-list-tile-content>Test</v-list-tile-content>
	        <v-list-tile-action>
	          <v-icon>delete</v-icon>
	        </v-list-tile-action>
	      </v-list-tile>
	  </v-list>
	</div>
	```


# Final result
![]()