# Vue Image Gallery

## Getting Started

Download [vue-image-gallery.zip](vue-image-gallery.zip)

Open `index.html`, which has the CSS already created and the Vue.js library ready for use.

We are going to display a list of images on the page so we will loop through the list using `v-for`

Inside the last `script` tag add the following code to get Vue up and running on the `app` div:

	new Vue({
		el: '#app'
	});

# Displaying the List

Add the following to the `body` of your html page:

	<div id="app">
		<h1 class="text-center">Submitted images</h1>
		<hr/>
		<div id="container">
			<ul>
				<li v-for="(res, index) in myResult">
					<img class="listImg" v-bind:src="'img/' + res.Thumb" />
					<p>{{ res.Thumb }} - {{ res.Label }}</p>
				</li>
			</ul>
		</div>
	</div>

The image is placed in the `img` tag by binding the `src` attribute.

Vue then looks inside the img folder for the `res.Thumb` image

	<img class="listImg" v-bind:src="'img/' + res.Thumb">

Then we display the name of the image and it’s description below it:

	<p>{{ res.Thumb }} - {{ res.Label }}</p>

## Adding it to Vue

We need to add some code to Vue:

	new Vue({
		el: '#app',
		data: {
			bigImg: '',
			cssClass: 'hide',
			myResult: []
		},
		created: function() {
			this.lookUpData();
		},
	});

The `data` is holding variables that we will use later, but the `myResult` is going to be the list of images, but it’s empty! We’ll load them from an outside JSON file.

We added some new code in something called `created` — this means _as soon as Vue is running_, run the lookUpData function. 

`this` refers to this instance of Vue as there could be other versions of Vue running on the page.

## Methods

Let’s add the `lookUpData` function to Vue by creating our methods directly after the close of `created },`

	methods: {
		lookUpData() {
			var app = this;
			axios.get('records.json').then(function(response) {
		    app.myResult = response.data.records;
		  }).catch(function(error) {
			  alert("There was an error loading the records");
	    })
		}
	}

This code uses a small library called "axios" that loads outside data using something called `XHR`.

Basically, Axios 'gets' the son file and if it succeeds/responds, the data gets loaded into our records array inside the Vue data. If Axios fails, it will post an alert message.

To get Axios running, we need to add it to the `head` of our html:

	<script src="https://unpkg.com/axios@0.12.0/dist/axios.min.js"></script>

Now our code loads "records.json" and puts it in the variable called `myResult`

Save and try this and you should see your images appear!

Open up `records.json` and look at the data:

	{
		"ID":"11",
		"Thumb":"space-thumb.jpg",
		"Content":"space.jpg",
		"Label":"Outer Space"
	}

It looks like a javascript object—that's because it is! _Remember:_ JSON is JavaScript _Object_ Notation. Our JSON file is just a bunch of object data storing a filename (the Content), the thumbnail (Thumb), an image description (Label), and and ID number.

## Adding Interaction

What we need to do now is make a way for us to be able to click the thumbnail to load a larger image.

Add the following after `#container` div to display the larger image over top:

	<div id="panel" v-bind:class="cssClass">
		<div id="holder">
			<img class="listImg" v-bind:src="bigImg" />
		</div>
	</div>

We will make the panel appear by changing it’s class, at the moment the `cssClass` in our Vue data is set to "hide"

We bound that data to our `#panel` dive with `v-bind:class="cssClass"`

The bigger image is controlled by the `src` for our img tag with `v-bind:src="bigImg"`

Now we need a way to click the thumbnail and make this happen—we will do this by adding an event

## The Big Event

Find the thumbnail image tag and add `v-on:click="showImg(index)"` to the end of the img tag so that it matches the code below:

	<img class="listImg" v-bind:src="'img/' + res.Thumb" v-on:click="showImg(index)">

This is calling a special function in Vue known as a method. 

The function is called `showImg` and we pass in the current index number of our array. (Remember: arrays are zero-indexed, so our index will begin with 0) 

The index number will let Vue know which big image to add in to the `panel` div.

## Add ShowImg

In the Vue code add this function inside the methods, adding a comma to the end of lookUpData:

	showImg(index) {
    this.bigImg = 'img/' + this.myResult[index].Content;
    this.cssClass = 'show';
	}

We pass in the `index` of the image into the `showImg` function so that it can use that to get the big image. The `show` css class is added instead of `hide`. Save and test it.

## Closing the Image

It works great except there is no way to close the image on the screen.

Let’s fix that, add `v-on:click="removeImg"` to the end of the `#panel` div and again at end of the `.listImg` image tag

The code should look like this:

	<div id="panel" v-bind:class="cssClass" v-on:click="removeImg">
		<div id="holder">
			<img class="listImg" v-bind:src="bigImg" v-on:click="removeImg">
		</div>
	</div>

Since we don't know exactly where the user will click, this adds a click event to both the `panel` div and the image that will remove the big image. 

Let's create that `removeImg` function

## One More Function!

Go to your methods and add a comma after the `showImg` function, and then add this:

	removeImg() {
		this.cssClass = 'hide';
	}

When the user clicks the `panel` div or image the `cssClass` is set back to "hide" and removes it from the page. OK save and test. 