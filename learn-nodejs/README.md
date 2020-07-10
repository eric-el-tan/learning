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

"dependancies": {
 "nodemon": "^1.12.0"
}

1.12.0
major version: 1
minor version: 12
bug version: 0

new feature: 1.13.0
major change: 2.0.0 

^1.12.0 keep major version, update to latest minor 1.x.x 
~1.12.0 keep minor version, update to latest bug version 1.12.x
1.12.0 always do not update version
latest always update to latest

> rm -fr node_modules

> npm install
>
## global install
 
> npm install nodemon -g

nodemon will be installed to 
```
/usr/local/lib/node_modules (Mac)
```

> cd /var/local/git/node/learn-node
> nodemon hello.js
```
[nodemon] starting `node hello.js`
hello3
[nodemon] clean exit - waiting for changes before restart
```
update hello.js and save
```
[nodemon] restarting due to changes...
[nodemon] starting `node hello.js`
hello12345
[nodemon] clean exit - waiting for changes before restart


```