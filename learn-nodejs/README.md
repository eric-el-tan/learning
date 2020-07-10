# learn-nodejs

## NodeJS

- [NodeJS](https://www.udemy.com/course/teachnodejs)
- [JS Intro](https://www.udemy.com/course/javascript-adv)


## NPM

> node -v

> npm -v

> cd /var/local/git/node
> mkdir learn-node
> cd learn-node

> npm init

> npm install express --save

## version
major.minor.bug
```json
"dependancies": {
 "nodemon": "^1.12.0"
}
```
- minor: new feature e.g. 1.13.0
- major: architectual change e.g 2.0.0 

do not update version
```json
'1.12.0' 
```
update to latest minor version 1.x.x 
```json
'^1.12.0'
```
update to latest bug version 1.12.x
```json
'~1.12.0'
```
update to latest version
```json
'latest'
```
download dependencies to *./node_modules*
> npm install
>
## global install
add new features, install to */usr/local/lib/node_modules* in Mac 
> npm install nodemon -g

nodemon will be installed to

> cd /var/local/git/node/learn-node
>
> nodemon hello.js
```shell script
[nodemon] starting `node hello.js`
hello3
[nodemon] clean exit - waiting for changes before restart
```
modify hello.js and save
```shell script
[nodemon] restarting due to changes...
[nodemon] starting `node hello.js`
hello12345
[nodemon] clean exit - waiting for changes before restart
```