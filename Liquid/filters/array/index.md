# Array filters
Array filters change the output of arrays.

In this article
* join
* first
* last
* concat
* index
* map
* reverse
* size
* sort
* uniq

## join
Joins the elements of an array with the character passed as the parameter. The result is a single string.

Input
```
{{ product.tags | join: ', ' }}
```
Output
```
tag1, tag2, tag3
```

## first
Returns the first element of an array.

Input
```
<!-- product.tags = "sale", "mens", "womens", "awesome" -->
{{ product.tags | first }}
```
Output
```
sale
```
You can use first with dot notation when you need to use the filter inside a tag.
```
{% if product.tags.first == "sale" %}
  This product is on sale!
{% endif %}
```

## last
Returns the last element of an array.

Input
```
<!-- product.tags = "sale", "mens", "womens", "awesome" -->
{{ product.tags | last }}
```
Output
```
awesome
```

You can use last with dot notation when you need to use the filter inside a tag.
```
{% if product.tags.last == "sale"%}
  This product is on sale!
{% endif %}
```
Using last on a string returns the last character in the string.

Input
```
<!-- product.title = "Awesome Shoes" -->
{{ product.title | last }}
```
Output
```
s
```

## concat
Concatenates (combines) an array with another array. The resulting array contains all the elements of the original arrays. concat will not remove duplicate entries from the concatenated array unless you also use the uniq filter.

Input
```
{% assign fruits = "apples, oranges, peaches, tomatoes" | split: ", " %}
{% assign vegetables = "broccoli, carrots, lettuce, tomatoes" | split: ", " %}

{% assign plants = fruits | concat: vegetables %}

{{ plants | join: ", " }}
```

Output
```
apples, oranges, peaches, tomatoes, broccoli, carrots, lettuce, tomatoes
```
You can string together multiple concat filters to combine more than two arrays:

Input
```
{% assign fruits = "apples, oranges, peaches" | split: ", " %}
{% assign vegetables = "broccoli, carrots, lettuce" | split: ", " %}
{% assign animals = "dogs, cats, birds" | split: ", " %}

{% assign things = fruits | concat: vegetables | concat: animals %}

{{ things | join: ", " }}
```
Output
```
apples, oranges, peaches, broccoli, carrots, lettuce, dogs, cats, birds
```

## index
Returns the item at the specified index location in an array. Note that array numbering starts from zero, so the first item in an array is referenced with [0].

Input
```
<!-- product.tags = "sale", "mens", "womens", "awesome" -->
{{ product.tags[2] }}
```
Output
```
womens
```

## map
Accepts an array element's attribute as a parameter and creates an array out of each array element's value.

Input
```
<!-- collection.title = "Spring", "Summer", "Fall", "Winter" -->
{% assign collection_titles = collections | map: 'title' %}
{{ collection_titles }}
```

Output
```
SpringSummerFallWinter
```

### reverse
Reverses the order of the items in an array.

Input
```
{% assign my_array = "apples, oranges, peaches, plums" | split: ", " %}

{{ my_array | reverse | join: ", " }}
```
Output
```
plums, peaches, oranges, apples
```

## size
Returns the size of a string (the number of characters) or an array (the number of elements).

Input
```
{{ 'The quick brown fox jumps over a lazy dog.' | size }}
```
Output
```
42
```
You can use size with dot notation when you need to use the filter inside a tag.
```
{% if collections.frontpage.products.size > 10 %}
  There are more than 10 products in this collection!
{% endif %}
```

## sort
Sorts the elements of an array by a given attribute of an element in the array.
```
{% assign products = collection.products | sort: 'price' %}
{% for product in products %}
  <h4>{{ product.title }}</h4>
{% endfor %}
```
The order of the sorted array is case-sensitive.

Input
```
<!-- products = "a", "b", "A", "B" -->
{% assign products = collection.products | sort: 'title' %}
{% for product in products %}
   {{ product.title }}
{% endfor %}
```
Output
```
A B a b
```

## uniq
Removes any duplicate instances of elements in an array.

Input
```
{% assign fruits = "orange apple banana apple orange" %}
{{ fruits | split: ' ' | uniq | join: ' ' }}
```
Output
```
orange apple banana
```