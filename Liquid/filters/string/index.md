# String filters
String filters are used to manipulate outputs and variables of the string type.

In this article
append
camelcase
capitalize
downcase
escape
handle/handleize
md5
sha1
sha256
hmac_sha1
hmac_sha256
newline_to_br
pluralize
prepend
remove
remove_first
replace
replace_first
slice
split
strip
lstrip
rstrip
strip_html
strip_newlines
truncate
truncatewords
upcase
url_encode
url_escape
url_param_escape
Reversing strings

## append
Appends characters to a string.

Input
```
{{ 'sales' | append: '.jpg' }}
```
Output
```
sales.jpg
```

## camelcase
Converts a string into CamelCase.

Input
```
{{ 'coming-soon' | camelcase }}
```
Output
```
ComingSoon
```

## capitalize
Capitalizes the first word in a string

Input
```
{{ 'capitalize me' | capitalize }}
```

Output
```
Capitalize me
```

## downcase
Converts a string into lowercase.

Input

{{ 'UPPERCASE' | downcase }}
Output

## uppercase
escape
Escapes a string.

Input

{{ "<p>test</p>" | escape }}
Output
```
&lt;p&gt;test&lt;/p&gt;
 <!-- Note: a browser will visually display this as <p>test</p> -->
```

## handle/handleize
Formats a string into a handle.

Input

{{ '100% M & Ms!!!' | handleize }}
Output

100-m-ms

## md5
Converts a string into an MD5 hash.

An example use case for this filter is showing the Gravatar image associated with the poster of a blog comment:

Input

<img src="https://www.gravatar.com/avatar/{{ comment.email | remove: ' ' | strip_newlines | downcase | md5 }}" />
Output

<img src="https://www.gravatar.com/avatar/2a95ab7c950db9693c2ceb767784c201" />

## sha1
Converts a string into a SHA-1 hash.

Input

{% assign my_secret_string = "ShopifyIsAwesome!" | sha1 %}
My encoded string is: {{ my_secret_string }}
Output

My encoded string is: c7322e3812d3da7bc621300ca1797517c34f63b6

## sha256
Converts a string into a SHA-256 hash.

Input

{% assign my_secret_string = "ShopifyIsAwesome!" | sha256 %}
My encoded string is: {{ my_secret_string }}
Output

My encoded string is: c29cce758876791f34b8a1543f0ec3f8e886b5271004d473cfe75ac3148463cb
hmac_sha1
Converts a string into a SHA-1 hash using a hash message authentication code (HMAC). Pass the secret key for the message as a parameter to the filter.

Input

{% assign my_secret_string = "ShopifyIsAwesome!" | hmac_sha1: "secret_key" %}
My encoded string is: {{ my_secret_string }}
Output

My encoded string is: 30ab3459e46e7b209b45dba8378fcbba67297304
hmac_sha256
Converts a string into a SHA-256 hash using a hash message authentication code (HMAC). Pass the secret key for the message as a parameter to the filter.

Input

{% assign my_secret_string = "ShopifyIsAwesome!" | hmac_sha256: "secret_key" %}
My encoded string is: {{ my_secret_string }}
Output

My encoded string is: 30ab3459e46e7b209b45dba8378fcbba67297304
newline_to_br
Inserts a <br > linebreak HTML tag in front of each line break in a string.

Input

{% capture var %}
One
Two
Three
{% endcapture %}
{{ var | newline_to_br }}
Output

One <br>
Two<br>
Three<br>
pluralize
Outputs the singular or plural version of a string based on the value of a number. The first parameter is the singular string and the second parameter is the plural string.

Input

{{ cart.item_count }}
{{ cart.item_count | pluralize: 'item', 'items' }}
Output

3 items
prepend
Prepends characters to a string.

Input

{{ 'sale' | prepend: 'Made a great ' }}
Output

Made a great sale
remove
Removes all occurrences of a substring from a string.

Input

{{ "Hello, world. Goodbye, world." | remove: "world" }}
Output

Hello, . Goodbye, .
remove_first
Removes only the first occurrence of a substring from a string.

Input

{{ "Hello, world. Goodbye, world." | remove_first: "world" }}
Output

Hello, . Goodbye, world.
replace
Replaces all occurrences of a string with a substring.

Input

<!-- product.title = "Awesome Shoes" -->
{{ product.title | replace: 'Awesome', 'Mega' }}
Output

Mega Shoes
replace_first
Replaces the first occurrence of a string with a substring.

Input

<!-- product.title = "Awesome Awesome Shoes" -->
{{ product.title | replace_first: 'Awesome', 'Mega' }}
Output

