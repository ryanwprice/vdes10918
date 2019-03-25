# Intro to Vue JS

## Getting Started

Download the [vue-js-intro.zip](vue-js-intro.zip)

Open the `vue-intro/start` folder in Brackets and note the following script tag in `index.html` to link up the Vue library:

	<script src="js/vue.min.js"></script>

That script tag gives us access to the Vue library, so we are ready to start creating a dynamic page with Vue.

Add the following to the body (typing—rather than copying & pasting—is a better way to practice & learn):

	<div id="app">
		<p>{{ message }}</p>
    </div>

There are two important parts here: The ID of `app` is what will define the Vue application in the code. In other words, anything inside that div can be manipulated/controlled by Vue.

The `message` is a variable that we can update through code. Note that it is inside of two curly braces! These double curly braces are referred to as an "expression".

Before the closing `body` tag add the following inside the second set of `script` tags at the bottom of the page:

	new Vue({
		el: '#app',
		data: {
			message: 'My First Vue Page'
		}
	});

This bit of code defines the `app` div as the section of code that Vue is going to take control of.

The `message` is a variable that is stored in the data of this app. 

Save your page and test it!

## Data Binding

What you have just done is known as data binding.

This is "one way" data binding, but it can be two way, so let’s explore that.

Add this into the `app` div:

	<input type="text" v-model="message" />

Save the page and test this in the browser.

Try typing into the input box to change the title.

This is just a simple demonstration of the power of Vue—without having to set up any complex event listeners, the page is updated on the fly!

## Using Vue to bind CSS

Add the following CSS to head section:

	<style>
		.red {
			background-color: red;
		}
	</style>

Now we will dynamically apply this via the input text box.

Update the `<p>` to match the code below:

	<p v-bind:class="message"> {{ message }}</p>	

This binds the message to also control the CSS class.

Save the page and type "red" into the input box.

This isn’t that useful but it will be the basis of things that we do later on in the term.

Before we go on, create a different css class and then try applying it via the input.

## Binding an Input Slider

Remember when we made that picture of Bill Murray change colours? Well, we're going to do it again, but this time we will code it with Vue!

Save the page and then choose `File > Save As`, naming it "slider.html"

Remove everything inside the `<div id="app">`, replace as follows:

	<input type="range" min="0" max="360" step="5" value="180" v-model="myValue" />
	<p>{{ myValue }}</p>

This creates an input slider that moves from 0 to 360 and moves in increments of 5. The starting value will be 180.

The `v-model` is used to create two-way data binding on form inputs.

The value of the slider is called `myValue` and will be displayed in the paragraph.

Change the vue code as shown:

	new Vue({
		el: '#app',
		data: {
			myValue: 180
		}
	});

Save the page and move the slider. It updates the text but wouldn’t it be good to use this number to control an image?

Add this to the body under the paragraph:

	<img src="http://fillmurray.com/300/400" v-bind:style="{ filter: 'hue-rotate(' + myValue + 'deg)' }">

This displays an image on the screen and connects the CSS with the `myValue` data element.
The filter: hue-rotate CSS is controlled by the `myValue` variable.

## Conclusion

Compare this to the code from the start of the term when we created the same slider with regular ol' _vanilla_ JS

Make sure you understand what data binding is, we will do it again next week