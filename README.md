# shopify_theme_development_guide
## Shopify Liquid
- Used for creating and modifying Shopify themes
## Shopify template and architecture file
- project
    - Layout
    - Templates
    - Sections
    - Assets
    - Config
    - Locales
## Shopify Liquid are categories in 3 features
1. Objects  { { ... } }
      - also known as variable , To output pices of data from a Shopify store
      - example :- {{ shop.name }}
      - learn Shopify objects ➡ [Read Docs](https://shopify.dev/api/liquid).
3. Tag { % ... % } { % end % }
      - TAGS are the programming logic that tells template what to do
      - Tags are divided into 3 category
          - Control flow TAGS  ex:- if,unless, else/elsif, case/when, and/or
          - iteration TAGS
          - theme variable TAGS
            1.   Template-specific HTML codes
            2.   Dividing arrays into multiple pages
            3.   To make Shopify themes use custom layouts/snippets
            4.   {% assign variable_name = shop.name %}
            5.   output :- {{variable_name}}
4. Filters {{ product.title | upcase }}
## login shopify partner account https://shopify.dev
## create a development store
## shopify CLI installation    [Rrad Docs](https://shopify.dev/themes/tools/cli/installation)
# initialize shopify project
1. ``` shopify theme init ```
2. ``` shopify theme init --clone-url=https://github.com/siddharthkumarrai/shopify_starter_template.git ```
3. ``` git clone https://github.com/siddharthkumarrai/shopify_starter_template.git ```
4. ``` shopify theme init [ NAME OF YOUR THEME ] --clone-url https://github.com/siddharthkumarrai/shopify_starter_template.git```
## connect shopify store to development environment
```node.js
    shopify theme dev --store siddharthkumarrai.myshopify.com
```
- if previous command not work
```node.js
    shopify auth logout
```
```node.js
    npm uninstall -g @shopify/cli @shopify/theme @shopify/hydrogen
    npm install -g @shopify/cli @shopify/theme
```
```node.js
    shopify login
```
```node.js
    shopify theme dev --store siddharthkumarrai.myshopify.com
```
#  Installing TailwindCSS to Shopify theme projects
1. ```node.js npm init -y```
2. ```node.js npm install -D tailwindcss ```
3. ```node.js npx tailwindcss init ```
> if not created tailwind.config.js then make manual
```node.js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./layout/*./liquid",
    "*",
    "./**/*.{liquid,html,js}", // Adjust this to match your Shopify theme files
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
```
> mkdir src touch input.css
```node.js
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
```
4. ```npx tailwindcss -i ./src/tailwind.css -o ./assests/application.css```
## Fixing Shopify CLI errors with .shopifyignore
> make .shopifyignore file in root directory
- write error file name ex:- package.json

