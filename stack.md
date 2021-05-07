## Initial setup

start from empty repo

### create package subdirectories, init yarn, setup workspaces

We will be creating `web` and `sanity` directories later, but let's set yarn up
to recognize them as workspace directories now.

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

## Initial Next Project setup

from the project root run the following to bootstrap a minimal next app with a
static index page and example api function

```sh
yarn create next-app web
cd web
```

We will be using packages from HZ's private github packages repo. Creating this
`.npmrc` in web project allows us to specify an access token in an environment
variable (which we will set in netlify later)

```ini
always-auth=true
registry=https://npm.pkg.github.com/
//npm.pkg.github.com/:_authToken=${GITHUB_TOKEN}
```

(should we not use yarnrc.yaml or whatever it is?)

## netlify web setup

### Add next and yarn support with netlify.toml

We need to configure netlify to properly host next. Netlify has a plugin that
will run the netlify export step, set up serverless support functions
as needed, and output static assets into the `out` directory.

We also to need explicitly to inform the netlify tooling that we are using yarn.
_(Netlify usually detects yarn projects by the presence of a lockfile, but our
yarn workspace setup maintains a single lockfile in the root directory, which is
above the base directory)_

create this `web/netlify.toml`

```toml
[build]
command = "yarn build"
publish = "out"

[build.environment]
NETLIFY_USE_YARN = "true"

[[plugins]]
package = "@netlify/plugin-nextjs"
```

### private git packages

setup env `GITHUB_TOKEN` in environment varibles section of netlify site

1. commit to repo
2. in netlify click _New site from Git_ button
3. pick project repo and don't worry about any other options
4. change site name
5. Go to _Build and deploY_ menu then in _Build settings_ set the base directory to `web/`
6. commit and push changes or trigger deploy

---

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
