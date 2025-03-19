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
- Tailwind CLI
> Terminal
```javascript
npm install tailwindcss @tailwindcss/cli
```
> src/input.css
```javascript
@import "tailwindcss";
```
> Terminal
```javascript
npx @tailwindcss/cli -i ./src/input.css -o ./src/output.css --watch
```
> src/index.html
```javascript
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="./output.css" rel="stylesheet">
</head>
<body>
  <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
</body>
</html>
```
## Fixing Shopify CLI errors with .shopifyignore
> make .shopifyignore file in root directory
- write ( error file name )
- example:- package.json
## Folders and file structure of source code
> sections/header.liquid
```javascript
```
> layout/theme.liquid
```javascript
  <body>
    {% section 'header' %}
    {% section 'hero_section_slider' %}
    <main role="main">
      {{ content_for_layout }}
    </main>
  </body>
```
## How to display links
```html
<nav x-data="{ open: false }">
        {% for link in linklists['main-menu'].links %}
          {% if link.links != blank %}
              <button
                x-on:click="open = ! open"
                type="button"
              >
                {{ link.title }}
                {% render 'drop-down-arrow' %}
              </button>
              <div
                x-show="open"
                @click.away="open = false"
              >
                    {% for childlink in link.links %}
                      <a href="{{ childlink.url }}">
                          <p class="text-gray-900 text-base font-medium">{{ childlink.title }}</p>
                      </a>
                    {% endfor %}
          {% else %}
            <div class="relative">
              <a
                href="{{ link.url }}"
                class="
                  {% if link.active == true %}
                    text-red-500
                  {% endif -%}
                  text-base
                  text-gray-500
                  hover:text-gray-900
                "
              >
                {{ link.title }}
              </a>
            </div>
          {% endif %}
        {% endfor %}
      </nav>
```
## How to use icon
> snippets/icon-bag.liquid
```svg
<svg width="18" height="20" viewBox="0 0 18 20" fill="none" xmlns="http://www.w3.org/2000/svg">
  <path d="M17 14 8.26522 14 8V7H16V17Z" fill="currentColor"/>
</svg>
```
> sections/header.liquid
```html
<a href="{{ routes.cart_url }}">
    {%- render 'icon-bag' -%}
</a>
```
## Schema Tag
![Alt text](https://res.cloudinary.com/dnknslaku/image/upload/v1741759999/projects_images/logo/Screenshot_356_oec4hs.png)
## JSON Templates
![Alt text](https://res.cloudinary.com/dnknslaku/image/upload/v1741845243/projects_images/logo/Screenshot_375_djeb6r.png)

## Templates Attributes how work
 ```templates/404.json```
```json
{
    "name": "Template 404",
    "layout": "custom_theme",
    "wrapper": "div#404_template.custom-class[custom-attribute=hello]",
    "sections": {
        "template-404": {
                "type": "example-404"
        },
        "order": ["template-404"]
}
#### step 2: Create the ```layout/custom_theme.liquid``` file
#### step 3: Create the ```sections/example-404.liquid``` file
#### step 4: order attribute array will value is section_id ( for ex: template-404 )


#### Step 1: Create the ```templates/404.json``` File
```json
{
  "sections": {
    "main_id": {
      "type": "main-404",
      "settings": {}
    }
  },
  "order": ["main_id"]
}
```
### Good Practice for tamplate
1. Step 1: create ```templates/404.json```
> templates/404.json
```json
{
    "name": "Template 404",
    "sections": {
        "template":{
            "type": "template-404"
         }
     },
     "order": ["template"]
}
```
2.) Step 2: create ```sections/template-404.liquid```
> sections/template-404.liquid
```liquid
<div class="page-404">
  <h1>{{ section.settings.title}}</h1>
  <p>{{ section.settings.Subtext_title }}</p>

    {% if section.settings.button_url == blank %}
        {% assign shop_url = shop.secure_url %}
    {% else %}
        {% assign shop_url = section.settings.button_url %}
    {% ebdif %}
    <a href="{{  shop_url }}"> {{ section.settings.button_label }}</a>


  <!-- Search Form -->
  <form action="/search" method="get" class="search-form">
    <input type="text" name="q" placeholder="Search the store...">
    <button type="submit">Search</button>
  </form>
</div>

<style>
  .page-404 {
    text-align: center;
    padding: 50px 20px;
  }
</style>

{% schema %}
{
  "name": "Template 404",
  "tag": "section",
  "class" "flex item-center justify-center"
  "settings":[
       {
            "type": "text",
            "id": "title",
            "default": "404",
            "label": "404 Heading Title"
       },
       {
            "type": "text",
            "id": "subtext_titlle",
            "default": "The page thaat you're looking for is not found",
            "label": "404 Subtext Title"
       },
       {
            "type": "text",
            "id": "button_label",
            "default": "Back to homepage",
            "label": "Button Label"
       },
       {
            "type": "url",
            "id": "button_url",
            "label": Button URL"
   ]
}
{% endschema %}
```
