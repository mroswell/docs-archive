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
4. We will use Vuetify list component to display our dogs. Let's add a `<div></div>` tag inside a template and then inside this `div` we will place our `<v-list></v-list`. At this moment our template looks like this:
	```
	<div>
		<v-list>
		</v-list>
	</div>
	```
5. We need a name of our list. Vuetify is using a `v-subheader` component for this purpose, let's add one:
	```
	<div>
	  <v-list>
	    <v-subheader>Your cart</v-subheader>
	  </v-list>
	</div>
	```
6. Now let's add a list element with mock data: dog image, name and delete icon. We will need `v-list-tile` component for list item; `v-list-tile-avatar` for dog image; `v-list-tile-content` for name and `v-list-tile-action` plus `v-icon` for delete button. You can check [Vuetify list component docs](https://vuetifyjs.com/en/components/lists) for more details. Now our template is:
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