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
4. Inside `template` tags create a `<div></div>` tag and att there a simple text 'Cart works!'.
	
	```
	<template>
	  <div>
	    Cart works!
	  </div>
	</template>
	```
Now let's connect our newly created component with the router and check if it's displaying correctly on corresponding route.
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
    <router-link to="/cart">
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
10. Great! Now it's time to display some real data inside the cart, but now we have a problem: how can we save selected dogs and pass them from the `Pets` component to the `Cart` one? We cannot use props, because this two component don't have any 'parent-child' relationship... In such cases we need a _state management_ library and Vue does have one: it's called `Vuex`
	>Vuex is a state management pattern + library for Vue.js applications. It serves as a centralized store for all the components in an application, with rules ensuring that the state can only be mutated in a predictable fashion.
11. To start working with this centralized store we have to add Vuex to our application. First, open the `Dependencies` dropdown, click on `Add dependency` button and seach for `vuex`
12. Now let's create a `store` folder and a `store.js` file inside of it. Here we will save the whole application data.
13. Open the `store.js` and add imports and install Vuex:
	
	```
	import Vue from "vue";
	import Vuex from "vuex";
	
	Vue.use(Vuex);
	```
14. Now let's create and export the actual store:

	```
	export default Vuex.Store({
	  
	})
	```
15. What actually do we want to save on out application state? It's a cart, which will contain selected dogs. Let's add a `cart` array to out initial `state` object:

	```
	export default Vuex.Store({
	  state: {
	  	cart: [],
	  }
	})
	```
16. We have to add this store to our Vue instance. To do this, move to the `main.js` file and add the import

	```
	import store from "./store/store";
	```
	Then add the `store` to the Vue instance properties:
	
	```
	new Vue({
	  el: "#app",
	  components: { App },
	  template: "<App/>",
	  router,
	  store
	});
	```
	Now all the components will have an access to our state via `this.$store.state` placed inside component's computed property. Let's try to access it from the `Cart` component.
	
	>Computed properties can be used to do quick calculations of properties that are displayed in the view. These calculations will be cached and will only update when their dependencies are changed. 
	
17. Inside `Cart.vue` add the script tag with the export default statement:
	
	```
	<script>
		export default {
		  
		};
	</script>
	```
	and add the `computed` property to the component:
	
	```
	<script>
		export default {
		  computed: {
		    cart() {
     		  return this.$store.state.cart;
    		}
		  }
		};
	</script>
	```
	
	You can see the `cart()` is a function which will return the value of our state `cart` array so we can use it in our component. Let's replace out mock data with the cart content.
18. First let's temporarily add some content to the `state.cart`. Copy first three dogs from the `data/dogs.js` file and paste them to the `cart`:
	
	```
	state: {
		cart: [
		  {
		    name: "Max",
		    breed: "husky",
		    img: "https://dog.ceo/api/img/husky/n02110185_1469.jpg"
		  },
		  {
		    name: "Rusty",
		    breed: "shiba",
		    img: "https://dog.ceo/api/img/shiba/shiba-13.jpg"
		  },
		  {
		    name: "Rocco",
		    breed: "boxer",
		    img: "https://dog.ceo/api/img/boxer/n02108089_14112.jpg"
		  },
		]
	},
	```
19. Inside the `Cart.vue` component we will iterate through the `cart` array with already known `v-for` directive. Let's change the template accordingly, using `dog.name` as a key:

	```
	<div>
	  <v-list>
	      <v-subheader>Your cart</v-subheader>
	      <v-list-tile avatar v-for="dog in cart" :key="dog.name" @click="{}">
	        <v-list-tile-avatar>
	          <img :src="dog.img">
	        </v-list-tile-avatar>
	        <v-list-tile-content>{{dog.name}}</v-list-tile-content>
	        <v-list-tile-action>
	          <v-icon>delete</v-icon>
	        </v-list-tile-action>
	      </v-list-tile>
	  </v-list>
	</div>
	```
	Don't forget to change `src` attribute to `:src`, because now we are using dynamic property for it.
20. Now we can see our mock data displaying on the `/cart` route! Let's add some more UI tweaks to them. First, we need some placeholder text to show when our cart is empty. We will wrap the whole list content in the wrapper div and show it only when we have items in our cart; otherwise user will see placeholder text. Let's change the template:

	```
	<div>
	  <v-list>
	    <v-subheader v-if="!cart.length">Your cart is empty</v-subheader>
	    <div v-else>
	      <v-subheader>Your cart</v-subheader>
	      <v-list-tile avatar v-for="dog in cart" :key="dog.name" @click="{}">
	        <v-list-tile-avatar>
	          <img :src="dog.img">
	        </v-list-tile-avatar>
	        <v-list-tile-content>{{dog.name}}</v-list-tile-content>
	        <v-list-tile-action>
	          <v-icon @click="removeFromCart(dog)">delete</v-icon>
	        </v-list-tile-action>
	      </v-list-tile>
	    </div>
	  </v-list>
	</div>
	```
	>`v-if` directive conditionally render the element based on the truthy-ness of the expression value. `v-else` directive serves as an 'else' block for `v-if`
	
	What is happening here? First the application will check if the `cart` array has a _length_ (i.e. if there are some items inside this array; empty array has a length equal to 0). It length is 0, the application will render only the `Your cart is empty` text and will ignore the `v-else` block. If array is not empty, application will jump to `v-else` block and render it.
21. Let's also display the amount of selected items above the cart icon in toolbar. Move to the `App.vue` and add a computed property for `cart` (similar to the `Cart` component one):

	```
	computed: {
		cart() {
		  return this.$store.state.cart;
		}
	}
	```
	Now let's wrap out cart icon with the Vuetify `v-badge` component and show the amount of cart items inside of it:
	
	```
	<router-link to="/cart">
	    <v-badge color="grey lighten-1" overlap right v-model="cart.length">
	      <span slot="badge">{{cart.length}}</span>
	      <v-icon large>shopping_cart</v-icon>
	    </v-badge>
	</router-link>
	```
	`v-model` directive here will define the visibility of the badge. So, if the cart is empty, the badge will be hidden. With our mock data we can see the number `3` inside the badge.
22. We need to find a way to add dogs to cart and remove them from it. In other words, we have to _change our state_.


# Final result
![]()