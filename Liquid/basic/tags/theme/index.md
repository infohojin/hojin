# Theme tags
Theme tags have many functions, including:

Outputting template-specific HTML markup
Telling the theme which layout and snippets to use
Splitting a returned array into multiple pages.

In this article
* comment
* include
* form
* layout
* paginate
* raw
* section

## comment
Allows you to leave un-rendered code inside a Liquid template. Any text within the opening and closing comment blocks will not be output, and any Liquid code within will not be executed.

Input
```
My name is Wilson Abercrombie{% comment %}, esquire{% endcomment %}.
```

Output
```
My name is Wilson Abercrombie.
```

## include
Inserts a snippet from the snippets folder of a theme.
```
{% include 'my-snippet-file' %}
```
Note 
that you don't need to write the file's .liquid extension.

When you include a snippet, the code inside it will have access to the variables within its parent template.

## Including multiple variables in a snippet
There are two ways to include multiple variables in a snippet. You can assign and include them on different lines, which creates them in the parent template:
```
{% assign my_variable = 'apples' %}
{% assign my_second_variable = 'oranges' %}
{% include 'snippet' %}
```
 
Or you can create variables on the same line where you include the snippet:
 
```
{% include 'snippet', my_variable: 'apples', my_other_variable: 'oranges' %}
```

## include tag parameters
### with
The with parameter assigns a value to a variable inside a snippet that shares the same name as the snippet.

For example, if you have a snippet named color.liquid which contains the following:

color.liquid
```
color: '{{ color }}'
shape: '{{ shape }}'
```
Within theme.liquid, you can include the color.liquid snippet as follows:

Input
```
{% assign shape = 'circle' %}
{% include 'color' %}
{% include 'color' with 'red' %}
{% include 'color' with 'blue' %}
{% assign shape = 'square' %}
{% include 'color' with 'red' %}
```

Which will produce:

Output
```
color: '' shape: 'circle'
color: 'red' shape: 'circle'
color: 'blue' shape: 'circle'
color: 'red' shape: 'square'
```

### form
Creates an HTML `<form>` element along with the required `<input>` elements to submit the form to a particular endpoint.

### form types and tag parameters
There are many types of forms that can be created and submitted in Shopify themes. Adding a product to the cart, creating a customer account, and commenting on a blog article all require `<form>` elements with different attributes and `<input>` elements.

To create different forms, the {% form %} tag requires a type and might require additional parameters. For example, the form used to submit a comment on a blog article requires the type of new_comment and needs an article object as a parameter.

```
{% form 'new_comment', article %}
...
{% endform %}
```

The different form types and their required parameters are listed below.

### activate_customer_password
Generates a form for activating a customer account on the activate_account.liquid template.

Input
```
{% form 'activate_customer_password' %}
...
{% endform %}
```
Output
```
<form accept-charset="UTF-8" action="https://my-shop.myshopify.com/account/activate" method="post">
  <input name="form_type" type="hidden" value="activate_customer_password" />
  <input name="utf8" type="hidden" value="✓" />
  ...
</form>
```

### contact
Generates a form for submitting an email through the Liquid contact form.

Input
```
{% form 'contact' %}
...
{% endform %}
```

Output
```
<form accept-charset="UTF-8" action="/contact" class="contact-form" method="post">
  <input name="form_type" type="hidden" value="contact" />
  <input name="utf8" type="hidden" value="✓" />
  ...
</form>
```

### customer
Generates a form for creating a new customer without registering a new account. This form is useful for collecting customer information when you don't want customers to log in to your store, such as building a list of emails from a newsletter signup.

To generate a form that registers a customer account, use the create_customer form.

Input
```
{% form 'customer' %}
...
{% endform %}
```
Output
```
<form method="post" action="/contact#contact_form" id="contact_form" class="contact-form" accept-charset="UTF-8">
  <input type="hidden" value="customer" name="form_type">
  <input type="hidden" name="utf8" value="✓">
  ...
</form>
```
### create_customer
Generates a form for creating a new customer account on the register.liquid template.

Input
```
{% form 'create_customer' %}
...
{% endform %}
```
Output
```
<form accept-charset="UTF-8" action="https://my-shop.myshopify.com/account" id="create_customer" method="post">
  <input name="form_type" type="hidden" value="create_customer" />
  <input name="utf8" type="hidden" value="✓" />
  ...
</form>
```

### customer_address
Generates a form for creating or editing customer account addresses on the addresses.liquid template. When creating a new address, include the parameter customer.new_address. When editing an existing address, include the parameter address.

Input
```
{% form 'customer_address', customer.new_address %}
...
{% endform %}
```
Output
```
<form accept-charset="UTF-8" action="/account/addresses/70359392" id="address_form_70359392" method="post">
  <input name="form_type" type="hidden" value="customer_address" />
  <input name="utf8" type="hidden" value="✓" />
  ...
</form>
```

### customer_login
Generates a form for logging into Customer Accounts on the login.liquid template.

Input
```
{% form 'customer_login' %}
...
{% endform %}
```
Output
```
<form accept-charset="UTF-8" action="https://my-shop.myshopify.com/account/login" id="customer_login" method="post">
  <input name="form_type" type="hidden" value="customer_login" />
  <input name="utf8" type="hidden" value="✓" />
  ...
</form>
```

### guest_login
Generates a form on the login.liquid template that directs customers back to their checkout session as a guest instead of logging in to an account.

