# Effortlessly Setting up Your React Project with Vite, Husky, TypeScript, and ESLint: A Comprehensive Guide

## **What we will learn**

This blog post provides a step-by-step guide to set up a React project using Vite, Husky, TypeScript, and ESLint. 

It explains the benefits of each tool and their role in ensuring a smooth and efficient development process. 

The post includes code snippets and screenshots to illustrate each step of the setup process, making it easy for readers to follow along.

To get The full code go to https://github.com/pappijx/Vite-react-eslint-prettier-husky-setup

## **Prerequisites**

Make sure you have Node.js installed on your machine. You can download it from the official website (https://nodejs.org/).

## **Setup Guide**

**1. Generate Vite + Typescript App**

-> After this you will be asked to enter your project name
```
terminal> npm create vite@latest
? Project name: » test-project
```

-> Next you need to select the framework of your choice
-> Select react here
```
? Select a framework: » - Use arrow-keys. Return to submit.
    Vanilla
    Vue
>   React
    Preact
    Lit
    Svelte
    Others
```

-> Next you need to add typescript to you project

```
? Select a variant: » - Use arrow-keys. Return to submit.
    JavaScript
>   TypeScript
    JavaScript + SWC
    TypeScript + SWC

```
-> After this you will see the final config as

```
terminal> npm create vite@latest
√ Project name: ... test-project
√ Select a framework: » React
√ Select a variant: » TypeScript

Scaffolding project in D:\Work\Blogs\test-project...

Done. Now run:

  cd test-project
  npm install
  npm run dev
```
-> To run the app we need to install dependencies, so just do 

```
terminal> npm i
```
-> After this you project directory and package.json looks like this


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/k7ftbjxymd3udek5psuz.png)


**2. Setup eslint**

-> First we need to install eslint as dev dependency
```
terminal> npm i -D eslint
```
-> Now we need to add a basic config file for eslint, for that

```
terminal> npx eslint --init

// this generates 

You can also run this command directly using 'npm init @eslint/config'.
Need to install the following packages:
  @eslint/create-config
Ok to proceed? (y)
```

-> Just say y (yes) here and proceed. After this we need to select the way we want to use eslint

```
? How would you like to use ESLint? ... 
  To check syntax only
> To check syntax and find problems
  To check syntax, find problems, and enforce code style
```
-> I will select the second option for now, and we will use airbnb style guide for eslint afterwards.

-> After this choose module type for your project, I will choose **Javascript modules**

```
? What type of modules does your project use? ...
> JavaScript modules (import/export)
  CommonJS (require/exports)
  None of these
```

-> Next choose framework as react

```
? Which framework does your project use? ...
> React
  Vue.js
  None of these
``` 
-> Next let the wizard know that we are using typescript

```
? Does your project use TypeScript? » No / Yes
// select yes and hit enter
```

-> Next select the platform where the will run, **select browser and hit enter**

```
? Where does your code run? ...  (Press <space> to select, <a> to toggle all, <i> to invert selection)
> Browser
  Node
```

-> Now select the .eslintrc file extension, I will go with **javascript** format.

```
? What format do you want your config file to be in? ...
> JavaScript
  YAML
  JSON
```

-> Now the wizard will ask you for **permission to install some dependencies**, hit enter and proceed

```
The config that you've selected requires the following dependencies:

eslint-plugin-react@latest @typescript-eslint/eslint-plugin@latest @typescript-eslint/parser@latest
? Would you like to install them now? » No / Yes  
```

-> And last question is, which package manager are you using? I am using npm, you can choose your package manager.

```
? Which package manager do you want to use? ... 
> npm
  yarn
  pnpm
```

-> Hitting enter initiates deps installation. And your root directory will have **.eslintrc.cjs** file with some basic settings.

-> **Now your package.json and .eslintrc files will look something like below**

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/81g68sqwpimp2ki0810p.png)

*There is an error in the *


-> Now we need to **setup a eslint style guide** in our project, **I am using airbnb**() as the base style.
This helps a developer to write proper and clean code.

