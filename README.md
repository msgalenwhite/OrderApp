# Practice App

## If this is your first time using MongoDB, follow directions [here](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)

If on MacOS using Homebrew:

1) run `brew tap mongodb/brew`
2) Install MongoDB by running `brew install mongodb-community@4.2`
3) To have launchd start mongodb/brew/mongodb-community now and restart at login:
  `brew services start mongodb/brew/mongodb-community`
  Or, if you don't want/need a background service you can just run:
  `mongod --config /usr/local/etc/mongod.conf`
4) Connect and Use MongoDB: `mongo`


## To create a new Node application, as learned from [here](https://www.codementor.io/shanewignall/making-a-restful-backend-with-node-js-knf7nbsii)

1) `npm init`

Creates a package.json file with basic app information.

2) `npm i --save express mongoose`
3) `npm i --save-dev babel-cli babel-preset-env nodemon`

Express - for a webserver
Mongoose - to interact with MongoDB database
Babel - to compile ES6 syntax
Nodemon - auto restart project when files change

4) Generate '.babelrc' file.  Have it use the "env" plugin, which will transpile ES6 code:

```
{
  "presets": ["env"]
}
```

5) Add scripts to `package.json`:

```
{
...
"scripts": {
  "start": "nodemon server.js --exec babel-node --presets env",
  "release": "npm run clean && npm run build && npm run serve",
  "clean": "rm -rf dist && mkdir dist", "build": "babel . -s -D -d dist --presets env --ignore node_modules",
  "serve": "node dist/server.js"
},
...
}
```

Note: the command to run tests will have been created by the initial `npm init` command prompts.

6) Add folders for controllers, models, and routes.  File structure:

```
app-name/
├── controllers/
│ └── firstController.js
├── models/
│ └── firstModel.js
├── routes/
│ └── index.js
├── app.js
├── server.js
└── package.json
```

7) Set up the server:

```
import app from './app';

const port = process.env.PORT || '3000'; app.listen(port);

console.log(`Listening on port ${port}`);
```

8) Generate models by importing `Schema` from 'mongoose'

9) Define CRUD routes in `index.js`

10) Add functions to the controller to invoke the routes defined in `index.js`

11) Set up `app.js` to connect to the database and define "middleware" functions. These will have access to request and response objects, so they can handle errors and parse data.
