# HTML filters
HTML filters wrap assets in HTML tags.

In this article
* img_tag
* script_tag
* stylesheet_tag

## img_tag
Generates an image tag.

Input
```
{{ 'smirking_gnome.gif' | asset_url | img_tag }}
```
Output
```
<img src="//cdn.shopify.com/s/files/1/0147/8382/t/15/assets/smirking_gnome.gif?v=1384022871" alt="" />
```
The img_tag filter accepts parameters to output an alt tag, class names, and a size parameter:

The first parameter is output as the alt text.
The second parameter is the css class, or classes to be applied to the tag.
The last parameter is the image size parameter.

Note
The image size parameter is the same one used in the img_url filter, which is a URL Filter. This cannot be used in conjunction with the img_url filter. If both filters are used, the img_url filter will override the size parameter of the img_tag filter.

Input
```
{{ 'smirking_gnome.gif' | asset_url | img_tag: 'Smirking Gnome', 'cssclass1 cssclass2' }}
```
Output
```
<img src="//cdn.shopify.com/s/files/1/0147/8382/t/15/assets/smirking_gnome.gif?v=1384022871" alt="Smirking Gnome" class="cssclass1 cssclass2" />
```
The img_tag filter can also be used on the following objects:

* product
* variant
* line item
* collection
* image

Input
```
{{ product | img_tag }}
{{ variant | img_tag: 'alternate text' }}
{{ line_item | img_tag: 'alternate text', 'css-class' }}
{{ image | img_tag: 'alternate text', 'css-class', 'small' }}
{{ collection | img_tag: 'alternate text', 'css-class', 'large' }}
```

Output
```
<img src="//cdn.shopify.com/s/files/1/0159/3350/products/red_shirt_small.jpg?v=1398706734" alt="Red Shirt Small" />
<img src="//cdn.shopify.com/s/files/1/0159/3350/products/red_shirt_small.jpg?v=1398706734" alt="alternate text" />
<img src="//cdn.shopify.com/s/files/1/0159/3350/products/red_shirt_small.jpg?v=1398706734" alt="alternate text" class="css-class" />
<img src="//cdn.shopify.com/s/files/1/0159/3350/products/red_shirt_small.jpg?v=1398706734" alt="alternate text" class="css-class" />
<img src="//cdn.shopify.com/s/files/1/0159/3350/products/shirts_collection_large.jpg?v=1338563745" alt="alternate text" class="css-class" />
```

## script_tag
Generates a script tag.

Input
```
{{ 'shop.js' | asset_url | script_tag }}
```
Output
```
<script src="//cdn.shopify.com/s/files/1/0087/0462/t/394/assets/shop.js?28178" type="text/javascript"></script>
```

## stylesheet_tag
Generates a stylesheet tag.

Input
```
{{ 'shop.css' | asset_url | stylesheet_tag }}
```
Output
```
<link href="//cdn.shopify.com/s/files/1/0087/0462/t/394/assets/shop.css?28178" rel="stylesheet" type="text/css" media="all" />
```