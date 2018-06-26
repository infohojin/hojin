# Iteration tags
Iteration tags repeatedly run blocks of code.

In this article
* for
* cycle
* tablerow

## for
Repeatedly executes a block of code. For a full list of attributes available within a for loop, see forloop (object).

for loops can output a maximum of 50 results per page. In cases where there are more than 50 results, use the paginate tag to split them across multiple pages.

Input
```
{% for product in collection.products %}
  {{ product.title }}
{% endfor %}
```
Output
```
Fancy hat Snazzy shirt Dapper pants
```

## else
Specifies a fallback case for a for loop which will run if the loop has zero length (for example, you loop over a collection that has no products):

Input
```
{% for product in collection.products %}
  {{ product.title }}
{% else %}
  The collection is empty.
{% endfor %}
```
Output
```
The collection is empty.
```

## break
Causes the loop to stop iterating when it encounters the break tag.

Input
```
{% for i in (1..5) %}
  {% if i == 4 %}
    {% break %}
  {% else %}
    {{ i }}
  {% endif %}
{% endfor %}
```
Output
```
1 2 3
```

## continue
Causes the loop to skip the current iteration when it encounters the continue tag.

Input
```
{% for i in (1..5) %}
  {% if i == 4 %}
    {% continue %}
  {% else %}
    {{ i }}
  {% endif %}
{% endfor %}
```
Output
```
1 2 3   5
```

## for tag parameters
limit
Exits the for loop at a specific index.

Input
```
  <!-- numbers = [1,2,3,4,5] -->

  {% for item in numbers limit:2 %}
    {{ item }}
  {% endfor %}
```
Output
```
1 2
```

## offset
Starts the for loop at a specific index.

Input
```
  <!-- numbers = [1,2,3,4,5] -->
  {% for item in numbers offset:2 %}
    {{ item }}
  {% endfor %}
```
Output
```
3 4 5 6
```

## range
Defines a range of numbers to loop through. You can define the range using both literal and variable values.

Input
```
{% for i in (3..5) %}
  {{ i }}
{% endfor %}

{% assign my_limit = 4 %}
{% for i in (1..my_limit) %}
{{ i }}
{% endfor %}
```
Output
```
3 4 5

1 2 3 4
```

## reversed
Reverses the order of the loop.

Input
```
<!-- if array = [1,2,3,4,5,6] -->
{% for item in array reversed %}
  {{ item }}
{% endfor %}
```
Output
```
6 5 4 3 2 1
```

## cycle
Loops through a group of strings and outputs them in the order that they were passed as parameters. Each time cycle is called, the next string that was passed as a parameter is output.

cycle must be used within a for loop block.

Input
```
{% cycle 'one', 'two', 'three' %}
{% cycle 'one', 'two', 'three' %}
{% cycle 'one', 'two', 'three' %}
{% cycle 'one', 'two', 'three' %}
```
Output
```
one
two
three
one
```
Uses for cycle include:

* applying odd/even classes to rows in a table
* applying a unique class to the last product thumbnail in a row


## cycle tag parameters
cycle accepts a parameter called cycle group in cases where you need multiple cycle blocks in one template. If no name is supplied for the cycle group, then it is assumed that multiple calls with the same parameters are one group.

The example below shows why cycle groups are necessary when there are multiple instances of the cycle block.
```
<ul>
  {% for product in collections.collection-1.products %}
    <li{% cycle ' style="clear:both;"', '', '', ' class="last"' %}>
      <a href="{{ product.url | within: collection }}">
        <img src="{{ product.featured_image.src | img_url: '240x' }}" alt="{{ product.featured_image.alt }}" />
      </a>
    </li>
  {% endfor %}
</ul>

<ul>
  {% for product in collections.collection-2.products %}
    <li{% cycle ' style="clear:both;"', '', '', ' class="last"' %}>
      <a href="{{ product.url | within: collection }}">
        <img src="{{ product.featured_image.src | img_url: '240x' }}" alt="{{ product.featured_image.alt }}" />
      </a>
    </li>
  {% endfor %}
</ul>
```
In the example above, if the first collection only has two products, the second collection loop will continue the cycle where the first one left off. This will result in this undesired output:

```
<ul>
  <li style="clear:both"></li>
</ul>

<ul>
  <li></li>
  <li class="last"></li>
  <li style="clear:both"></li>
  <li></li>
</ul>
```
To avoid this, you can use a cycle group for each cycle block, as shown below:

```
<ul>
{% for product in collections.collection-1.products %}
  <li{% cycle 'group1': ' style="clear:both;"', '', '', ' class="last"' %}>
    <a href="{{ product.url | within: collection }}">
      <img src="{{ product.featured_image.src | img_url: '240x' }}" alt="{{ product.featured_image.alt }}" />
    </a>
  </li>
{% endfor %}
</ul>

<ul>
{% for product in collections.collection-2.products %}
  <li{% cycle 'group2': ' style="clear:both;"', '', '', ' class="last"' %}>
    <a href="{{ product.url | within: collection }}">
      <img src="{{ product.featured_image.src | img_url: '240x' }}" alt="{{ product.featured_image.alt }}" />
    </a>
  </li>
{% endfor %}
</ul>
```

With the code above, the two cycle blocks are independent of each other. The result is shown below:

```
<ul>
  <li style="clear:both"></li>
  <li></li>
</ul>
<!-- new cycle group starts! -->
<ul>
  <li style="clear:both"></li>
  <li></li>
  <li></li>
  <li class="last"></li>
</ul>
```

## tablerow
Generates rows for an HTML table. Must be wrapped in an opening <table> and closing  </table> HTML tags. For a full list of attributes available within a tablerow loop, see tablerow (object).

Input
```
<table>
  {% tablerow product in collection.products %}
    {{ product.title }}
  {% endtablerow %}
</table>
```
Output
```
<table>
  <tr class="row1">
    <td class="col1">
      Cool Shirt
    </td>
    <td class="col2">
      Alien Poster
    </td>
    <td class="col3">
      Batman Poster
    </td>
    <td class="col4">
      Bullseye Shirt
    </td>
    <td class="col5">
      Another Classic Vinyl
    </td>
    <td class="col6">
      Awesome Jeans
    </td>
  </tr>
</table>
```

## tablerow tag parameters
### cols
Defines how many columns the tables should have.

Input
```
<table>
  {% tablerow product in collection.products cols:2 %}
    {{ product.title }}
  {% endtablerow %}
</table>
```
Output
```
<table>
  <tr class="row1">
    <td class="col1">
      Cool Shirt
    </td>
    <td class="col2">
      Alien Poster
    </td>
  </tr>
  <tr class="row2">
    <td class="col1">
      Batman Poster
    </td>
    <td class="col2">
      Bullseye Shirt
    </td>
  </tr>
  <tr class="row3">
    <td class="col1">
      Another Classic Vinyl
    </td>
    <td class="col2">
      Awesome Jeans
    </td>
  </tr>
</table>
```
### limit
Exits the tablerow loop after a specific index.
```
{% tablerow product in collection.products cols:2 limit:3 %}
  {{ product.title }}
{% endtablerow %}
```

### offset
Starts the tablerow loop at a specific index.
```
{% tablerow product in collection.products cols:2 offset:3 %}
  {{ product.title }}
{% endtablerow %}
```
### range
Defines a range of numbers to loop through. The range can be defined by both literal and variable numbers.
```
<table>
  {% tablerow i in (3..5) %}
    {{ i }}
  {% endtablerow %}
</table>

{% assign num = 4 %}
<table>
  {% tablerow i in (1..num) %}
    {{ i }}
  {% endtablerow %}
</table>
```


