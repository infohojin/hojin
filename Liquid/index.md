# Luquid 소개
Liquid reference

https://help.shopify.com/themes/liquid

Also in this section
Liquid is a template language created by Shopify and written in Ruby. It is now available as an open source project on GitHub, and used by many different software projects and companies. Liquid is the backbone of all Shopify themes, and is used to load dynamic content to the pages of online stores.

In this article
What is a template language?
Liquid syntax
Accessing theme templates
Additional resources
What is a template language?
Website designers and developers can use a template language to build webpages that combine static content, which is the same on multiple pages, and dynamic content, which changes from one page to the next. A template language makes it possible to re-use the static elements that define the layout of a webpage, while dynamically populating the page with data from a Shopify store. The static elements are written in HTML, and the dynamic elements are written in Liquid. The Liquid elements in a file act as placeholders: when the code in the file is compiled and sent to the browser, the Liquid is replaced by data from the Shopify store where the theme is installed.

Liquid syntax
Like traditional programming languages, Liquid has a syntax, interacts with variables, and includes constructs such as output and logic. Due to its readable syntax, Liquid constructs are easy to recognize, and can be distinguished from HTML by two sets of delimiters: the double curly brace delimiters {{ }}, which denote output, and the curly brace percentage delimiters {% %}, which denote logic and control flow.

There are three main features of Liquid code:

Objects
Tags
Filters
Objects
Liquid objects output pieces of data from a Shopify admin. In a theme template, objects are wrapped in double curly brace delimiters {{ }}, and look like this:

{{ product.title }}
In the above example, product is the object, and title is a property of that object. Each object has a list of associated properties. To learn more about the product object's properties, see the Liquid reference.

The {{ product.title }} Liquid object can be found in the product template of a Shopify theme. When the code in the file is compiled and rendered on a product page of a Shopify store, the output of the Liquid object will be the title of the product. For example, in a clothing store, the result might be:

Awesome T-Shirt
Even though the same template is used for every product in a Shopify store, the Liquid objects in the template will output different data depending on the product page that you are viewing.

To learn more about the different Liquid objects that can be used in theme templates, see the Liquid objects page.

Tags
Liquid tags are used to create logic and control flow for templates. The curly brace percentage delimiters {% %} and the text that they surround do not produce any visible output when the webpage is rendered. This lets you assign variables and create conditions or loops without showing any of the Liquid logic on the page.

For example, you can use Liquid tags to display different content on the product page depending on whether or not a product is available:

{% if product.available %}
<h2>Price: $99.99</h2>
{% else %}
<h2 class="sold-out">Sorry, this product is sold out.</h2>
{% endif %}
If the product is available, then the output will be:

Price: $99.99
If the product is not available, then the output will be:

Sorry, this product is sold out.
The above example uses if and else Liquid tags, which are control flow tags.

Liquid tags are categorized into various types:

Control flow tags
Iteration tags
Section tags
Theme tags
Variable tags
Filters
Liquid filters are used to modify the output of numbers, strings, objects, and variables. They are placed within an output tag {{ }}, and are denoted by a pipe character |.

A simple example is the capitalize string filter:

{{ 'hello, world!' | capitalize }}
The filter modifies the string by capitalizing it. The output will be:

Hello, world!
Multiple filters can be used on one output, and they are applied from left to right:

{{ 'hello, world!' | capitalize | remove: "world" }}
The string is first capitalized, and then the word world is removed. The output will be:

Hello, !
You can use Liquid filters to make a wide variety of useful data manipulations. They are categorized into 8 types:

Array filters
Color filters
HTML filters
Math filters
Money filters
String filters
URL filters
Additional filters