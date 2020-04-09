Fantasy Basketball Draft App!

Fantasy Basketball Draft App is an app written in javascript designed to mimic a mock draft for an Fantasy Basketball League. See below for explanations of each section of the app:

The Database:<br>
The backend consists of a database madeup of seeded data created by the Faker gem. The seed file creates 12 fake owners for a 12 team maximum league. For each owner, the seed file creates 5 players associated with said owner, one for every player position (60 in total). An owner has many players and a player belongs to an owner. The associations are temporary and will be overwritten during the drafting process.

Controller Actions:<br>
The Owner and Player Controllers render APIs of json objects in RESTful URLs. The Player controller includes an update action which updates a specific json player object based on form params.

index.js:<br>
The index.js file displays various javascript objects with three different AJAX calls. 

Add an Owner:<br>
Upon the 'Add an Owner' button being clicked, the fetchOwners method is called, which calls a GET fetch method on the Owners API. The GET request takes the response and transfers the data into JSON. A new Owner is generated based on a random integer generated from the Random Owner Integer function, which generates a unique number (between 1 & 12) that serves as the placement of the array element representing a new owner JSON object. Once selected, that JSON object is fed into the JS Owner Object Constructor and creates a new Owner object. A div is created to store the owner information and prospective team roster, which is displayed in HTML by calling ownerHTML on the Owner object. Lastly, a "Draft a Player" button is appended to the HTML displaying the Owner info.

Draft a Player:<br>
Upon the "Draft a Player" button being clicked, the fetchPlayers method is called. It first checks if any of the roster elements are empty before calling a fetch GET request to the Players API. The request takes the response from the GET request and transfers the data to JSON. Using a similar Random Integer method, a new Player Object is generated by picking a random number (between 1 & 60) and using that to select the array element of the JSON objects. Based on the owner div where the player is drafted from, that owner's name is assigned as the player's owner. If the newly generated player's position is undrafted by the owner, then the player's information is displayed in a roster HTML using a playerHTML function called on the player. If the player's position has already been drafted by that owner, a new Player is continuously generated until a player matching a vacant position is generated. Two buttons are appended to the player information -- a button to edit the player's name, and a button to remove the player from the roster.

Edit Player Name:<br>
When the "Edit Name" button is clicked, a form containing an input field & submit button is generated in which the user can fill in a new name for the respective player. When the "Update Name" button is clicked, a fetch UPDATE request is called to the API of the specific player who's name is being updated. This request takes the updated response, converts the response to JSON, and updates the name of the player based on the value of the input field. The player's name will remain the same if nothing is entered into the form field and the submit button is clicked.

Remove Player:<br>
When the "X" button next to a player is clicked, the draft pick is deleted from an owner's roster. This is achieved by rendering the parent Element of the "X" blank. TO ensure the player can be drafted again, the Random Number used to generate the JSON player object is deleted from an array storing Random Numbers already used (which ensures a unique player is generated upon each click of the "Draft a Player" button).