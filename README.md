# Eventing API Docs

## Installation

- You should have Ruby version 2.3.7 installed.
  - Install `rbenv` [https://github.com/rbenv/rbenv#installation](https://github.com/rbenv/rbenv#installation)
- You will also need to install bundler with `gem install bundler`
- Install middleman globally with `gem install middleman`
- Install the dependencies with `bundle exec install`
- Install Firebase's CLI tool with `npm install -g firebase-tools`
- Login to Firebase using `firebase login`

## Development workflow

- Start a dev server: `middleman server`
- Edit the /source/index.html.md file to make updates to the documentation

## Deployment

- Run `middleman build` to build the production bundle.
- Run `firebase deploy` to deploy your bundle to the Firebase server
