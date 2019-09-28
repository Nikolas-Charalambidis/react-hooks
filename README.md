[![Build Status](https://travis-ci.org/Nikolas-Charalambidis/react-hooks.svg?branch=master)](https://travis-ci.org/Nikolas-Charalambidis/react-hooks)

# react-hooks

A sample React web application automatically built and deployed via Travis CI. This application demonstrates my first attempt of using React, hooks and makes it autodeployed with each push to the `master` branch (except the commits ending to `[skip ci]` which skips the entire CI engine and is useful for `README.md` commits). 

Disclaimer: I have no idea how exactly `package.json` with `yarn` works and I am fully acknowledged the entire process might be done in a way all simpler, straightener and securer. This includes the `GITHUB_TOKEN` usage which probably might be secured using `travis encrypt` and/or a custom script deployment used instead. This is the first way worked and I made this repository as a tutorial for all who are interested. Obviously you are not allowed to deploy to this GitHub Page, yet you will know how to manage your own one :)

## [https://nikolas-charalambidis.github.io/react-hooks/](https://nikolas-charalambidis.github.io/react-hooks/)

## Phases

Here are a few basic scenarios you might want to go through.

### Localhost running

Simply type `yarn start` at the root of the checkout repository folder. The webpage automatically runs on `http://localhost:3000/` and updates with each file save.

### GitHub Pages manual deployment

Since the `gh-pages` dependency is included, run:

    yarn build
    yarn deploy
    
### GitHub Pages automatic deployment

Push to the `master` and don't touch anything in the `.travis.yml` and `package.json` You might want to change the `"homepage"` property otherwise you wouldn't be able to deploy, because the correct secure token is required. How to do so?

 1. Generate a new token at [https://github.com/settings/tokens](https://github.com/settings/tokens) with full rights to the `repo`.
 2. Use this token as a `GITHUB_TOKEN` variable and the token itself is its value. Don't let the token `DISPLAY VALUE IN BUILD LOG` or you have to use a new one.
 3. Include `github_token: $GITHUB_TOKEN` in the `deploy` with `provider: pages`. Now Travis CI should be authorized to push to the `gh-pages` branch, which is the default one.
 4. The last thing you might want to change is *what* exactly would get deployed. If you leave it as is, the entire repository content gets copied to the `gh-pages` branch. We want the content of newly created `build` folder generated using `yarn build` in the `.travis.yml` CI configuration file. Therefore, use `local_dir: build/` in the `deploy` which copies the *content* - mind the `/` at the end.

### Localhost deployment

If you want to make sure how the built webpage would look in the production, you might build it locally. Since the `package.json` is ready for the GitHub Pages deployment, you need to change the `homepage` property to:

    "homepage": "."
    
This configuration is required in order to correct paths usage for the resources loading and the error `Failed to load resource: net::ERR_FILE_NOT_FOUND` is present in the browser console. 
