# Grocery List App

This tutorial will guide you through building an editable grocery list app that lets you check off items from the list.

Take a look at the `finished.html` file to see what you're going to build. 

_Remember: you can reference the finished version at any time to compare the code if something isn't working the way you expect it to_

## Getting Started

Download [vue-grocery-list.zip](vue-grocery-list.zip)

Open the `start.html` file in Brackets and note the following script tag that links up the Vue library:

	<script src="js/vue.min.js"></script>

That script tag gives us access to the Vue library, so we are ready to start creating a dynamic page with Vue.

## Start Coding

Add the following to the body:

	<div id="app" class="container">
		<h2>{{ title }}</h2>
	</div>

There are two important parts here. The `id="app"` is what will define what markup Vue will interact with.

The `title` is a variable that we can update through code, note it’s inside of two curly braces—these double braces are referred to as an "expression".

Inside the last set of `<script>` tags you need to add the following code:

	new Vue({
		el: '#app',
			data: { 
				title: 'Your Page'
			}
	});

Here we define the `#app` as the section of HTML that Vue is going to take control of.
The `title` is a variable that is stored in the data of this app.

Save your page and test it out!

## Data Binding

You may remember that `title` is connected by data binding.

This example is one way data binding, but it can be two way; let’s explore that. 

Add the following code to the end of the `#app` div:

	<div class="footer">
		<hr/>
		<em>Change the title of your shopping list here</em>
		<input v-model="title" />
	</div>

Save your file and try it out by changing the text in the input field.

In Vue, `v-model` is a way to create two-way data binding in forms.


## Creating the List

Add the following to the HTML under the `<h2> ` heading:

	<ul>
		<li v-for="item in items">{{ item.text }}</li>
	</ul>

The `v-for` is the same as creating a For loop in vanilla Javascript. 

In this instance, we are going to have `v-for` loop through an array called "items" and list the text property from each object in the array.

But first, we need to add that data into our code!

Update the data in the Vue so it looks like this:

	data: {
    newItem: '',
    items: [
        { text: 'Bananas', checked: true }, 
        { text: 'Apples', checked: false}
    ],
    title: 'grocery list'
	}

There’s the list of "items" and the text that will be put into our shopping list.

Save and view in the browser.

Now add the following CSS:

	.removed {
	    text-decoration: line-through;
	    color: rgba(0,0,0,0.5);
	}
	
	ul li {
	    list-style-type: none;
	}

You might have noticed that our data has a true or false state for the "checked" item, let’s add that to our HTML.

Update the unordered list as follows:

	<ul>
		<li v-for="item in items" :class="{ 'removed': item.checked }">
			<label><input type="checkbox" v-model="item.checked"> {{ item.text }}</label>
		</li>
	</ul>

Save and try out the changes in the browser!

Let's break down what's going on here...

The `v-model="item.checked"` passes back to the item whether or not the checkbox is checked or not—remember: `v-model` allows two-way binding.

In our Data, Bananas is true and Apples is false. The checkboxes are updated to reflect that.

In the `:class="{ 'removed': item.checked }"`, the `:class` is short for `v-bind:class`, the one-way data binding we saw in the last tutorial.
 
The class "removed" is only added if this item is checked. 

## Updating the List

Add the following directly under the `<h2>`:

	<input v-model="newItem" @keyup.enter="addItem" placeholder="add item" type="text" >

This line of code is going to add a `newItem` to our list. We already have an empty variable called `newItem` in our Data (we added it along with our items array). 

When the user presses enter this input text will become a new item in our list.

`@keyup` is the same as an eventListener that listens for any key to be released.

`@keyup.enter` tells the listener to only listen for the "enter" key.

`@keyup.enter="addItem"` the "addItem" is the function we call when the enter key is released.

To add our `addIitem` function, we need to add it after our data in the Vue script—Make sure you add a comma , after the data closing bracket, then add this:

	methods: {
		addItem() {
		    var text;
		    text = this.newItem.trim();
		    if (text) {
		        this.items.push({text: text, checked: false});
		        this.newItem = '';
		    }
		}
	}

There's a lot going on here, so I've put what each line does in comments below:

	methods: {
		// addItem() is the function	
		addItem() {
				//we create a local variable called "text"
		    var text;
		    //we then fill the text var with our newItem
		    //trim removes any extra spaces at the end of the text
		    //"this" refers to our current Vue app
		    text = this.newItem.trim();
		    // the if statement evaluates whether there is anything inside the text var--if it is empty, nothing happens
		    if (text) {
				    //the text and a checked: false gets added to the end of the items array
		        this.items.push({text: text, checked: false});
		        //we then clear the input for another item
		        this.newItem = '';
		    }
		}
	}

Now you have a full-fledged list app ;)