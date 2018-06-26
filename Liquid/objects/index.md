# Liquid objects


Liquid objects contain attributes to output dynamic content on the page. For example, the product object contains an attribute called title that can be used to output the title of a product.

Liquid objects are also often referred to as Liquid variables.

To output an object's attribute, wrap the object's name in {{ and }}, as shown below:
```
{{ product.title }} <!-- Output: “Awesome Shoes” -->
```

In this article
* Global objects
* Content objects
* Other objects

## Global objects

The following objects can be used and accessed from any file in your theme, and are defined as global objects, or global variables:

### all_products
The all_products object contains a list of all the products in your store. You can use all_products to access products by their handles. More info ›
```
{{ all_products['wayfarer-shades'].title }}
```
Note
The all_products object has a limit of 20 unique handles per page. If you want more than 20 products, then consider using a collection instead.

### articles
The articles object can be used to retrieve an article using its handle.
```
{% assign article = articles['news/hello-world'] %}
{{ article.title | link_to: article.url }}
```

### blogs
The blogs object returns all the blogs in your store. More info ›
```
<ul>
  {% for article in blogs.myblog.articles  %}
   <li>{{ article.title | link_to: article.url }}</li>
  {% endfor %}
</ul>
```

### canonical_url
The canonical_url object returns the canonical URL for the current page. The canonical URL is the page's "default" URL with any URL parameters removed.

For products and variants, the canonical URL is the default product page with no collection or variant selected. For example, for a product in a collection with a variant selected:
```
https://docksupply.co/collections/classics/products/dory-shoes?variant=17287731270
```
The canonical URL is the product page:
```
https://docksupply.co/products/dory-shoes
```
Google's Search Console Help provides more information on canonical URLs.

### cart
The cart object returns your store's cart. More info ›

collections
The collections object returns all the collections in your store. More info ›

```
{% for product in collections.frontpage.products %}
  {{ product.title }}
{% endfor %}
```

### current_page
The current_page object returns the number of the page a customer is on when browsing through paginated content. More info ›
```
{% if current_page != 1 %}
  Page {{ current_page }}
{% endif %}
```

### current_tags
The current_tags object will return a different list of tags depending on the template that is being rendered. More info ›
```
<!-- in blog.liquid -->
{% if current_tags %}
  <h1>{{ blog.title | link_to: blog.url }} &rsaquo; {{ current_tags.first }}</h1>
{% else %}
  <h1>{{ blog.title }}</h1>
{% endif %}
```

### customer
The customer object returns the customer that is logged in to the store. It will not return anything if a customer isn't logged in. More info ›
```
{% if shop.customer_accounts_enabled %}
  {% if customer %}
    <a href="/account">My Account</a>
    {{ 'Log out' | customer_logout_link }}
  {% else %}
    {{ 'Log in' | customer_login_link }}
    {% if shop.customer_accounts_optional %}
      {{ 'Create an account' | customer_register_link }}
    {% endif %}
  {% endif %}
{% endif %}
```

### linklists
The linklists object returns the set of the menus and links in your store. You can access a menu by calling its handle on the linklists object. More info ›
```
<ul>
 {% for link in linklists.categories.links %}
    <li>{{ link.title | link_to: link.url }}</li>
  {% endfor %}
</ul>
```

### handle
The handle object returns the handle of the page that is being viewed. More info ›
```
{% if handle contains 'hide-from-search' %}
  <meta name="robots" content="noindex">
{% endif %}
```

### images
The images object lets you access any image in your store by its filename. More info ›
```
{% assign image = images['my-image.jpg'] %}
<img src="{{ image }}" alt="{{ image.alt }}">
```

### pages
The pages object returns a list of all the pages in your store. More info ›
```
<h1>{{ pages.about.title }}</h1>
<p>{{ pages.about.author }} says...</p>
<div>{{ pages.about.content }}</div>
```

### page_description
The page_description object returns the description of the product, collection, or page that is being rendered. Descriptions for these items can be set in your Shopify admin. More info ›
```
{% if page_description %}
  <meta name="description" content="{{ page_description }}" />
{% endif %}
```

### page_title
The page_title object returns the title of the current page. More info ›

### shop
The shop object contains information about your store. More info ›

### scripts
The scripts object returns information about a store's active scripts.

To access information about a script, use the syntax scripts.type, where type is the script type. There can be only one active script of a particular type. Currently, the only script type is cart_calculate_line_items.

To learn more about Shopify Scripts, visit the help content for the Shopify Scripts and the Script Editor .
```
{% if scripts.cart_calculate_line_items %}
  <p>We are currently running a {{ scripts.cart_calculate_line_items.name }} promotion!</p>
{% endif %}
```

### settings
The settings object lets you access the settings of a store's published theme. More info ›

```
{% if settings.logo %}
  {{ settings.logo | img_url | img_tag: shop.name }}
{% else %}
  <span class="no-logo">{{ shop.name }}</span>
{% endif %}
```

### template
The template object returns the name of the template that is being used to render the current page, not including its .liquid file extension. As a best practice, it's recommended that you apply the template name as a CSS class on your HTML <body> tag. More info ›
```
<body class="{{ template }}">
```

### theme
The theme object returns the store's published theme. More info ›
```
Visit the <a href="/admin/themes/{{ theme.id }}/settings">theme editor</a>.
```

## Content objects
The following objects are used to output the content of template and section files, as well as the scripts and stylesheets loaded by Shopify and Shopify apps.

### content_for_header
The content_for_header object is required in theme.liquid. It must be placed inside the HTML <head> tag. It dynamically loads all scripts required by Shopify into the document head. These scripts include Shopify analytics, Google Analytics, and scripts required for Shopify apps.

### content_for_index
The content_for_index object contains the content of dynamic sections to be rendered on the home page. This object must be included in templates/index.liquid.

### content_for_layout
The content_for_layout object is required in theme.liquid. It must be placed inside the HTML <body> tag. It dynamically loads content generated by other templates such as index.liquid or product.liquid.

## Other objects
Some Liquid objects are only used in specific circumstances.

### additional_checkout_buttons
Returns true if a merchant's store has any payment providers with offsite checkouts, such as PayPal Express Checkout. Use additional_checkout_buttons to check whether these gateways exist, and content_for_additional_checkout_buttons to show the additional buttons. More info ›

### content_for_additional_checkout_buttons
Returns checkout buttons for any active payment providers with offsite checkouts. More info ›

additional_checkout_buttons and content_for_additional_checkout_buttons are used in many Shopify themes:

```
{% if additional_checkout_buttons %}
  <div class="additional_checkout_buttons">{{ content_for_additional_checkout_buttons }}</div>
{% endif %}
```