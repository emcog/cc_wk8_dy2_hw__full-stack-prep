# cc_wk8_dy2_hw__full-stack-prep
Notes on reading an exsiting codebase


### Questions

1. What is responsible for defining the routes of the `games` resource?
2. What do you notice about the folder structure?  Whats the client responsible for? Whats the server responsible for?
3. What are the the responsibilities of server.js?
4. What are the responsibilities of the `gamesRouter`?
5. What process does the the client (front-end) use to communicate with the server?
6. What optional second argument does the `fetch` method take? And what is it used for in this application? Hint: See [Using Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) on the MDN docs
7. Which of the games API routes does the front-end application consume (i.e. make requests to)?
8. What are we using the [MongoDB Driver](http://mongodb.github.io/node-mongodb-native/) for?


## 1. What is responsible for defining the routes of the `games` resource?
GamesService.js (const baseURL = ...)

## 2. What do you notice about the folder structure?  Whats the client responsible for? Whats the server responsible for?
### Client responsbilility
- CRUD to server (GET, POST, DELETE) are defined in GamesService and handled in GameForm, which has a base url of local/3000
– Renders DOM

### Server responsbilility
– CRUD with database (GET, POST, DELETE & PUT) are defined in create_router.js
– creates the server
– seeds.js creates the db and populates with inital data
– server.js connects to the DB on port 27017
– Using express server.js listens to port 3000 for any CRUD "activity" emited from the event bus of GamesFrom.vue

### What are the the responsibilities of server.js?
– initalise ther server using express
– connect to DB on 27017
– listen to client on 3000
– parse header/body and only pass body to DB
– use cors to allow cross origin "actions"


### What are the responsibilities of the `gamesRouter`?
– it a creates a route which connects in a collection from the DB
– this route is then used to connect front and back end through app.use

### What process does the the client (front-end) use to communicate with the server?
– CRUD functions defined in GamesService are imported to the components GamesForm.vue, GamesGrid and GamesCard.
– The components handle different parts of the CRUD
– GamesFrom and GamesCard emit to local:3000 which is rendered in the DOM
– Server.js listens for changes on port 3000 and handles requests to the DB

### What optional second argument does the `fetch` method take? And what is it used for in this application?
– the second argument of fetch is a data object
– used in postGame function in GamesService.js
– postGanne is implemented in GameFrom.vue and is used to **add games**


### Which of the games API routes does the front-end application consume (i.e. make requests to)?
– GET, POST, DELETE

### What are we using the [MongoDB Driver](http://mongodb.github.io/node-mongodb-native/) for?
– its gives us the ID of an object in our database


### Why do we need to use ObjectId from the MongoDB driver
– We use the ID object to CRUD on
– from the docs "callback-based and Promise-based interaction"
– promised-based interaction is asynchronous and prevents javascripts single-thread from becoming blocked, i.e. slow/unresponive

