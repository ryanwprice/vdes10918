# Vue Dynamic CSS

## Getting Started

Download [vue-dynamic-css.zip](vue-dynamic-css.zip)

Open the `index.html` file in Brackets and note the following script tag that links up the Vue library:

	<script src="js/vue.min.js"></script>

That script tag gives us access to the Vue library, so we are ready to start creating a dynamic page with Vue.

Take a moment and familiarize yourself with the Vue code already in the file

	new Vue ({
    el: '#app',
    data: {
        bands: [
            { name: 'Wintersleep', genre: 'Indie' },
            { name: 'Justin Bieber', genre: 'Pop' }, 
            { name: 'Dan Mangan', genre: 'Indie' },
            { name: 'Bruno Mars', genre: 'Pop' },
            { name: 'Madonna', genre: 'Pop' },
            { name: 'Stars', genre: 'Indie' }
        ]
		}
	})

There is an array called bands with six objects indexed within in. Each object has a "name" and "genre" property associated to it.

## Start Coding

Add the following to the body, right after the `<h1>`:

	<ul>
    <li v-for="band in bands">{{ band.name }}</li>
	</ul>

This will loop through our `bands` array and list the `name` of each artist as a `<li>`

Go ahead, give it a try!

## Filtering the Genre

Let’s create a way to select different genre’s by adding this between the `<h1>` and `<ul>`

	<p>What kind of music do you want to see?</p>
	<label for="Indie"><input type="radio" id="Indie" value="Indie" v-model="picked">Indie</label> | <label for="Pop">Pop<input type="radio" id="Pop" value="Pop" v-model="picked"></label>
        
	<p>Currently Highlighting: <span>{{ picked }}</span></p>

This will place the value of "Indie" or "Pop" in the variable picked.

It won’t work just yet; we need to add the `picked` variable to our data in the Vue code:

	data: {
		picked: '',
		bands: [{
		etc…

Save your code and try it now and it will display what you’ve picked from those radio buttons.

## Adding Some Colour

Highlighting each selected list item is tricky, but before we solve that let’s add a new CSS class to show the selected items:

.highlight {       background: #ceff00;         }

We need to add the `.highlight` class whenever the selected genre matches the genre associated with the band. We can do this by adding `v-bind:class="{ highlight: isSelected(band.genre) }"` to our `<li>` like so:

	<li v-for="band in bands" :class="{ highlight: isSelected(band.genre) }">{{ band.name }}</li>

This new bit of code is calling a special function in Vue known as a method. The function is called `isSelected` and we pass in the current genre (via the brackets).
 
The function will check if the radio button is the same as the band's genre and if so will return true when there is a match, and false when there isn't. 

By returning true it adds the highlight CSS class.

## Add the Method

In the Vue code add a comma after the `data` closing bracket },
Now add this method directly after:

	methods: {
		isSelected(genre) {
	        if (genre == this.picked) {
	            return true;
	        } else {
	            return false;
	        }
	    }
	}

Save the page and test this out.

