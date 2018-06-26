# Additional filters
General filters serve many different purposes including formatting, converting, and applying CSS classes.

In this article
* date
* time_tag
* default
* default_errors
* default_pagination
* format_address
* highlight
* highlight_active_tag
* json
* weight_with_unit
* placeholder_svg_tag

## date
Converts a timestamp into another date format.

Input
```
{{ article.published_at | date: "%a, %b %d, %y" }}
```
Output
```
Tue, Apr 22, 14
```
date accepts the same parameters as Ruby's strftime method. You can find a list of the shorthand formats in Ruby's documentation or use a site like strfti.me.

## time_tag
The time_tag filter converts a timestamp into an HTML <time> tag:

Input
```
{{ article.published_at | time_tag }}
```
Output
```
<time datetime="2016-02-24T14:47:51Z">Wed, 24 Feb 2016 09:47:51 -0500</time>
```
To customize the time output, you can pass date parameters to the time_tag filter. This doesn't affect the value of the datetime attribute set in the <time> tag:

Input
```
{{ article.published_at | time_tag: '%b %d, %Y' }}
```
Output
```
<time datetime="2016-02-24T14:47:51Z">Feb 24, 2016</time>
```

### Custom datetime
You can pass a datetime parameter with date parameters to use a custom format for the datetime attribute of the output time tag:

Input
```
{{ article.published_at | time_tag: datetime: '%b %d, %Y' }}
```
Output
```
<time datetime="Feb 24, 2016">Wed, 24 Feb 2016 09:47:51 -0500</time>
```

### Localized date format
You can pass a format parameter to the filter to use a date format defined in your theme's locale settings:

In theme / locales / en.json
```
"date_formats": {
  "month_day_year": "%B %d, %Y"
}
```

Input
```
{{ article.published_at | time_tag: format: 'month_day_year' }}
```

Output
```
<time datetime="2016-02-24T14:47:51Z">February 24, 2016</time>
```

## default
Sets a default value for any variable with no assigned value. Can be used with strings, arrays, and hashes.

The default value is returned if the variable resolves to nil or an empty string "". A string containing whitespace characters will not resolve to the default value.

Input
```
Dear {{ customer.name | default: "customer" }}
```

Output
```
<!-- If customer.name is nil -->
Dear customer

<!-- If customer.name is "" -->
Dear customer

<!-- If customer.name is "   " -->
Dear
```

## default_errors
Outputs default error messages for the form.errors variable. The messages returned are dependent on the strings returned by form.errors.

Input
```
{% if form.errors %}
      {{ form.errors | default_errors }}
{% endif %}
```

Output
```
<!-- if form.errors returned "email" -->

Please enter a valid email address.
```

## default_pagination
Creates a set of links for paginated results. Used in conjunction with the paginate variable.

Input
```
{{ paginate | default_pagination }}
```
Output
```
<span class="page current">1</span>
<span class="page"><a href="/collections/all?page=2" title="">2</a></span>
<span class="page"><a href="/collections/all?page=3" title="">3</a></span>
<span class="deco">…</span>
<span class="page"><a href="/collections/all?page=17" title="">10</a></span>
<span class="next"><a href="/collections/all?page=2" title="">Next »</a></span>
```
Default pagination uses the labels Next » and « Previous for links to the next and previous pages. You can override these labels by passing new words to the default_pagination filter:

Input
```
{{ paginate | default_pagination: next: 'Older', previous: 'Newer' }}
```
Output
```
<span class="page current">1</span>
<span class="page"><a href="/collections/all?page=2" title="">2</a></span>
<span class="page"><a href="/collections/all?page=3" title="">3</a></span>
<span class="next"><a href="/collections/all?page=2" title="">Older</a></span>
```

## format_address
Use the format_address filter on an address to print the elements of the address in order according to their locale. The filter will only print the parts of the address that have been provided. This filter works on the addresses page for customers who have accounts in your store, or on your store's address:

Input
```
{{ address | format_address }}
```

