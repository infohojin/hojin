# Math filters
Math filters allow you to apply mathematical tasks.

Math filters can be linked and, as with any other filters, are applied in order of left to right. In the example below, minus is applied first, then times, and finally divided_by.

You save {{ product.compare_at_price | minus: product.price | times: 100.0 | divided_by: product.compare_at_price }}%
In this article
abs
at_most
at_least
ceil
divided_by
floor
minus
plus
round
times
modulo
abs
Returns the absolute value of a number.

Input


{{ -17 | abs }}

Output

17
abs will also work on a string if the string only contains a number.

Input


{{ "-19.86" | abs }}

Output

19.86
at_most
Limits a number to a maximum value.

Input

{{ 4 | at_most: 5 }}
{{ 4 | at_most: 3 }}
Output

4
3
at_least
Limits a number to a minimum value.

Input

{{ 4 | at_least: 5 }}
{{ 4 | at_least: 3 }}
Output

5
4
ceil
Rounds an output up to the nearest integer.

Input

{{ 4.6 | ceil }}
{{ 4.3 | ceil }}
Output

5
5
divided_by
Divides an output by a number. The output is rounded down to the nearest integer.

Input

<!-- product.price = 200 -->
{{ product.price | divided_by: 10 }}
Output

20
floor
Rounds an output down to the nearest integer.

Input

{{ 4.6 | floor }}
{{ 4.3 | floor }}
Output

4
4
minus
Subtracts a number from an output.

Input

<!-- product.price = 200 -->
{{ product.price | minus: 15 }}
Output

185
plus
Adds a number to an output.

Input

<!-- product.price = 200 -->
{{ product.price | plus: 15 }}
Output

215
round
Rounds the output to the nearest integer or specified number of decimals.

Input

{{ 4.6 | round }}
{{ 4.3 | round }}
{{ 4.5612 | round: 2 }}
Output

5
4
4.56
times
Multiplies an output by a number.

Input

<!-- product.price = 200 -->
{{ product.price | times: 1.15 }}
Output

230
modulo
Divides an output by a number and returns the remainder.

Input

{{ 12 | modulo:5 }}
Output

2