Input
```
{% form 'guest_login' %}
...
{% endform %}
```
Output
```
<form method="post" action="https://my-shop.myshopify.com/account/login" id="customer_login_guest" accept-charset="UTF-8">
  <input type="hidden" value="guest_login" name="form_type">
  <input type="hidden" name="utf8" value="✓">
  ...
  <input type="hidden" name="guest" value="true">
  <input type="hidden" name="checkout_url" value="https://checkout.shopify.com/store-id/checkouts/session-id?step=contact_information">
</form>
```

### new_comment
Generates a form for creating a new comment in the article.liquid template. Requires the  article object as a parameter.

Input
```
{% form 'new_comment', article %}
...
{% endform %}
```
Output
```
<form accept-charset="UTF-8" action="/blogs/news/10582441-my-article/comments" class="comment-form" id="article-10582441-comment-form" method="post">
  <input name="form_type" type="hidden" value="new_comment" />
  <input name="utf8" type="hidden" value="✓" />
  ...
</form>
```

### product
Generates a form for adding a product variant to the cart. Requires a product object as a parameter.

Input
```
{% form "product", product %}
  ...
{% endform %}
```
Output
```
<form method="post" action="/cart/add" enctype="multipart/form-data">
  <input type="hidden" name="form_type" value="product">
  <input type="hidden" name="utf8" value="✓">
  ...
</form>
```
Note 
Read about building product templates for an example of using the product form type.

### recover_customer_password
Generates a form for recovering a lost password on the login.liquid template.

Input
```
{% form 'recover_customer_password' %}
...
{% endform %}
```
Output
```
<form accept-charset="UTF-8" action="/account/recover" method="post">
  <input name="form_type" type="hidden" value="recover_customer_password" />
  <input name="utf8" type="hidden" value="✓" />
  ...
</form>
```

### reset_customer_password
Generates a form on the customers/reset_password.liquid template for a customer to reset their password.

Input
```
{% form 'reset_customer_password' %}
...
{% endform %}
```
Output
```
<form method="post" action="https://my-shop.myshopify.com/account/account/reset" accept-charset="UTF-8">
  <input type="hidden" value="reset_customer_password" name="form_type" />
  <input name="utf8" type="hidden" value="✓" />
  ...
  <input type="hidden" name="token" value="408b680ac218a77d0802457f054260b7-1452875227">
  <input type="hidden" name="id" value="1080844568">
</form>
```

### storefront_password
Generates a form on the password.liquid template for entering a password-protected storefront.

Input
```
{% form 'storefront_password' %}
...
{% endform %}
```
Output
```
<form method="post" action="/password" id="login_form" class="storefront-password-form" accept-charset="UTF-8">
  <input type="hidden" value="storefront_password" name="form_type">
  <input type="hidden" name="utf8" value="✓">
  ...
</form>
```

### Modifying form attributes
When you create a <form> element, you can modify its default attributes, or add new attributes. You can do this by including the attribute that you want to add or modify to the form tag as a named parameter, and assigning a value.

Input
```
{% form "product", product, id: "newID", class: "custom-class", data-example: "100" %}
  ...
{% endform %}
```
Output
```
<form method="post" action="/cart/add" id="newID" class="custom-class" data-example="100" enctype="multipart/form-data">
  <input type="hidden" name="form_type" value="product">
  <input type="hidden" name="utf8" value="✓">
    ...
</form>
```
You can also use Liquid variables as parameters:

Input
```
{% capture 'form_id' %}addToCartForm-{{ section.id }}{% endcapture %}

{% form 'product', product, id:form_id %}
...
{% endform %}
```
Output
```
<form action="/cart/add" method="post" enctype="multipart/form-data" id="addToCartForm-36197306239">
  <input type="hidden" name="form_type" value="product">
  <input type="hidden" name="utf8" value="✓">
    ...
</form>
```

## layout
Include {% layout 'alternate' %} at the beginning of a template file to use an alternate layout file from the Layout folder of your theme. If you don't define an alternate layout, the theme.liquid template file is used by default:

Load the layout/full-width.liquid template
```
{% layout 'full-width' %}
```
If you want a template to use no layout file, you can specify none as the layout:

Render the template file without using a layout
```
{% layout none %}
```

## paginate
Splitting products, blog articles, and search results across multiple pages is a necessary part of theme design as you are limited to 50 results per page in any for loop.

The paginate tag works with thefor tag to split content into many pages. It must wrap a for tag block that loops through an array, as shown in the example below:

```
{% paginate collection.products by 5 %}
  {% for product in collection.products %}
    <!--show product details here -->
  {% endfor %}
{% endpaginate %}
```

The by parameter is followed by an integer between 1 and 50 that tells the paginate tag how many results it should output per page.

Within paginate tags, you can access attributes of the paginate object. This includes the attributes to output the links required to navigate within the generated pages.

## raw
Allows output of Liquid code on a page without being parsed.

Input
```
{% raw %}{{ 5 | plus: 6 }}{% endraw %} equals 11.
```

Output
```
{{ 5 | plus: 6 }} equals 11.
```

## section
Inserts a section from the sections folder of a theme.

Input
```
{% section 'header' %}
```
Output
```
<div id="shopify-section-header" class="shopify-section">
  <!-- content of sections/header.liquid -->
</div>
```
Including section files with the {% section %} tag will render a "static" section. To learn more about sections and how to include them in your theme, check out the documentation on theme sections.

Each section supports section-specific tags for defining settings, styles, and scripts that are unique to a section file.