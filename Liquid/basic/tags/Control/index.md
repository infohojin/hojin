# Control flow tags
Control flow tags create conditions that decide whether blocks of Liquid code get executed.

In this article
* if
* unless
* else / elsif
* case / when
* Multiple conditions (and / or)

## if
Executes a block of code only if a certain condition is met (that is, if the result is true).

Input
```
{% if product.title == 'Awesome Shoes' %}
  You are buying some awesome shoes!
{% endif %}
```
Output
```
You are buying some awesome shoes!
```

## unless
Like if, but executes a block of code only if a certain condition is not met (that is, if the result is false).

Input
```
{% unless product.title == 'Awesome Shoes' %}
  You are not buying awesome shoes.
{% endunless %}
```
Output
```
You are not buying awesome shoes.
```

The above example is the same as:
```
{% if product.title != 'Awesome Shoes' %}
  You are not buying awesome shoes.
{% endif %}
```

## else / elsif
Adds more conditions to an if or unless block.

Input
```
{% if shipping_method.title == 'International Shipping' %}
  You're shipping internationally. Your order should arrive in 2–3 weeks.
{% elsif shipping_method.title == 'Domestic Shipping' %}
  Your order should arrive in 3–4 days.
{% else %}
  Thank you for your order!
{% endif %}
```
Output
```
Your order should arrive in 3–4 days.
```

## case / when
Creates a switch statement to execute a particular block of code when a variable has a specified value. case initializes the switch statement, and when statements define the various conditions.

You can optionally add an else statement at the end of the case to provide code to execute if none of the conditions are met.

Input
```
{% case shipping_method.title %}
  {% when 'International Shipping' %}
     You're shipping internationally. Your order should arrive in 2–3 weeks.
  {% when 'Domestic Shipping' %}
    Your order should arrive in 3–4 days.
  {% when 'Local Pick-Up' %}
    Your order will be ready for pick-up tomorrow.
  {% else %}
     Thank you for your order!
{% endcase %}
```
Output
```
Your order should arrive in 3–4 days.
```

## Multiple conditions (and / or)
You can use the and and or operators to include more than one condition in a control flow tag. and and or can be chained together to create complex conditionals.

If you use multiple and or or operators, note that and operators will be evaluated first, then or operators. You cannot use parentheses to simulate an order of operations and control the order of operator evaluation. Parentheses are invalid characters within Liquid tags and prevent your tags from working.

and
The and operator lets you add additional conditions to a tag. A condition with an and will only be true if both the left and the right side of the condition are true.

Input
```
{% if line_item.grams > 20000 and customer_address.city == 'Ottawa' %}
  You're buying a heavy item, and live in the same city as our store. Choose local pick-up as a shipping option to avoid paying high shipping costs.
{% endif %}
```
Output
```
You're buying a heavy item, and live in the same city as our store. Choose local pick-up as a shipping option to avoid paying high shipping costs.
```

## or
The or operator lets you add additional conditions to a tag. A condition with an or will be true if either the left or the right side of the condition is true.

Input
```
{% if customer.tags contains 'VIP' or customer.email contains 'mycompany.com' %}
  Welcome! We're pleased to offer you a special discount of 15% on all products.
{% else %}
  Welcome to our store!
{% endif %}
```
Output
```
Welcome! We're pleased to offer you a special discount of 15% on all products.
```