Output
```
<p>
  Elizabeth Gonzalez<br>
  1507 Wayside Lane<br>
  San Francisco<br>
  CA<br>
  94103<br>
  United States
</p>
```

Input
```
{{ address | format_address }}
```

Output
```
<p>
  Feng Sun<br>
  No. 2094, 1006, Hui Dong Xin Cun<br>
  Nanhui District<br>
  201300, Shanghai<br>
  China
</p>
```

## highlight
Wraps words inside search results with an HTML <strong> tag with the class highlight if it matches the submitted search.terms.

Input
```
{{ item.content | highlight: search.terms }}
```
Output
```
<!-- If the search term was "Yellow" -->
<strong class="highlight">Yellow</strong> shirts are the best!
```

## highlight_active_tag
Wraps a tag link in a <span> with the class active if that tag is being used to filter a collection.

Input
```
<!-- collection.tags = ["Cotton", "Crew Neck", "Jersey"] -->
{% for tag in collection.tags %}
    {{ tag | highlight_active | link_to_tag: tag }}
{% endfor %}
```
Output
```
<a title="Show products matching tag Cotton" href="/collections/all/cotton"><span class="active">Cotton</span></a>
<a title="Show products matching tag Crew Neck" href="/collections/all/crew-neck">Crew Neck</a>
<a title="Show products matching tag Jersey" href="/collections/all/jersey">Jersey</a>
```

## json
Converts a string into JSON format.

Input
```
var content = {{ pages.page-handle.content | json }};
```

Output
```
var content = "\u003Cp\u003E\u003Cstrong\u003EYou made it! Congratulations on starting your own e-commerce store!\u003C/strong\u003E\u003C/p\u003E\n\u003Cp\u003EThis is your shop\u0026#8217;s \u003Cstrong\u003Efrontpage\u003C/strong\u003E, and it\u0026#8217;s the first thing your customers will see when they arrive. You\u0026#8217;ll be able to organize and style this page however you like.\u003C/p\u003E\n\u003Cp\u003E\u003Cstrong\u003ETo get started adding products to your shop, head over to the \u003Ca href=\"/admin\"\u003EAdmin Area\u003C/a\u003E.\u003C/strong\u003E\u003C/p\u003E\n\u003Cp\u003EEnjoy the software,  \u003Cbr /\u003E\nYour Shopify Team.\u003C/p\u003E";
```

Tip 
You do not have to wrap the Liquid output in quotations - the json filter will add them in. The json filter will also escape quotes as needed inside the output.

The json filter can also used to make Liquid objects readable by JavaScript:
```
var json_product = {{ collections.featured.products.first | json }};
var json_cart = {{ cart | json }};
```

### Product inventory and the JSON filter
The JSON filter doesn't output values for the inventory_quantity and inventory_policy fields for any Shopify stores created after December 5, 2017. These fields are deprecated to help eliminate bots and crawlers from retrieving inventory quantities for stores to which they aren't granted access.

Instead of using the JSON filter, you can use variant.inventory_quantity and variant.inventory_policy to access inventory information.

### weight_with_unit
Formats the product variant's weight. The weight unit is set in General settings.

Input
```
{{ product.variants.first.weight | weight_with_unit }}
```

Output
```
24.0 kg
```
The unit can be overridden by passing it into the filter. This is useful in the case of product variants which can each have their own unit.

Input
```
{{ variant.weight | weight_with_unit: variant.weight_unit }}
```

Output
```
52.9 lb
```

### placeholder_svg_tag
Takes a placeholder name and outputs a placeholder SVG illustration. An optional argument can be supplied to include a custom class attribute on the SVG tag.

Input
```
{{ 'collection-1' | placeholder_svg_tag }}
```
Output
```
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 525.5 525.5">...omitted for brevity...</svg>
```

## Custom class attribute
You can pass a class paramater to include a custom class attribute for the SVG tag:

Input
```
{{ 'collection-1' | placeholder_svg_tag: 'custom' }}
```
Output
```
<svg class="custom" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 525.5 525.5">...omitted for brevity...</svg>
```