Mega Awesome Shoes
slice
The slice filter returns a substring, starting at the specified index. An optional second parameter can be passed to specify the length of the substring. If no second parameter is given, a substring of one character will be returned.

Input

{{ "hello" | slice: 0 }}
{{ "hello" | slice: 1 }}
{{ "hello" | slice: 1, 3 }}
Output

h
e
ell
If the passed index is negative, it is counted from the end of the string.

Input

{{ "hello" | slice: -3, 2  }}
Output

ll
split
The split filter takes on a substring as a parameter. The substring is used as a delimiter to divide a string into an array. You can output different parts of an array using array filters.

Input

{% assign words = "Hi, how are you today?" | split: ' ' %}

{% for word in words %}
{{ word }}
{% endfor %}
Output

Hi,
how
are
you
today?
strip
Strips tabs, spaces, and newlines (all whitespace) from the left and right side of a string.

Input

{{ '   too many spaces      ' | strip }}
Output

too many spaces
lstrip
Strips tabs, spaces, and newlines (all whitespace) from the left side of a string.

Input

{{ '   too many spaces           ' | lstrip }}
Output

<!-- Highlight to see the empty spaces to the right of the string -->
too many spaces           
rstrip
Strips tabs, spaces, and newlines (all whitespace) from the right side of a string.

Input

{{ '              too many spaces      ' | rstrip }}
Output

<!-- Notice the empty spaces to the left of the string -->
              too many spaces
strip_html
Strips all HTML tags from a string.

Input

{{ "<h1>Hello</h1> World" | strip_html }}
Output

Hello World
strip_newlines
Removes any line breaks/newlines from a string.

{{ product.description | strip_newlines }}
truncate
Truncates a string down to the number of characters passed as the first parameter. An ellipsis (...) is appended to the truncated string and is included in the character count.

Input

{{ "The cat came back the very next day" | truncate: 13 }}
Output

The cat ca...
Custom ellipsis
truncate takes an optional second parameter that specifies the sequence of characters to be appended to the truncated string. By default this is an ellipsis (...), but you can specify a different sequence.

The length of the second parameter counts against the number of characters specified by the first parameter. For example, if you want to truncate a string to exactly 10 characters, and use a 3-character ellipsis, use 13 for the first parameter of truncate, since the ellipsis counts as 3 characters.

Input

{{ "ABCDEFGHIJKLMNOPQRSTUVWXYZ" | truncate: 18, ", and so on" }}
Output

ABCDEFG, and so on
No ellipsis
You can truncate to the exact number of characters specified by the first parameter and show no trailing characters by passing a blank string as the second parameter:

Input

{{ "I'm a little teapot, short and stout." | truncate: 15, "" }}
Output

I'm a little te
truncatewords
Truncates a string down to the number of words passed as the first parameter. An ellipsis (...) is appended to the truncated string.

Input

{{ "The cat came back the very next day" | truncatewords: 4 }}
Output

The cat came back...
Custom ellipsis
truncatewords takes an optional second parameter that specifies the sequence of characters to be appended to the truncated string. By default this is an ellipsis (...), but you can specify a different sequence.

Input

{{ "The cat came back the very next day" | truncatewords: 4, "--" }}
Output

The cat came back--
No ellipsis
You can avoid showing trailing characters by passing a blank string as the second parameter:

Input

{{ "The cat came back the very next day" | truncatewords: 4, "" }}
Output

The cat came back
upcase
Converts a string into uppercase.

Input

{{ 'i want this to be uppercase' | upcase }}
Output

I WANT THIS TO BE UPPERCASE
url_encode
Converts any URL-unsafe characters in a string into percent-encoded characters.

Input

{{ "john@liquid.com" | url_encode }}
Output

john%40liquid.com
Note that url_encode will turn a space into a + sign instead of a percent-encoded character.

Input

{{ "Tetsuro Takara" | url_encode }}
Output

Tetsuro+Takara
url_escape
Identifies all characters in a string that are not allowed in URLS, and replaces the characters with their escaped variants.

Input

{{ "<hello> & <shopify>" | url_escape }}
Output

%3Chello%3E%20&%20%3Cshopify%3E
url_param_escape
Replaces all characters in a string that are not allowed in URLs with their escaped variants, including the ampersand (&).

Input

{{ "<hello> & <shopify>" | url_param_escape }}
Output

%3Chello%3E%20%26%20%3Cshopify%3E
Reversing strings
reverse cannot be used directly on a string, but you can split a string into an array, reverse the array, and rejoin it by chaining together other filters:

Input

{{ "Ground control to Major Tom." | split: "" | reverse | join: "" }}
Output

.moT rojaM ot lortnoc dnuorG