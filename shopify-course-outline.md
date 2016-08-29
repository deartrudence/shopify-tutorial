# Shopify Course Outline

[Visit GitHub!](www.github.com)

## The Setup
* Download starter theme
* Setup development store
* Setup Starter theme in development store
* Should just see ‘main page :)’
* This is found in the ‘templates/index.liquid’ file
* Setup Theme watch for local development
* Now add some words to the index.liquid file, save and see the changes in the store!
* Setup Compass for sass compilation
* Upload sample products
  * Csv upload

## The Layout - Theme.liquid
* Brief intro to Liquid
* Bring in Header/Content
  * Bring in stylesheets
    1. <meta name="viewport" content="width=device-width, initial-scale=1">
    2. <title>{{ page_title}} - {{ shop.name }}</title>
    3. {{ "normalize.css" | asset_url | stylesheet_tag }}
    4. {{ 'styles.scss' | asset_url | stylesheet_tag }}
    5. Wrap p tags around words <p>The main page :)</p> to make sure styles took
  * Bring in JavaScript
    1. {{ "option_selection.js" | shopify_asset_url | script_tag }}
    2. {{ "shopify_common.js" | shopify_asset_url | script_tag }}
    3. {{ "customer_area.js"  | shopify_asset_url | script_tag }}
    4. {{ "//cdnjs.cloudflare.com/ajax/libs/jquery/3.1.0/jquery.min.js" | script_tag }}
* {{ content_for_layout}}
  * <div class="container">
      {{ content_for_layout}}
    </div>
  * Added blue box so you can see container
* Shop title
  * Our first use of Liquid templating
    * ```<h1><a href="/">{{ shop.name }}</a></h1>```
  * Bringing in an image with the asset_url
  * ```<img src="{{'logo.svg' | asset_url}}" class="logo" alt="pineapple">```
* Main Menu  
  * Linklist for main menu
    1. Go to online store/navigation, you’ll see menus.
    2. Click edit on the menu to find out the handle
    3. ```<ul>
      {% for link in linklists.main-menu.links %}
       <li {% if link.active %}class="current"{% endif %}><a href="{{ link.url }}">{{ link.title }}</a></li>
      {% endfor %}
        {{ content_for_layout}}
      </ul>```
  * Linklist for footer menu
    ```
    <footer>
    <ul>
    {% for link in linklists.footer.links %}
    <li {% if link.active %}class="current"{% endif %}><a href="{{ link.url }}">{{ link.title }}</a></li>
    {% endfor %}
    </ul>
    </footer>
    ```

  * shopify_asset_url
    * Returns the URL of a global assets that are found on Shopify's servers. Globally-hosted assets include:
      * option_selection.js
      * api.jquery.js
      * shopify_common.js,
      * customer_area.js
      * currencies.js
      * Customer.css




## Index.liquid
  * In the homepage page of the in the shopify panel and the bottom of the page in the Search engine listing preview section, the ‘handle’ of the page is the last bit of the url
  [](images/search-engine-preview.png)

Front page
Assign page {% assign page = pages.frontpage %}
<h2>{{ page.title }}</h2>
<p>{{ page.content }}</p>
About page
Create page.about.liquid
Go to about page
Must save for ‘templates’ dropdown to appear
Select page.about
{% assign page = pages.about-us %}
<h2>{{ page.title }}</h2>
<p>{{ page.content }}</p>
Add above to page.about.liquid

## Snippets - product-loop.liquid
Got to Products / Collections / Home page
Add all your products to the home collection
Snippets! Reusable bits of code!
{% for product in collection.products | limit:8 %}
      {% include 'product-loop' %}
    {% endfor %}
Cycle {% cycle '','','','last' %}

<div class="left {% cycle '','','','last' %}">
  <div>
    <a href="{{ product.url | within: collection }}">
      <img src="{{ product.featured_image.src | product_img_url: 'medium' }}" alt="{{ product.featured_image.alt | escape }}" />
    </a>
  </div>
  <div>
    <a href="{{ product.url | within: collection }}">
        {{ product.title }}
      </a>
  </div>
  <div >
    {% if product.price_varies %}From{% endif %}
    {{ product.price | money }}
  </div>
</div>

## The Product Page - Product.liquid
In the products section of the Shopify admin click on one of the products.  You’ll notice there is already a title and description and a price (and maybe some variants).  This was all added when we uploaded the sample products csv.
Product.liquid
the products featured image (code in 05-pineapple)
if the product has extra product shots (code in 05-pineapple)
Product title, cost, and description
navigating to previous/next product in the collection
If there are variants or not, select dropdown
A call back to check if there are variants, if it there are it checks availability. (js)
initialize multi selector for product (js)
selectCallback is a very important Javascript function that is used on the product template. Its main purpose is to split up a product’s options into multiple dropdowns, based on how many Options a product has. What’s important to know about selectCallback is that it triggers every time a user selects a different variant using the dropdowns. This means that it can be used to output information of the currently-selected variant such as price, compare at price, SKU, inventory quantity, etc. (for a full list of what can be output, seehttp://wiki.shopify.com/Variant).Notice how the price and availability of the variant now update as you select different variants from the dropdowns. That’s selectCallback at work baby!
The Cart - cart.liquid

## The Cart
{% if cart.item_count > 0 %}
<p>There's something in the cart</p>
{% else %}
<p>There's noting in your cart</p>
{% endif %}
Then you should see one of these messages at https://pineapple-18.myshopify.com/cart
Cart Form
Inside form table
2 submit forms
1 submit needs name=”chechout”, this takes you to checkout...all other names just update the form
If nothing, just have one sentence (maybe get that styled as well)
<h3>Cart: <a href="/cart">{{ cart.item_count }} {{ cart.item_count | pluralize: 'item', 'items' }} ({{ cart.total_price | money }})</a></h3>
On layout theme.liquid

## Pagination and the Collection and List-collection
Paginate the front page in index.liquid
Add more collections to shop
Make list-collection.liquid
Add collections to menu (in shopify admin onlinestore/navigation)
Same product-loop
Customer Accounts
7 .liquid files that allow returning customers to create an account, view their previous orders, set their default addresses, and more.
Enable customer accounts - Settings > Checkout  in customer accounts area select “Accounts are optional”
 browser, navigate to your-store-name.myshopify.com/account/register

## Create customer account
## Page.liquid (later)
