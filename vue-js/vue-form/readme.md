# Vue Form 

This is the same list app we made with vanilla JS a couple of weeks ago, but adapted to take advantage of Vue

You can see that pretty much everything is the same as it was when we started on this last time. The only difference is the script tag linking the Vue.js

First, lets wrap the form with `<div id="app>` so that Vue can control it.

Next lets start up Vue. 


	new Vue({
	    el: '#app'
	})

This bit of code goes in our `<script>` tag and tells Vue what it has control over (which in this case is the `<div id="app>`

Next we can take our objects of Homer, Bill, and Justin, and build them in Vue. We will also load them straight into an array called "people"

	new Vue({
		el: '#app',
		data: {
		    people: [
		        {name: "Homer Simpson", city: "Springfield"},
		        {name: "Justin Trudeau", city: "Ottawa"},
		        {name: "Bill Gates", city: "Redmond"}
		    ]
			}
	})

Now we can list the people out using a `v-for` loop

	<ul id="results">
    <li v-for="person in people">{{ person.name }}, {{ person.city }}</li>
	</ul>

Now we need to make the inputs work, so we need to add data binding to the inputs

	<label>Name</label><input v-model="name" type="text" name="name" />
	<label>City</label><input v-model="city" type="text" name="city" />

And we need to add a listener for our button

	<form id="form" v-on:submit.prevent="addName()">

The `prevent` stops the page from refreshing on submit, which is the default response from the browser

To pass down the data, we add `name` and `city` in our addName pipe addName(name, city)

We need to build our `addName` function, so we need to add a _method_ to Vue—**don't forget to add a comma** at the end of the Data

	methods: {
	addName(name, city) {
	        this.people.push({name: name, city: city});
	        this.name = "";
	        this.city = "";
	    };      
	}

This bit of code pushes the name and city to the end of our people array. Then it resets the value of each to be empty

We also need some error checking for both the fields, so we can wrap our code in some IF statements

	if(!name){
	    alert("Please enter a name");
	    return;
	} else {
	    if(!city) {
	        alert("Please enter a city");
	        return;
	    };
	    this.people.push({name: name, city: city});
	    this.name = "";
	    this.city = "";
	};      

Now our form should work, just the same as it did when we wrote it earlier in our plain ol' vanilla Javascript. Take a look at the older code in week 7 and compare the two solutions.