# one-fits-all flavour

[![Greenkeeper badge](https://badges.greenkeeper.io/cyclejs-community/one-fits-all.svg)](https://greenkeeper.io/)

[Cycle-app](https://github.com/cyclejs-community/create-cycle-app) flavor.

## Installation

Run `create-cycle-app myAppName --flavor cycle-scripts-one-fits-all`

## Template

An elementary SPA. Each page is a cycle component and has its own state, which is persisted in local storage

Uses:
* xstream observables designed for HTML apps
* @cycle/dom and snabbdom for HTML rendering and events
* @cycle/http for http requests
* @cycle/time for accurate timing
* cycle-onionify and @cycle/isolate for fractal single state atom
* cycle-storageify and @cycle/storage for persistence in browser local storage
* cyclic-router and switch-path for routing and history management
* cycle-rerun for Hot Module Reloading (HMR)
* Custom HTML speech driver (write only)

## Language

Typescript (strict) with TSLint or ES6, uses the Typescript compiler for both.

## How does this flavor work

My goal is to create a flavor where you don't have to eject if you want to customize the config. This is now possible with the 3.0.0 update. The template will create a `webpack.config.js` inside your app folder that defines the entry points of the app. You can add to that config and it will be merged with the config defined in this flavor.

I strongly recommend [wepack-blocks](https://github.com/andywer/webpack-blocks) as they help a lot in making webpack easy.

## Migrating

To migrate an existing app to `5.0.0` you have to
* update `cycle-scripts-one-fits-all`
* update `package.json` like this:
```
"nyc": {
  "instrument": false,
  "sourceMap": false,
  "include": [<paths of files you want to test>, "src/components"],
  "reporter": ["html", "text-summary"]
},

"mocha-webpack": {
  "include": [
    "src/components/**/*.{jsx,js,ts,tsx}", //Should be the same as in nyc.include
    "test/**/*.test.{js,jsx,ts,tsx}" //All your tests
  ]
}
    
```
 
## Bundler

Webpack is configured using [webpack-blocks](https://github.com/andywer/webpack-blocks)
* [Webpack dev server](https://webpack.js.org/configuration/dev-server)
* [Hot Module Replacement](https://webpack.js.org/concepts/hot-module-replacement/)

## Scripts

- `npm start`: Start development server listening on port 8080
- `npm test`: Run the tests with mocha-webpack
- `npm run build`: Generate a production-ready build content, on the `build` folder (this folder is *gitignored*)
- `npm run eject`: Copy flavor's dependencies and configurations to the project folder, update `package.json` and remove the dependency on the flavored `cycle-scripts`. This is irreversible.
- `npm run clean`: Delete all the files and folders that were generated by the other commands (build, start and test)

### Config files
* webpack.config.js (Added to `config/` after running the eject script)
* webpack.config.test.js (Added to `config/` after running the eject script)
