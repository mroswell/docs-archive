# 📋 Chapter 5: Complete the cart with a checkout form

| **Project&nbsp;Goal** | Build a form to accept dummy checkout data                                                                                                                                   |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **What&nbsp;you’ll&nbsp;learn**       | How to create and validate forms inVue application                                                                                             |
| **Tools&nbsp;you’ll&nbsp;need**       | A modern browser like Chrome. If using Chrome, download Chrome DevTools for Vue.js. An account in CodeSandbox.io. If you get lost, import the starting point for this chapter [here](https://github.com/VueVixens/projects/tree/master/chapter-2-end). Instructions on how to do this are in [Appendix 1](appendix_1.md) |
| **Time needed to complete** | 1 hour                                                                                                                                                                                     |

# Instructions
1. Start [here](https://github.com/VueVixens/projects/tree/master/chapter-4-end)
2. Now we want to create a form to fill after you finish selecting dogs. First of all, we should create a new component to contain this form and a add a form route to our router settings. Go to the `views` page and create there a new file called `Form.vue`
3. Inside this file place a `<template></template>` tag and create a div inside it. Add text `Form works!` inside this div. Now our component should look like this:

	```
	<template>
	  <div>
		Form works!
	  </div>
	</template>
	```
4. Now let's create a route for this component. Go to the `main.js` and import `Form` component:

	```
	import Form from "./views/Form";
	```
5. Add one more option to the `routes` array:

	```
	{ path: "/form", component: Form }
	```
6. Let's check how our form works. Go to the `/form` route: you should see the text 'Form works' between our header and footer.
7. Let's add a class to our `div` and create a styling for it.

	```
	<div class="form-wrapper">
		Form works!
	</div>
	```
	Add a `<style scoped><style>` tag below the template. Inside this tag we will add some stylings for our form and the first one will be `form-wrapper` padding:
	
	```
	<style scoped>
		.form-wrapper {
		  padding: 40px;
		}
	</style>
	```
8. Now it's time to build our actual form. We will use Vuetify component called `v-form` for it (please check te [docs](https://vuetifyjs.com/en/components/forms)). As a first step we will add an empty `v-form` inside our `form-wrapper`

	```
	<template>
	  <div class="form-wrapper">
	    <v-form>
	      
	    </v-form>
	  </div>
	</template>
	```
	Of course, nothing is displayed right now, because we have to add dome form fields.
9. For the form inputs Vuetify uses the component called `v-text-field`. It has an attribute `label` where we can set a label for a certain field. Let's create three fields with labels "Name", "Email" and "Phone".

	```
	  <div class="form-wrapper">
	    <v-form>
	      <v-text-field label="Name"></v-text-field>
	      <v-text-field label="Email"></v-text-field>
	      <v-text-field label="Phone"></v-text-field>
	    </v-form>
	  </div>
	```
10. And of course we need to submit our form somehow. Let's add a submit button below the form fields

	```
	  <div class="form-wrapper">
	    <v-form>
	      <v-text-field label="Name"></v-text-field>
	      <v-text-field label="Email"></v-text-field>
	      <v-text-field label="Phone"></v-text-field>
	      <v-btn>Submit</v-btn>
	    </v-form>
	  </div>
	```
	Our button is aligned to the left side, so let's also add a `text-align: center` to `form-wrapper` styles
	
	```
	.form-wrapper {
	  padding: 40px;
	  text-align: center;
	}
	```
11. For now `Submit` button doesn't do anything but we will add a method, which will take all form fields values and print them in the console. To achieve this we have to create a property for each field in component's `data` and bind this properties to corresponding fields with `v-model` directive.
	>v-model directive creates two-way data bindings on form input and textarea elements. It automatically picks the correct way to update the element based on the input type.
	
	What does `two-way binding` mean? We can change binded data either from the input field or inside the component's `data` (and both binded data will be changed as a result).
	Let's add a `<script></script>` above the styles, add `export default` statement into it and create component's `data` (remember `data` should be a function returning an object:
	
	```
	<script>
	export default {
	  data() {
	    return {
	      
	    }
	  }
	}
	</script>
	```
12. Now let's add three new properties to the newly created object:

	```
	  data() {
	    return {
	      name: "",
	      email: "",
	      phone: ""
	    };
	  }
	```
	As you can see, all of them are empty strings.
13. Bind these properties to corresponding form inputs in the template:

	```
	    <v-form>
	      <v-text-field label="Name" v-model="name"></v-text-field>
	      <v-text-field label="Email" v-model="email"></v-text-field>
	      <v-text-field label="Phone" v-model="phone"></v-text-field>
	      <v-btn>Submit</v-btn>
	    </v-form>
	```
	Now try to change `name` property to your own name. Observe how the input has changed! When you're typing something in the input field, the corresponding data property will be changed too. That's how two-way data binding works.
14. Now we can simply print our form values to console on submission. Let's create a method for this (we will add `methods` right after `data`:

	```
	  methods: {
	    submit() {
	      console.log(
	        "Name:",
	        this.name,
	        "Email:",
	        this.email,
	        "Phone:",
	        this.phone
	      );
	    }
	  }
	``` 
	and bind it to `Submit` button click:
	
	```
	<v-btn @click="submit">Submit</v-btn>
	```
	Try to fill the form and click `Submit`. You can see the form data in your console.
	
	
# Final result
![](https://i.imgur.com/XtbvYRl.jpg)