So we run below command to get all the dependencies required by eslint airbnb style guide.

```
terminal> npx install-peerdeps --dev eslint-config-airbnb
Need to install the following packages:
  install-peerdeps
Ok to proceed? (y) y
```
-> Insert y and hit enter. Now your **devDependencies** looks like below.

```
"devDependencies": {
    "@types/react": "^18.0.28",
    "@types/react-dom": "^18.0.11",
    "@typescript-eslint/eslint-plugin": "^5.57.0",
    "@typescript-eslint/parser": "^5.57.0",
    "@vitejs/plugin-react": "^3.1.0",
    "eslint": "^8.2.0",
    "eslint-config-airbnb": "^19.0.4",
    "eslint-plugin-import": "^2.25.3",
    "eslint-plugin-jsx-a11y": "^6.5.1",
    "eslint-plugin-react": "^7.28.0",
    "eslint-plugin-react-hooks": "^4.3.0",
    "typescript": "^4.9.3",
    "vite": "^4.2.0"
  }
```

-> Just add "airbnb", "airbnb/hooks" in your .eslintrc files extends key. Now your .eslintrc files looks like below

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/su3b2f5mlmy43t9hby84.png)

-> we need to add typescript support for eslint-airbnb

```
terminal> npm install --save-dev eslint-config-airbnb-typescript
```
-> After this add 'airbnb-typescript' to your **.eslintrc** extends array.

-> After this we need to add **project: './tsconfig.json'** to out **.eslintrc** parserOptions.

-> You have a different error at top line in **.eslintrc** file as shown below.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1scxjxactn86por2ur68.png)

-> This is because our **.eslintrc** file is not looked up by **tsconfig** file. So we need to add this in tsconfig.json, like below

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/dw6kajrhasprngqf5s1f.png)

-> After this open any tsx file, you will see blood all over the screen. This is because we are following airbnb guide for javascript.

Let open app.tsx file and remove all not so important code. So now the file looks like below with an error.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/2hht0avd2hl54acob8l2.png)

The error says
```
'React' must be in scope when using JSXeslint
```
This error occurs because airbnb style guide forces us to import React from 'react' as in old react this was a requirement, but in new versions of react we don't need this.

To escape this rule we will add exception in **.eslintrc** file in rules array.

```
module.exports = {
  env: {
    browser: true,
    es2021: true,
  },
  extends: [
    'airbnb',
    'airbnb-typescript',
    'airbnb/hooks',
    'plugin:react/recommended',
    'plugin:@typescript-eslint/recommended',
  ],
  overrides: [],
  parser: '@typescript-eslint/parser',
  parserOptions: {
    ecmaVersion: 'latest',
    sourceType: 'module',
    project: './tsconfig.json',
  },
  plugins: ['react', '@typescript-eslint'],
  rules: {
    'react/react-in-jsx-scope': 0,
  },
};

```

Thats it for eslintrc file.

**3. Add Prettier**

-> We need prettier to format our code properly so that it is more readable and so everyone use similar code formatting

-> So now just install all prettier dependencies
```
terminal> npm i -D prettier eslint-config-prettier eslint-plugin-prettier
```
-> Now create .prettierrc.cjs file in root directory

```
module.exports = {
  trailingComma: "es5",
  tabWidth: 2,
  semi: true,
  singleQuote: true,
};
```

Thats all for prettier!!!

**4. Add husky to project**
-> Now, this is the easiest thing to do but the most important. Using husky you make your team follow the guidelines specified by you and that makes code cleaner and helps make good coding implementations.

-> To install husky just do

```
npx mrm@2 lint-staged
npm i
```

and then just add the below lines to your package.json.

```
"lint-staged": {
        "*.{js,css,ts,tsx,jsx}": [
"prettier --write", "eslint --fix"]
    }
```
*Keep in mind to add eslint after prettier else it both will conflict and husky generates error*

## **Thats it, You now have a well structured project with prettier, eslint, husky and vite.**

