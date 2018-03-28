# 📋 Chapter 3: Connect your project to API

| **Project&nbsp;Goal** | Learn how API calls work                                                                                                                                   |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **What&nbsp;you’ll&nbsp;learn**       | Using the [DogCEO API](https://dog.ceo/dog-api/) you will load dog images dynamically                                                                                             |
| **Tools&nbsp;you’ll&nbsp;need**       | A modern browser like Chrome. If using Chrome, download Chrome DevTools for Vue.js. An account in CodeSandbox.io. If you get lost, import the starting point for this chapter [here](https://github.com/VueVixens/projects/tree/master/chapter-1-end). Instructions on how to do this are in [Appendix 1](appendix_1.md) |
| **Time needed to complete** | 1 hour                                                                                                                                                                                     |

# Instructions
1. Start [here](https://github.com/VueVixens/projects/tree/master/chapter-2-end)
2. To perform API calls we will need a library called [axios](https://github.com/axios/axios). It's a promise-based HTTP client that works both in the browser and in a node.js environment. We have to to add it to our project dependencies. To do so, please click on `File Editor` tab -> `Dependencies` -> `Add Dependency` and search for `axios`
3. Now let's import axios into the component where we will perform our API call - `Pets.vue`.
	```
	import axios from "axios";
	```
4. All our calls will use the same base URL with different endpoints. Let's add our base URL to axios' options:
	```
	axios.defaults.baseURL = "https://dog.ceo/api";
	```
	Now we are ready for our first API call.
5. Let's replace the first static image with the random husky picture from DogCEO API. First we have to check which endpoint should we use. Looking at the [documentation](https://dog.ceo/dog-api/) we can easily find out that we need `/breed/husky/images/random` (`api` part is already in our base URL). We want new image to replace old one right on the component creation, so let's add a `created()` hook right after `data`:
	```
	created() {}
	```
6. Inside the created hook we will add our first query. To perform GET-request `axios` uses `axios.get` method. The result will be a JavaScript promise, so we have to provide success and failure callbacks to it. Let's simply print query result to console:
	```
    axios
      .get("/breed/husky/images/random")
      .then(response => {
        console.log(response);
      })
      .catch(error => {
        console.log(error);
      });
   ```
7. Now you can see an object in your console. We are interested in its `data` field. You can see we have a status `success` and a message with image URL (you can copy/paste it to your browser and have a look at a cute husky).
8. Let's replace our husky image with this new one. First, we should find a husky in our dogs array with an `Array.find` method. It will check array items one by one to find a first item matching provided criteria. In our case the criteria is a `breed` equal to `husky`. Add this string inside `then` callback:
	```
	const husky = this.dogs.find(dog => dog.breed === 'husky');
	```
9. Ok, we have found a husky, now let's provide a new nice portrait for it.
	```
	husky.img = response.data.message;
	```
10. Let's try to load random image for each dog in our `dogs` array. First thing we need is a proper endpoint for each breed we have. We will create an array of links with `.map` method.

	?> Note: The `map()` method creates a new array with the results of calling a provided function on every element in the calling array.
	```
	const linksArray = this.dogs.map(
      dog => "/breed/" + dog.breed + "/images/random"
   );
   ```
   So for each dog in the array we're taking its breed and insert it inside the endpoint string (we used the same one for husky, but breed was a static value there)
11. Now we have to perform multiple API calls using all the links we've just created. `axios` has a helper functions for this case called `axios.all` and `axios.spread`. We should provide an array of our requests to the first one; it will return an array of responses and we should use `axios.spread` to spread this array into multiple arguments. To create an array of queries we will use a `.map` method on our `linksArray`, performing `axios.get` for each link:
	```
	axios.all(linksArray.map(link => axios.get(link)))
    .then(
      axios.spread((...res) => {
        this.dogs.forEach((dog, index) => {
          dog.img = res[index].data.message;
        });
      })
    );
    ```
    
    ?> Note: The forEach() method executes a provided function once for each array element.
    
	So, after we've got an array of images in response, we are iterating through our `dogs` array again, replacing each dog image with a corresponding new one (`index` is the index of the current element being processed in the array; it is the same for both arrays because response objects are placed in the same order they were sent).
12. Now we have new images each time our `Pets` component is created (on page refresh or simply navigation to `/pets` route from home). The only issue is we can still see old images for a short moment. Let's clear dogs images before we perform a query. Add this string as a first one inside `created()` hook:
	```
	this.dogs.forEach(dog => {
      dog.img = "";
    });
	```
13. Now we have empty dog portraits from the start and then images are loaded from API

# Final result
![](https://i.imgur.com/XtbvYRl.jpg)