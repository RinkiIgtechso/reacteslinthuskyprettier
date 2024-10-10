# Steps for creating a react typescript project with vite 🙌.

> It includes react, typescript, eslint, prettier, & husky 🔧.

###  Eslint 
ESLint is a popular open-source linting utility for JavaScript and TypeScript that helps developers identify and fix problems in their code. It is highly configurable and extensible, allowing teams to enforce coding standards, improve code quality, and catch common errors before they cause issues in production.

--------- 
### Prettier
Prettier is an opinionated code formatter designed to enforce a consistent style across your codebase. It automatically formats your code based on predefined rules, ensuring that it looks the same regardless of who wrote it or when it was written.

---------
### Husky
Husky is a tool that enables you to manage Git hooks in your projects easily. It allows you to run scripts at specific points in the Git workflow, such as before commits, before pushing changes, or after checking out a branch. This is particularly useful for enforcing code quality and consistency standards within a team.

-------------

### Start creating the project by running this command
`` npm create vite@latest ``

Once the project has been created, we need to add eslint, prettier & husky in this.
To add the prettier to your project, run the below-listed commands 👇:
 - ``npm install --save-dev --save-exact prettier`` to install the prettier locally. After that initialize the git in your project as it is necessary if you are gonna add prettier and husky.
 - ``node --eval "fs.writeFileSync('.prettierrc','{}\n')"`` create an empty config file to let editors and other tools know you are using Prettier.
 - ``node --eval "fs.writeFileSync('.prettierignore','# Ignore artifacts:\nbuild\ncoverage\n')"`` create a .prettierignore file to let the Prettier CLI and editors know which files to not format
 - ``npm install --save-dev eslint-config-prettier``
 - ``npm install --save-dev eslint-plugin-prettier``

After the above steps, just add this ``"lint": "eslint ./src --fix",`` inside script of package.json file and run ``npm run lint`` command to check whether we have successfully set up or not.

But before you proceed with the above thing, you may need to overwrite the eslint config file to make more proper.

```` import js from "@eslint/js";
import globals from "globals";
import reactHooks from "eslint-plugin-react-hooks";
import reactRefresh from "eslint-plugin-react-refresh";
import tseslint from "typescript-eslint";
import eslintConfigPrettier from "eslint-config-prettier";
import eslintPluginPrettierRecommended from 'eslint-plugin-prettier/recommended';

export default tseslint.config(
  { ignores: ["dist"] },
  {
    extends: [js.configs.recommended, ...tseslint.configs.recommended, eslintConfigPrettier, eslintPluginPrettierRecommended],
    files: ["**/*.{ts,tsx}"],
    languageOptions: {
      ecmaVersion: 2020,
      globals: globals.browser,
      parserOptions: {
    warnOnUnsupportedTypeScriptVersion: false,
  },
    },
    plugins: {
      "react-hooks": reactHooks,
      "react-refresh": reactRefresh,
    },
    rules: {
      ...reactHooks.configs.recommended.rules,
      "react-refresh/only-export-components": [
        "warn",
        { allowConstantExport: true },
      ],
      "no-unused-vars": ["error"],
       "@typescript-eslint/no-explicit-any": "error",
        quotes: ["error", "single"],
        "jsx-quotes": ["error", "prefer-double"]
    },
  },
);
````
And try to add something in your ``` App.tsx``` file. For example: you can include a variable that is not in used.
So, when you run the npm run lint command, it should through error of no-unused-var of eslint with typescript. If that so, then you have successfully set up the eslint in your project 🎊.

Now as we have completed set up for eslint & prettier, we need to add husky. And for this we need to run certain command 👇:
- `` npm install --save-dev husky lint-staged ``
- `` npx husky init ``
- `` node --eval "fs.writeFileSync('.husky/pre-commit','npx lint-staged\n')" ``

And also modify the ```.prettierrc``` file. Add the below code in your file:
```` 
{
    "trailingComma": "all",
    "tabWidth": 2,
    "semi": true,
    "singleQuote": true,
    "jsxSingleQuote": false,
    "endOfLine": "lf",
    "printWidth": 100,
    "arrowParens": "always"
}
````

These configurations in the Prettier file help standardize the code formatting across the project, ensuring consistency and readability.Including these rules in your Prettier config ensures a consistent coding style, avoids common formatting pitfalls, and simplifies collaboration in larger teams.

We have set up React TypeScript project with Vite and adding ESLint, Prettier, and Husky, and each tool serves a specific purpose in ensuring code quality, style consistency, and automated checks. 

### How They Work Together:
- ESLint checks for code quality and TypeScript errors.
- Prettier ensures the code is consistently formatted.
- Husky automates running these checks before commits to ensure code quality and formatting rules are followed by all developers, enforcing them before code is committed.


### Example Workflow:
- As you write code, ESLint warns you of potential problems and style issues.
- When you save your file, Prettier automatically formats the code to maintain consistency.
- When you try to commit your changes, Husky runs ESLint and Prettier checks to ensure everything is compliant. If there's an issue, it prevents the commit and prompts you to fix it before trying again.

This setup provides an automated way to maintain code quality and consistency across a team, leading to fewer bugs and a cleaner codebase. Now, you can try pushing your code on git.

Hurry 💥, Now we are good to go 🥳🎉.
