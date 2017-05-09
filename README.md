# Login-System with Express and NodeJS
- Users can register and login

## Includes
- [Bootstrap](http://getbootstrap.com/) and CSS
- [Sass](http://sass-lang.com/)
- [Font Awesome](http://fontawesome.io/)
- [License free Images from Pexels.com](https://nodejs.org/en/) 
- [Google Fonts Link](https://fonts.google.com/)
- Database (NoSQL)
- BCrypt for password encryption
- form validation with Express-Validation

## Requirements
- NodeJS
- [Koala](http://koala-app.com/) Compiler for Sass
- MongoDB (installation manual below in "How to Recreate")

## Manual Setup
1. Download mit Git:
```bash
git clone https://github.com/MariaHildebrandt/Geometrie-Rechner-mit-Laravel projectname
```
2. navigate to projectname and install with node package manager
```bash
npm install
```

## Screenshots

#### Full View:
<p>
  <a href="">Pic</a>,
</p>

#### Preview:
<p align="left">
  <img src=""  width="">
</p>

## How to recreate
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
```

#### 5.) Views and Layout
- in folder nodeauth/routes/users.js:
```bash

```

