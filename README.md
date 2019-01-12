# angular-webpack-dashboard

This project serves as a simple example of how to get [`webpack-dashboard`](https://github.com/FormidableLabs/webpack-dashboard) running with Angular CLI >= @6 _without ejecting_.

The workflow takes advantage of Angular 6 builders to inject the necessary config to load `webpack-dashboard`. You can follow this [article](https://codeburst.io/customizing-angular-cli-6-build-an-alternative-to-ng-eject-a48304cd3b21) or read the steps below.

### Make sure you have Angular CLI >= @6 installed.

```sh
npm install -g @angular/cli
ng new angular-webpack-dashboard
cd angular-webpack-dashboard
```

### Add `@angular-builders/custom-webpack`.

```sh
npm i -D @angular-builders/custom-webpack
```

### Update `angular.json`

```json
"architect": {
   ...
  "build": {
      "builder": "@angular-builders/custom-webpack:browser"
      "options": {
            ...
      }
  ...
}
```

### Add `customWebpackConfig` to the build target options.

```json
"architect": {
   ...
  "build": {
      "builder": "@angular-builders/custom-webpack:browser"
      "options": {
            "customWebpackConfig": {
               "path": "./extra-webpack.config.js"
            }
            ...
      }
  ...
}
```

### Install `webpack-dashboard`.

```sh
npm i -D webpack-dashboard
```

### Create `extra-webpack.config.js` in the project root.

```js
const DashboardPlugin = require("webpack-dashboard/plugin");

module.exports = {
  plugins: [new DashboardPlugin()]
};
```

### Use `@angular-builders/dev-server`.

```sh
npm i -D @angular-builders/dev-server
```

Then, in `angular.json`:

```json
"serve": {
  "builder": "@angular-builders/dev-server:generic",
  ...
}
```

### Update the `package.json` `start` script.

```json
"scripts": {
  "ng": "ng",
  "start": "webpack-dashboard -- ng serve",
  ...
}
```

### Run `npm start` and party!
