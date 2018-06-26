# Variable tags
You can use variable tags to create new Liquid variables.

In this article
* assign
* capture
* increment
* decrement
* assign

Creates a new named variable.

Input
```
{% assign favorite_food = 'apples' %}

My favorite food is {{ favorite_food }}.
```
Output


```
My favorite food is apples.
```

assigned variables can be strings or booleans (true or false). Remember not to use quotation marks around the value if it is true or false:

Input
```
{% assign first_time_visitor = true %}
{% if first_time_visitor == true %}
  Welcome to the site!
{% endif %}
```
Output


```
  Welcome to the site!
```

## capture
Captures the string inside of the opening and closing tags and assigns it to a variable. Variables that you create using capture are stored as strings.

Using capture, you can create complex strings using other variables created with assign.

Input
```
{% assign favorite_food = 'pizza' %}
{% assign age = 35 %}

{% capture about_me %}
I am {{ age }} and my favorite food is {{ favorite_food }}.
{% endcapture %}

{{ about_me }}
```
Output
```
I am 35 and my favorite food is pizza.
```

## increment
Creates a new number variable, and increases its value by 1 every time increment is called on the variable. The counter's initial value is 0.

Here, an increment counter is used to create a unique numbered class for each list item:

Input
```
<ul>
  <li class="item-{% increment counter %}">apples</li>
  <li class="item-{% increment counter %}">oranges</li>
  <li class="item-{% increment counter %}">peaches</li>
  <li class="item-{% increment counter %}">plums</li>
</ul>
```
Output
```
<ul>
  <li class="item-0">apples</li>
  <li class="item-1">oranges</li>
  <li class="item-2">peaches</li>
  <li class="item-3">plums</li>
</ul>
```
Variables created using increment are separate from variables created using assign or capture.

In the example below, a variable named my_number is created using assign. The increment tag is then used several times on a variable with the same name. Note that the increment tag does not affect the value of my_number that was created through assign.

Input
```
{% assign my_number = 10 %}

{% increment my_number %}
{% increment my_number %}
{% increment my_number %}

{{ my_number }}
```
Output


```
0
1
2

10
```

## decrement
Creates a new number variable, and decreases its value by 1 every time decrement is called on the variable. The counter's initial value is -1.

Input
```
{% decrement variable %}
{% decrement variable %}
{% decrement variable %}
```
Output
```
-1
-2
-3
```
Like increment, variables declared using decrement are independent from variables created using assign or capture.