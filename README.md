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

## Requirements
- NodeJS
- [Koala](http://koala-app.com/) Compiler for Sass
- MongoDB (installation manual below in "How to Recreate")

## Manual Setup

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




