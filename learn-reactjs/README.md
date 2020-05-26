# React.Js

## Roadmap

- [React Roadmap](https://medium.com/free-code-camp/learning-react-roadmap-from-scratch-to-advanced-bff7735531b6)
- [Fullstack Roadmap](https://medium.com/@dtkatz/how-to-learn-fullstack-development-a-roadmap-in-charts-9b9e4aac400f)

## Reference
- [Start with nvm, npm, node and react](https://medium.com/@eisoftlabs/installing-and-using-nvm-npm-and-react-js-712bf612af20)
- [15 VSCode extension](https://levelup.gitconnected.com/15-vs-code-extension-to-save-your-time-and-make-you-a-better-developer-506f79baec53)



## Deployment

cd /var/local/git/react/mydeploy/deployment--01-finished

> npm run build

```
> react-complete-guide@0.1.0 build /var/local/git/react/mydeploy/deployment--01-finished
> node scripts/build.js

Creating an optimized production build...
Compiled successfully.

File sizes after gzip:

  73.27 KB  build/static/js/main.860317e4.js
  3.3 KB    build/static/js/0.20e32a95.chunk.js
  2.69 KB   build/static/js/1.ee5c0352.chunk.js
  2.51 KB   build/static/css/main.454467de.css
  1.52 KB   build/static/js/2.7bc24cc8.chunk.js

The project was built assuming it is hosted at the server root.
To override this, specify the homepage in your package.json.
For example, add this to build it for GitHub Pages:

  "homepage" : "http://myname.github.io/myapp",

The build folder is ready to be deployed.
You may serve it with a static server:

  npm install -g serve
  serve -s build

```

> sudo npm install -g firebase-tools


-------------------------------------------------------------------------

[Part 3: Installing Node,js using the Node Version Manager (NVM)
](https://hostadvice.com/how-to/how-to-install-node-js-on-ubuntu-18-04/)

> curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
```
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 12819  100 12819    0     0    811      0  0:00:15  0:00:15 --:--:--  3000
=> nvm is already installed in /home/erictan/.nvm, trying to update using git
=> => Compressing and cleaning up git repository

=> nvm source string already in /home/erictan/.bashrc
=> bash_completion source string already in /home/erictan/.bashrc
npm ERR! peer dep missing: bufferutil@^4.0.1, required by ws@7.3.0
npm ERR! peer dep missing: utf-8-validate@^5.0.2, required by ws@7.3.0
=> You currently have modules installed globally with `npm`. These will no
=> longer be linked to the active version of Node when you install a new node
=> with `nvm`; and they may (depending on how you construct your `$PATH`)
=> override the binaries of modules installed with `nvm`:

/usr/local/lib
├── create-react-app@3.4.1
└── firebase-tools@8.4.0
=> If you wish to uninstall them at a later point (or re-install them under your
=> `nvm` Nodes), you can remove them from the system Node as follows:

     $ nvm use system
     $ npm uninstall -g a_module

=> Close and reopen your terminal to start using nvm or run the following to use it now:

export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
``` 

> nvm --version
```
0.33.11
```
> nvm install node
```
Downloading and installing node v14.3.0...
Downloading https://nodejs.org/dist/v14.3.0/node-v14.3.0-linux-x64.tar.xz...
######################################################################### 100.0%
Computing checksum with sha256sum
Checksums matched!
Now using node v14.3.0 (npm v6.14.5)
Creating default alias: default -> node (-> v14.3.0)
```

erictan@coding:~$ npm --version
6.14.5
erictan@coding:~$ node --version
v14.3.0
erictan@coding:~$ nodejs --version
v8.10.0
erictan@coding:~$ 



> firebase login
    -   open chrome and login via google account
```
erictan@coding ~> firebase login
i  Firebase optionally collects CLI usage and error reporting information to help improve our products. Data is collected in accordance with Google's privacy policy (https://policies.google.com/privacy) and is not used to identify you.

? Allow Firebase to collect CLI usage and error reporting information? Yes
i  To change your data collection preference at any time, run `firebase logout` and log in again.

Visit this URL on this device to log in:
https://accounts.google.com/o/oauth2/auth?client_id=563584335869-fgrhgmd47bqnekij5i8b5pr03ho849e6.apps.googleusercontent.com&scope=email%20openid%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloudplatformprojects.readonly%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Ffirebase%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloud-platform&response_type=code&state=500868117&redirect_uri=http%3A%2F%2Flocalhost%3A9005

Waiting for authentication...

✔  Success! Logged in as eric.el.tan@gmail.com
```


> firebase init

```
Error: Invalid project id: ENTER_YOUR_PROJECT_ID_HERE.
Note: Project id must be all lowercase.
``` 

Problem: Invalid project id: ENTER_YOUR_PROJECT_ID_HERE.

 - [Fix](https://github.com/firebase/firebase-tools/issues/2203), to fix your system, open the file ~/.config/configstore/firebase-tools.json with your favorite editor. Look for the activeProjects key, then find the file path that has the invalid project identifier as the value in that collection. Remove it (making sure it remains valid JSON - check the ending commas) and that should remove the issue.
 
```
erictan@coding /v/l/g/r/react-burger> firebase init

     ######## #### ########  ######## ########     ###     ######  ########
     ##        ##  ##     ## ##       ##     ##  ##   ##  ##       ##
     ######    ##  ########  ######   ########  #########  ######  ######
     ##        ##  ##    ##  ##       ##     ## ##     ##       ## ##
     ##       #### ##     ## ######## ########  ##     ##  ######  ########

You're about to initialize a Firebase project in this directory:

  /var/local/git/react/react-burger

Before we get started, keep in mind:

  * You are currently outside your home directory
  * You are initializing in an existing Firebase project directory

? Which Firebase CLI features do you want to set up for this folder? Press Space to select features, then Enter to confirm your choice
s. 
 ◯ Database: Deploy Firebase Realtime Database Rules
 ◯ Firestore: Deploy rules and create indexes for Firestore
 ◯ Functions: Configure and deploy Cloud Functions
❯◉ Hosting: Configure and deploy Firebase Hosting sites
 ◯ Storage: Deploy Cloud Storage security rules
 ◯ Emulators: Set up local emulators for Firebase features

```