# Login-System with Express and NodeJS

Users can register and login. Screenshots below

## Includes
- [Bootstrap](http://getbootstrap.com/) 
- [Font-Awesome](http://fontawesome.io/)
- [Google Fonts](https://fonts.google.com/)
- [LESS](http://lesscss.org/) Script for autocompiling with Node.js below in "How to Recreate Environment" Step 6
- [License free Images from Pexels.com](https://nodejs.org/en/) 
- Database (NoSQL, [MongoDB](https://www.mongodb.com/) )
- [BCrypt](http://nodecode.de/bcrypt) for password encryption
- Form Validation with [Express-Validator](https://github.com/ctavan/express-validator)
- [Multer](https://www.npmjs.com/package/multer) for user image upload
- [Express-Messages](https://github.com/expressjs/express-messages)
- [Jade](https://naltatis.github.io/jade-syntax-docs/) Template View
- [Backstretch](https://github.com/jquery-backstretch/jquery-backstretch) responsive showcase image
- [wow](https://wowjs.uk/) reveal animations
- heavily adapted [Registration Template ](http://azmind.com/free-bootstrap-themes-templates/)by AZMIND

## Requirements
- [Node.js](https://nodejs.org/en/)
- [Koala](http://koala-app.com/) Compiler for Sass
- [MongoDB](https://www.mongodb.com/) (installation manual below in "How to Recreate Environment")

## Manual Setup
1. Download mit Git:
```bash
git clone https://github.com/MariaHildebrandt/Geometrie-Rechner-mit-Laravel projectname
```
2. navigate to projectname and install with node package manager
```bash
npm install
```
3. start your project and open http://localhost:3000 in your browser
```bash
npm start
```

## Screenshots

#### Full View:
<p>
  <a href="https://postimg.org/image/wwj9smbhb/">Register</a>,
  <a href="https://postimg.org/image/fxabdd09r/">Login</a>
</p>

#### Preview:
<p align="left">
  <img src="https://s19.postimg.org/8g13y5aqr/nodelogreg.png"  width="400px">
  <img src="https://s19.postimg.org/llgm494mb/nodeloglogin.png"  width="400px">
</p>

## Work in Progress: ToDo and Bugs
#### Bugs: 
- none
#### ToDo: 
- Image upload with Multer is working but image display not implemented yet
- Members Area and Errors need CSS/LESS customization
- showcase picture (iPad) asymetrical to formular ->crop image

## How to Recreate Environment
#### 1.) Install and Setup MongoDb
- download msi file from [homepage](https://www.mongodb.com/)
- custom installation in C:/mongodb/
- in C:/mongodb create new folders: C:/mongodb/data and C:/mongodb/log
- open windows command prompt ans administrator and navigate to mongodb/bin folder
- C:\mongodb\bin>mongod --directoryperdb --dbpath C:\mongodb\data\db --logpath C:\mongodb\log\mongodb.log --logappend --rest --install
- start Service: C:\mongodb\bin>net start MongoDB (should say that the service was started successfully)
- open shell: C:\mongodb\bin>mongo

#### 2.) Create Database
- start shell in C:\mongodb\bin>mongo
```bash
use nodeauth
db.createCollection('users');
show collection
```
- insert a new user:
```bash
  db.users.insert({name:'Maria Hildebrandt', email:'hildebrandt.maria@googlemail.com', username:'Mary', password:'1234'});
```
- password will be encrypted later
```bash
db.users.find().pretty()
```
- shows content of users collection
##### Some MongoDB commands:
- change(update) content with:
```bash
db.users.update({username:'Mary'}, {$set:{username:'Maria'}});
```
- delete content with:
```bash
db.users.remove({username:'Maria'});
```
#### 3.) Express Generator for App & Middleware
- create new folder "nodeauth" (for ex. in your project folder)
- open folder in Git Bash
```bash
$ npm install -g express
$ npm install -g express generator
```
- in package.json: 
- jade: template engine
- add new dependencies: mongodb, mongoose, connect-flash(login messages), express-messages, express-session(http session), express-validator(for form validation),passport, passport-local, passport-http (login and registration), multer(image upload)
```bash
{
  "name": "nodeauth",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "start": "node ./bin/www"
  },
  "dependencies": {
    "bcryptjs": "^2.3.0",
    "body-parser": "~1.13.2",
    "connect-flash": "*",
    "cookie-parser": "~1.3.5",
    "debug": "~2.2.0",
    "express": "~4.13.1",
    "express-messages": "*",
    "express-session": "^1.13.0",
    "express-validator": "*",
    "jade": "~1.11.0",
    "mongodb": "*",
    "mongoose": "*",
    "morgan": "~1.6.1",
    "multer": "*",
    "passport": "*",
    "passport-http": "*",
    "passport-local": "*",
    "serve-favicon": "~2.3.0"
  }
}
```
- update changes:
```bash
$ npm install 
```
##### or install dependencies manually:
```bash
$ npm install express-session --save
```
#### 4.) Include all dependencies in app.js
```bash
var express = require('express');
var path = require('path');
var favicon = require('serve-favicon');
var logger = require('morgan');
var cookieParser = require('cookie-parser');
var bodyParser = require('body-parser');
var session = require('express-session');
var passport = require('passport');
var LocalStrategy = require('passport-local').Strategy;
var expressValidator = require('express-validator');
var multer = require('multer');
var upload = multer({dest: './uploads'});
var flash = require('connect-flash');
var bcrypt = require('bcryptjs');
var mongo = require('mongodb');
var mongoose = require('mongoose');
var db = mongoose.connection;
//(...)
var app = express();
```

#### 5.) Setup Middleware
##### express-session
```bash
app.use(session({
  secret:'secret',
  saveUninitialized: true,
  resave: true
}));
```
##### passport
```bash
app.use(passport.initialize());
app.use(passport.session());
```

##### express-validator
- copied from documentation of [Express-Validator](https://github.com/ctavan/express-validator)
```bash
app.use(expressValidator({
  errorFormatter: function(param, msg, value) {
      var namespace = param.split('.')
      , root    = namespace.shift()
      , formParam = root;

    while(namespace.length) {
      formParam += '[' + namespace.shift() + ']';
    }
    return {
      param : formParam,
      msg   : msg,
      value : value
    };
  }
}));
```
##### express-messages
- copied from documentation of [Express Messages](https://github.com/expressjs/express-messages)
```bash
app.use(flash());
app.use(function (req, res, next) {
  res.locals.messages = require('express-messages')(req, res);
  next();
});
```
#### Bcrypt
- [BCrypt](http://nodecode.de/bcrypt)
```bash
```

#### Multer Image-Upload
- from documentation: [Multer](https://www.npmjs.com/package/multer)
```bash
```
#### 6.) Layout and View
- download [Bootstrap](http://getbootstrap.com/) and place the file bootstrap.css into folder public/stylesheets
- put bootstrap.js in public/javascripts
- include bootstrap and jquery in your views/layout.jade file:
```bash
//head
link(href='/stylesheets/bootstrap.css', rel='stylesheet')
link(href='/stylesheets/style.css', rel='stylesheet')
//at the end of body container
script(src='https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js')
script(src='javascripts/bootstrap.js')
```
- in case you are not confident with the [Jade](https://naltatis.github.io/jade-syntax-docs/) Temmplate View, use the [Html2Jade](http://html2jade.org/)-Converter

##### Install LESS
- install LESS globally
```bash
$ npm install -g less
```
- for beginners [winless.org](http://winless.org/online-less-compiler) shows what is going on behind the scene when your are using LESS. 
- create an new file style.less in folder stylesheets
###### Option 1
- to compile navigate to projectname/public/stylesheets
```bash
$ lessc style.less style.css
```
###### Option 2: Autocompile in Node.js
- navigate to folder projectname and install node to dependencies. This will add less to your package.json file
```bash
$ npm i less --save-dev
```
- require LESS in app.js
```bash
var less = require('less');
var fs = require('fs');
```
- setup middleware:
```bash
fs.readFile('public/stylesheets/style.less', function(error, data){
    data = data.toString();
    less.render(data, function (e, output) {
        fs.writeFile('public/stylesheets/style.css', output.css, function(err){
            console.log('stylesheet compiled');
        });
    });
});
```
##### Install Backstretch
- download JS file from GitHub source and place in directory of your project
- install viea Bower:
```bash
bower install jquery-backstretch
```
- Setup in scripts.js. top-content is container class of your showcase:
```bash
jQuery(document).ready(function() {
    $('.top-content').backstretch("/img/backgrounds/1.jpg");
});
```
##### Install Font-Awesome
- download the package from FA Hompage and place it in your directory
- embed font-awesome.css in the header of the html file and edit the following lines to point to your directory:
```bash
src: url('/font-awesome/fonts/fontawesome-webfont.eot?v=4.6.2');
src: url('/font-awesome/fonts/fontawesome-webfont.eot?#iefix&v=4.6.2') format('embedded-opentype'), url('/font-awesome/fonts/fontawesome-webfont.woff2?v=4.6.2') format('woff2'), url('/font-awesome/fonts/fontawesome-webfont.woff?v=4.6.2') format('woff'), url('/font-awesome/fonts/fontawesome-webfont.ttf?v=4.6.2') format('truetype'), url('/font-awesome/fonts/fontawesome-webfont.svg?v=4.6.2#fontawesomeregular') format('svg');
```
##### Install WOW
- follow easy [manual](https://wowjs.uk/docs.html)
