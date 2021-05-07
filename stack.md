## Initial setup

start from empty repo

### create package subdirectories, init yarn, setup workspaces

We will be creating `web` and `sanity` directories later, but let's set yarn up
to recognize them as workspace folders now.

`yarn init` is dumb, especially for private repos, just create this
`package.json` for now:

```json
{
  "name": "repo-name",
  "version": "1.0.0",
  "private": true,
  "license": "UNLICENSED",
  "workspaces": ["web", "sanity"]
}
```

### install prettier, eslint, gitignore

`-D` install as dev dependencies, `-W` don't nag about workspace root

```sh
  yarn add -WD @hzdg/eslint-config eslint prettier
```

in project root, add `.eslintrc`:

```json
{
  "extends": [
    "@hzdg",
    "@hzdg/eslint-config-typescript",
    "@hzdg/eslint-config-react"
  ]
}
```

also add `prettier.config.js`:

```js
module.exports = require('@hzdg/eslint-config/prettier.config.js');
```

dont't forget your `.gitignore` file. After adding that would be a good time for
an initial push!

now let's setup next

## Initial Next setup

from the project root run the following to bootstrap a minimal next app with a
static index page and example api function

```sh
yarn create next-app web
```

after we run this we want to add one more script, `export` to the three that
were added to `web/package.json`, add the following in the `"scripts"` object:

```json
"export": "next export"
```

The export script will actually fail for now if run locally, because image
processing relies on the nextjs server or someother setup. We will address this
later

## npm

create `.npmrc` in web project:

```ini
always-auth=true
registry=https://npm.pkg.github.com/
//npm.pkg.github.com/:_authToken=${GITHUB_TOKEN}
```

(should we not yarnrc.yaml or whatever it is?)

## netlify web setup

[ ] setup env `GITHUB_TOKEN` in environment varibles section of netlify site

1. commit to repo
2. in netlify click _New site from Git_ button
3. pick project repo and don't worry about any other options
4. change site name
5. Go to _Build and deploY_ menu then in _Build settings_ set the base directory
   to `web/`
6. setup netlify projects web, studio (do we need studio?)
7. link projects
8. netlify.toml
9. link to repo
10. test CI

## more web

1. install styling? (maybe this is another section
2. create static page
3. create pagebuilder template stuff
4. execute

## Initial Sanity setup

1. create sanity project
2. locally install sanity to /sanity
3. link up projects
4. start with a basic schema
5. run sanity and add data

## sources

https://rhnmht30.dev/blog/next-image-with-netlify
