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
## connect shopify store to development environment
```node.js
    shopify theme dev --store siddharthkumarrai.myshopify.com
```

