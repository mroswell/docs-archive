# 📋 Chapter 4: Create a dog shopping cart

| **Project&nbsp;Goal** | Create a shopping cart for the shop so that you can add and remove a dog from your cart                                                                                                                                   |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **What&nbsp;you’ll&nbsp;learn**       | State management in Vue application with Vuex                                                                                             |
| **Tools&nbsp;you’ll&nbsp;need**       | A modern browser like Chrome. If using Chrome, download Chrome DevTools for Vue.js. An account in CodeSandbox.io. If you get lost, import the starting point for this chapter [here](https://github.com/VueVixens/projects/tree/master/chapter-3-end). Instructions on how to do this are in [Appendix 1](appendix_1.md) |
| **Time needed to complete** | 1.5 hour                                                                                                                                                                                     |

# Instructions
1. Start [here](https://github.com/VueVixens/projects/tree/master/chapter-3-end)
2. We need a shopping cart component to show the list of selected dogs. Let's create a new file in the `views` folder and name it `Cart.vue`
3. First thing we need in new component is a template. Inside this new file add a `<template></template>` tags.
4. Inside `template` tags create a `<div></div>` tag and add there a simple text 'Cart works!'.
	
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
6. Let's add a link to our cart inside the navbar. Later we will also show the selected items amount on it, but for now it will be just a plain icon with link. Go to the `App.vue` file and add the following code inside `v-toolbar` right after the closing tag of `v-toolbar-items`:
	
	```
	<v-spacer></v-spacer>
    <router-link to="/cart">
	   <v-icon large>shopping_cart</v-icon>
	</router-link>
	```
	
	>`v-spacer` is a Vuetify component to fill the whole free space between other components. `v-icon` is a component displaying [Material icons](https://material.io/icons/)

	Now when you're clicking on the cart icon you will be navigated to `/cart` route.

7. Let's create a markup for `Cart` component. We will use Vuetify list component to display our dogs. Let's remove our placeholder text from the `<div></div>` tag and replace it with `<v-list></v-list` tag. At this moment our template looks like this:
	
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
10. Great! Now it's time to display some real data inside the cart, but now we have a problem: how can we save selected dogs and pass them from the `Pets` component to the `Cart` one? We cannot use props, because this two components don't have any 'parent-child' relationship... In such cases we need a _state management_ library and Vue does have one: it's called `Vuex`
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
	          <v-icon>delete</v-icon>
	        </v-list-tile-action>
	      </v-list-tile>
	    </div>
	  </v-list>
	</div>
	```
	>`v-if` directive conditionally render the element based on the truthy-ness of the expression value. `v-else` directive serves as an 'else' block for `v-if`
	
	What is happening here? First the application will check if the `cart` array has a _length_ (i.e. if there are some items inside this array; empty array has a length equal to 0). If the length is 0, the application will render only the `Your cart is empty` text and will ignore the `v-else` block. If array is not empty, application will jump to `v-else` block and render it.
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
22. We need to find a way to add dogs to cart and remove them from it. In other words, we have to _change our state_. The only way to actually change state in a Vuex store is by committing a _mutation_. Vuex mutations are very similar to events: each mutation has a string **type** and a **handler**. The handler function is where we perform actual state modifications and it will receive the state as the first argument. Let's create our first mutation. Inside the `store.js` clear the state `cart` array and after the `state` property add `mutations`:

	```
	export const store = new Vuex.Store({
	  state: {
	    cart: []
	  },
	  mutations: {
	  },
	});
	```
	Inside this object create `addToCart` mutation:
	
	```
	export const store = new Vuex.Store({
	  state: {
	    cart: []
	  },
	  mutations: {
	    addToCart(state, payload) {
	      state.cart.push(payload);
	    },
	  },
	});
	```
	The mutation has two parameters: first is the state as said above; the second is the data which we will add to our `state.cart`. `addToCart` mutation will add the payload item to the `state.cart` array.
	>You cannot directly call a mutation handler. To invoke it, you need to call store.commit with its type: `store.commit('addToCart')
	Usually in Vuex mutations are committed with _actions_. Actions are similar to mutations but they can contain asyncronous operations (like API calls).
23. Let's register an action to commit our `addToCart` mutation. Add the `actions` property to the store object and `addToCart` action to this property:

	```
	export const store = new Vuex.Store({
	  state: {
	    cart: []
	  },
	  mutations: {
	    addToCart(state, payload) {
	      state.cart.push(payload);
	    },
	  },
	  actions: {
	    addToCart({ commit }, payload) {
	      commit("addToCart", payload);
	    },
	  }
	});
	```
	>Action handlers receive a context object which exposes the same set of methods/properties on the store instance, so you can call `context.commit` to commit a mutation. We are using ES6 [argument destructuring](https://github.com/lukehoban/es6features#destructuring) to have only `commit` method of `context`
	
	`payload` here is the same data we want to pass from the component to the mutation to change the state.
24. Let's call our action from inside the `Pets.vue` component. First we need some kind of a button to add a certain dog to cart. Move to the `Dog.vue` component and add the button right below the `v-card-title` closing tag:

	```
	<v-btn @click="$emit('addToCart', dog)">Add to Cart</v-btn>
	```
	With the `$emit` we are sending the message to our parent component (in this case it's `Pets.vue`) like 'Hi, something is happened here! Please read this message and react to it'. Our message also contains a second parameter: it's the `dog` which we're trying to add to our cart.
25. Now let's open a `Pets.vue` and add a _listener_ to our emitted event:

	```
	<app-dog :dog="pet" @addToCart=""></app-dog>
	```
	Fow now this listener is doing nothing but we want to call an action on this event. To do so we have to map the actions to our component.
	>You can dispatch actions in components with `this.$store.dispatch('xxx')`, or use the `mapActions` helper which maps component methods to store.dispatch calls
		
	We will use the second solution. First import the `mapActions` helper:
		
	```
	import { mapActions } from "vuex";
	```
	and then add it to the component `methods` using [ES6 spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
	
	```
    methods: {
      ...mapActions(["addToCart"])
    },
	```
	Now we can dispatch `addToCart` like a simple component method.
26. Let's call this method on `app-dog` `addToCart` event:

	```
	<app-dog :dog="pet" @addToCart="addToCart"></app-dog>
	```
	Try to click on `Add to Cart` buttons. You can see how the icon badge number increases and you can open the shopping cart by click on this icon and check how many dogs we have there.
27. For now we can add any dog multiple times but we don't have five Maxs! Let's check our payload inside the mutation and add the dog only if it's not in the cart already:

	```
	addToCart(state, payload) {
      if (state.cart.indexOf(payload) <= -1) {
        state.cart.push(payload);
      }
    },
	```
	Here we're checking the index of `payload` inside the `state.cart` array. If index is lower or equal to -1 (in other words if the array does not contain such an element), we will add this item to the cart.
28. Now we need a mechanism to remove dogs from the cart. Let's create an action and a mutation for this. In the `store.js` add the `removeFromCart` mutation to `mutations` object:

	```
	removeFromCart(state, payload) {
      state.cart.splice(state.cart.indexOf(payload), 1);
   }
	```
	>Here the splice() method changes the contents of an array by removing existing elements. First argument is the index of element we want to start with and the second argument is the number of elements we want to remove
	
	So first we're finding the index of `payload` item inside the `state.cart` array and remove the one item starting from this index (i e we will remove only the `payload` item itself)
29. Add the action to commit the `removeFomCart` mutation:

	```
	removeFromCart({ commit }, payload) {
      commit("removeFromCart", payload);
   }
	```
30. Now we need to dispatch this action on delete icon clicks. Go to the `Cart.vue` file. As you remember, first we should map actions to component methods. Import `mapActions` helper:

	```
	import { mapActions } from "vuex";
	```
	and add it to the component `methods`
	
	```
	methods: {
    ...mapActions(["removeFromCart"])
  	}
	```
	And finally add the click listener to delete icon:
	
	```
	<v-icon @click="removeFromCart(dog)">delete</v-icon>
	```
	Now you can add and remove dogs from your shopping cart.
	
Chapter 4 complete!

# Final result
![](https://i.imgur.com/Co0iGJT.jpg)