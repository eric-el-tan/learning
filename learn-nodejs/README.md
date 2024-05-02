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
## [npm-check-updates](https://www.hostingadvice.com/how-to/update-npm-packages/#:~:text=One%20built%2Din%20way%20to,to%20easily%20upgrade%20your%20package)
```
npm install -g npm-check-updates
ncu --help
ncu

etan221@IT421751 MINGW64 /c/opt/04-research-budget/api-research-budget-v1 (master)
$ ncu
Checking C:\opt\04-research-budget\api-research-budget-v1\package.json
[====================] 23/23 100%

 @aws-sdk/client-ssm             ^3.27.0  →   ^3.567.0
 @types/aws-lambda              ^8.10.72  →  ^8.10.137
 @types/lodash                 ^4.14.192  →    ^4.17.0
 @types/node                   ^14.14.31  →   ^20.12.8
 @types/uuid                      ^8.3.4  →     ^9.0.8
 @uoa/lambda-tracing              ^1.6.0  →     ^2.1.2
 aws-sdk                        ^2.655.0  →  ^2.1611.0
 chai                             ^4.3.6  →     ^5.1.0
 dotenv                          ^16.0.3  →    ^16.4.5
 fsevents                         ^2.3.2  →     ^2.3.3
 lambda-local                     ^2.0.3  →     ^2.2.0
 mocha                           ^10.0.0  →    ^10.4.0
 moment                          ^2.29.4  →    ^2.30.1
 moment-timezone                 ^0.5.38  →    ^0.5.45
 oracledb-prebuilt-for-lambda     ^5.5.0  →     ^6.3.0
 sinon                           ^14.0.1  →    ^17.0.1
 typescript                       ^4.7.4  →     ^5.4.5
 uuid                             ^9.0.0  →     ^9.0.1

Run ncu -u to upgrade package.json

```