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

# Final result
![](https://i.imgur.com/XtbvYRl.jpg)