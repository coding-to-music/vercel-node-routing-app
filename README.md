# How to deploy a Node/Express App to Vercel

By Andrew Baisden
Posted on Sep 17, 2020

https://github.com/coding-to-music/vercel-node-routing-app

https://dev.to/andrewbaisden/how-to-deploy-a-node-express-app-to-vercel-2aa

http://localhost:3000

http://localhost:3000/about

http://localhost:3000/portfolio

http://localhost:3000/contact

This is just a quick simple example of course more complex applications will work as well.

## Prerequisites

### Step 1

Create an account with Vercel if you don't already have one.

Vercel is a cloud platform for static sites and Serverless Functions that fits perfectly with your workflow. It enables developers to host Jamstack websites and web services that deploy instantly, scale automatically, and requires no supervision, all with no configuration.

## Step 2

Use npm to install Vercel globally on your computer https://www.npmjs.com/package/vercel

```java
npm i -g vercel
Setup the project
Create a project
mkdir vercel-node-app
cd vercel-node-app
touch index.js
npm init -y
npm i express
```

Open the project in your code editor and then create a Node server in the index.js file

```java
const express = require('express');

const app = express();

app.get('/', (req, res) => res.send('Home Page Route'));

app.get('/about', (req, res) => res.send('About Page Route'));

app.get('/portfolio', (req, res) => res.send('Portfolio Page Route'));

app.get('/contact', (req, res) => res.send('Contact Page Route'));

const port = process.env.PORT || 3000;

app.listen(port, () => console.log(`Server running on ${port}, http://localhost:${port}`));
Create a run script in the package.json file
"scripts": {
"start": "node index.js"
},
```

Run the command below to see your Node app working locally in the browser

```java
npm run start
```

## Deploying to Vercel

Make sure that you are in the root folder for your project and then run the command vercel in your terminal.

Use the project setup settings below as a guide to setup your own project with Vercel.

```java
? Set up and deploy “~/Desktop/username/vercel-node-app”? [Y/n] y
? Which scope do you want to deploy to? username
? Link to existing project? [y/N] n
? What’s your project’s name? vercel-node-app
? In which directory is your code located? ./
No framework detected. Default Project Settings:

- Build Command: `npm run vercel-build` or `npm run build`
- Output Directory: `public` if it exists, or `.`
- Development Command: None
  ? Want to override the settings? [y/N] n
  Once that is complete it is going to give you some links. The app is NOT going to work yet it is only going to show you the code inside of your index.js file. You need to create a vercel.json file and put it in the root folder so that Vercel knows that it is a Node application. And it is very important that your index.js file remains in the root folder along with your other server side code for the project otherwise your app won't work.
```

Create a vercel.json file and put it in the root of your project folder and then add the code below

```java
{
    "version": 2,
    "builds": [
        {
            "src": "./index.js",
            "use": "@vercel/node"
        }
    ],
    "routes": [
        {
            "src": "/(.*)",
            "dest": "/"
        }
    ]
}
```

Now run the command vercel again to deploy your app. Open the Production link and your app should be working online with full working routes.
