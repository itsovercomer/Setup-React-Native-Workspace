## Setup React Native Workspace for Fast Development

This note would help you setup the right work environment for your react native development which includes:

* Code hinting
* Auto-format code on file-save
* Auto-run ESLint at git commit - *ESLint helps maintain code structure and debugging*
* Use shortcuts to make coding faster

Before you begin, please [download VSCode](https://code.visualstudio.com/download) if you don't have it. If you do, open VSCode and let's begin...

Let's begin...

#### 1. Create a new react native app

To create a new app, we'll use `create-react-native-app`. First, lets install it.
```
npm install -g create-react-native-app
```

Create project `appname`.

```
create-react-native-app appname
```

Enter app directory and start the app.
```
cd appname
yarn start
```

#### 2. Setup ESLint

ESLint helps find problematic patterns or code that doesn't adhere to predefined style guidelines. It ensures that you're writing codes the right way.

First, install and ESLint.

```
yarn add --dev eslint
```

Next, we'll initialize ESLint and pay attention to the following initialization options:
```
./node_modules/.bin/eslint --init
```
* For rules, select `airbnb` or any other options you may prefer.
* For file type, select `json`

**Simplify Eslint call**

Add the following lines within the `scripts` object on `package.json`:

```
"lint": "eslint .",
"lint-fix":"eslint . --fix"
```

**Update Eslint config**

Add the following objects to the base object on `.eslintrc.json`:

```
"env": {
    "jest": true
},
"rules": {
    "react/jsx-filename-extension" : [
        "extensions": [".js",".jsx"]
    ]
}
```

#### 3. Code formatting

In order to ensure that written codes are well indented and formatted, we need to use `prettier` to help with formatting.

Install `prettier`

```
yarn add prettier --dev --exact
```

Example on how to run prettier:
```
yarn prettier --write "*.js"
```

**Combine ESLint and Prettier on a single command**

Update `scripts` in `package.json`.
```
"prettier": "prettier --write '*.js'",
"format-code": "yarn run prettier && yarn run lint:fix"
```

So from the above, when you run `yarn run format-code`, it will run `prettier` and also run `lint:fix`.

#### 4. Setup linting and prettier to run at commit

First, we beed to add `husky`:

```
yarn add lint-staged husky --dev
```

Setup precommit by adding the following to `scripts` in `package.json`.

```
"precommit": "lint-staged",
"lint-staged": {
    "*.js": ["yarn run format-code", "git add"]
}
```

#### 5. Format code on file-save

Search for and install *ESlint by Dirk Baeumer* on vscode extensions.

Search for and install *Prettier - Code formatter by Esben Petersen* on vscode extensions.

*Setup Prettier*:

Press `cmd + ,` or `ctrl + ,` to open up settings and add the following lines:

```
"prettier.eslintIntegration": true
```
This would ensure eslint is run when prettier runs.

Click on the `workspace settings` tab and add the following:

```
"editor.formatOnSave": true
```
This would format the code when you save a file.

#### 6. A Few Other Extensions for VSCode

* React Native Tools - *for code hinting*
* React-Native/React/Redux snippets for es6/es7 - *provides shortcuts*


### Credit

This note was extracted from [Spencer Carli](https://learn.handlebarlabs.com/courses/author/49797)'s free course on [How to Set up a New React Native Project](https://learn.handlebarlabs.com/courses/enrolled/253279). I highly recommend that you checkout the course for better understanding. Also, you will learn how to structure your codes.
