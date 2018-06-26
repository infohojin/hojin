# Liquid basics

Liquid uses a combination of tags, objects, and filters to load dynamic content. They are used inside Liquid template files, which are the files that make up a theme. For more information on the available templates, please see Building themes.

In this article
* Tags
* Objects
* Filters

## Tags
Tags make up the programming logic that tells templates what to do. 
Read more ›
```
{% if user.name == 'elvis' %}
  Hey Elvis
{% endif %}
```

## Objects
Objects contain attributes that are used to display dynamic content on a page.
Read more ›

```
{{ product.title }} <!-- Output: Awesome T-Shirt-->
```

## Filters
Filters are used to modify the output of strings, numbers, variables, and objects.
Read more ›

```
{{ 'sales' | append: '.jpg' }} <!-- Output: sales.jpg -->
```