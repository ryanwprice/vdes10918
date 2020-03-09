# Find-A-Designer

## Instructions

The code has 10 famous designers saved to an array for review. 

Use the input box to allow users to search for a designer by first _or_ last name. 

If the designer is found, display their _full_ name for the user. If the designer is not found, display an error message.

## Bonus

Capitalize the first and last name of the designer when you display it.

## The Code

	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <meta name="viewport" content="width=device-width, minimum-scale=1.0">

	    <title>Find-A-Designer</title>

	    <style>

	    </style>
	</head>
	<body>
		<h1>Find-A-Designer</h1>
		<input id="search" type="text" placeholder="Enter a name"></input>
		<button id="button">Search for a Designer</button>
		<p id="results"></p>

		<script>
			var person1 = {
				first: "michael",
				last: "beirut"
			}

			var person2 = {
				first: "jessica",
				last: "helfand"
			}

			var person3 = {
				first: "ellen",
				last: "lupton"
			}

			var person4 = {
				first: "chip",
				last: "kid"
			}

			var person5 = {
				first: "marian",
				last: "bantjes"
			}

			var person6 = {
				first: "aaron",
				last: "draplin"
			}

			var person7 = {
				first: "susan",
				last: "kare"
			}

			var person8 = {
				first: "arnaud",
				last: "maggs"
			}

			var person9 = {
				first: "paula",
				last: "scher"
			}

			var person10 = {
				first: "paul",
				last: "rand"
			}

			var designers = [person1, person2, person3, person4, person5, person6, person7, person8, person9, person10]

		</script>
	</body>
	</html>