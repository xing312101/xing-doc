# React.js

## using toolchain: create-react-app
```
notice: 不太建議用 npx ，因為在某些系統安裝時會卡住，可以考慮npm install -g 安裝及initial project

$ npm cache clean --force // 避免卡住的方式之一，但我的SERVER環境無效
$ npx create-react-app hello_react

or

$ npm cache clean --force
$ npm install create-react-app -g
$ create-react-app hello_react


Creating a new React app in /home/xing312101/hello_react

Installing packages. This might take a couple of minutes.
Installing react, react-dom, and react-scripts with cra-template...
... ...
Aborting installation.
  npm install --save --save-exact --loglevel error react react-dom react-scripts cra-template has failed.

Deleting generated file... node_modules
Deleting generated file... package.json
Done.
```

結論: 安裝失敗，改用yarn的方式安裝成功

## using yarn to install
```
npm install -g yarn

// Method 1
yarn global add create-react-app
create-react-app hello_react

// Method 2
yarn create react-app hello_react
```
### result:

```
xing312101@instance-free:~$ npm install -g yarn
/home/xing312101/.nvm/versions/node/v12.18.2/bin/yarn -> /home/xing312101/.nvm/versions/node/v12.18.2/lib/node_modules/yarn/bin/yarn.js
/home/xing312101/.nvm/versions/node/v12.18.2/bin/yarnpkg -> /home/xing312101/.nvm/versions/node/v12.18.2/lib/node_modules/yarn/bin/yarn.js
+ yarn@1.22.4
added 1 package in 0.461s
xing312101@instance-free:~$ yarn create react-app hello_react
yarn create v1.22.4
[1/4] Resolving packages...
[2/4] Fetching packages...
[3/4] Linking dependencies...
[4/4] Building fresh packages...
success Installed "create-react-app@3.4.1" with binaries:
      - create-react-app
[###################################################################################################] 99/99
Creating a new React app in /home/xing312101/hello_react.

Installing packages. This might take a couple of minutes.
Installing react, react-dom, and react-scripts with cra-template...

yarn add v1.22.4
[1/4] Resolving packages...
[2/4] Fetching packages...
info fsevents@1.2.12: The platform "linux" is incompatible with this module.
info "fsevents@1.2.12" is an optional dependency and failed compatibility check. Excluding it from installation.
info fsevents@2.1.2: The platform "linux" is incompatible with this module.
info "fsevents@2.1.2" is an optional dependency and failed compatibility check. Excluding it from installation.
[3/4] Linking dependencies...
warning "react-scripts > @typescript-eslint/eslint-plugin > tsutils@3.17.1" has unmet peer dependency "typescript@>=2.8.0 || >= 3.2.0-dev || >= 3.3.0-dev || >= 3.4.0-dev || >= 3.5.0-dev || >= 3.6.0-dev || >= 3.6.0-beta || >= 3.7.0-dev || >= 3.7.0-beta".
[4/4] Building fresh packages...
success Saved lockfile.
success Saved 15 new dependencies.
info Direct dependencies
├─ cra-template@1.0.3
├─ react-dom@16.13.1
├─ react-scripts@3.4.1
└─ react@16.13.1
info All dependencies
├─ @babel/helper-member-expression-to-functions@7.11.0
├─ @babel/plugin-syntax-typescript@7.10.4
├─ @babel/plugin-transform-flow-strip-types@7.9.0
├─ @babel/plugin-transform-runtime@7.9.0
├─ @babel/plugin-transform-typescript@7.11.0
├─ @babel/preset-typescript@7.9.0
├─ babel-preset-react-app@9.1.2
├─ cra-template@1.0.3
├─ eslint-config-react-app@5.2.1
├─ react-dev-utils@10.2.1
├─ react-dom@16.13.1
├─ react-error-overlay@6.0.7
├─ react-scripts@3.4.1
├─ react@16.13.1
└─ scheduler@0.19.1
Done in 135.36s.

Installing template dependencies using yarnpkg...
yarn add v1.22.4
[1/4] Resolving packages...
warning @testing-library/react > @types/testing-library__react > @types/testing-library__dom@7.5.0: This is a stub types definition. testing-library__dom provides its own type definitions, so you do not need this installed.
[2/4] Fetching packages...
info fsevents@2.1.2: The platform "linux" is incompatible with this module.
info "fsevents@2.1.2" is an optional dependency and failed compatibility check. Excluding it from installation.
info fsevents@1.2.12: The platform "linux" is incompatible with this module.
info "fsevents@1.2.12" is an optional dependency and failed compatibility check. Excluding it from installation.
[3/4] Linking dependencies...
warning "react-scripts > @typescript-eslint/eslint-plugin > tsutils@3.17.1" has unmet peer dependency "typescript@>=2.8.0 || >= 3.2.0-dev || >= 3.3.0-dev || >= 3.4.0-dev || >= 3.5.0-dev || >= 3.6.0-dev || >= 3.6.0-beta || >= 3.7.0-dev || >= 3.7.0-beta".
warning " > @testing-library/user-event@7.2.1" has unmet peer dependency "@testing-library/dom@>=5".
[4/4] Building fresh packages...
success Saved lockfile.
success Saved 22 new dependencies.
info Direct dependencies
├─ @testing-library/jest-dom@4.2.4
├─ @testing-library/react@9.5.0
├─ @testing-library/user-event@7.2.1
├─ react-dom@16.13.1
└─ react@16.13.1
info All dependencies
├─ @babel/runtime-corejs3@7.11.0
├─ @sheerun/mutationobserver-shim@0.3.3
├─ @testing-library/dom@6.16.0
├─ @testing-library/jest-dom@4.2.4
├─ @testing-library/react@9.5.0
├─ @testing-library/user-event@7.2.1
├─ @types/aria-query@4.2.0
├─ @types/prop-types@15.7.3
├─ @types/react-dom@16.9.8
├─ @types/react@16.9.44
├─ @types/testing-library__dom@7.5.0
├─ @types/testing-library__react@9.1.3
├─ aria-query@4.2.2
├─ css.escape@1.5.1
├─ csstype@3.0.2
├─ dom-accessibility-api@0.3.0
├─ min-indent@1.0.1
├─ react-dom@16.13.1
├─ react@16.13.1
├─ redent@3.0.0
├─ strip-indent@3.0.0
└─ wait-for-expect@3.0.2
Done in 42.34s.
Removing template package using yarnpkg...

yarn remove v1.22.4
[1/2] Removing module cra-template...
[2/2] Regenerating lockfile and installing missing dependencies...
info fsevents@2.1.2: The platform "linux" is incompatible with this module.
info "fsevents@2.1.2" is an optional dependency and failed compatibility check. Excluding it from installation.
info fsevents@1.2.12: The platform "linux" is incompatible with this module.
info "fsevents@1.2.12" is an optional dependency and failed compatibility check. Excluding it from installation.
warning " > @testing-library/user-event@7.2.1" has unmet peer dependency "@testing-library/dom@>=5".
warning "react-scripts > @typescript-eslint/eslint-plugin > tsutils@3.17.1" has unmet peer dependency "typescript@>=2.8.0 || >= 3.2.0-dev || >= 3.3.0-dev || >= 3.4.0-dev || >= 3.5.0-dev || >= 3.6.0-dev || >= 3.6.0-beta || >= 3.7.0-dev || >= 3.7.0-beta".
success Uninstalled packages.
Done in 25.63s.

Success! Created hello_react at /home/xing312101/hello_react
Inside that directory, you can run several commands:

  yarn start
    Starts the development server.

  yarn build
    Bundles the app into static files for production.

  yarn test
    Starts the test runner.

  yarn eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd hello_react
  yarn start

You had a `README.md` file, we renamed it to `README.old.md`

Happy hacking!
Done in 217.38s.
```

## Start server to check
```
## start dev server for checking initail success
$ npm start
$ yarn start
```

## build production
```
$ npm run build
$ yarn build
```
