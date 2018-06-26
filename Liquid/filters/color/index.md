# Color filters
Color filters change or extract properties from CSS color strings. These filters are commonly used with color theme settings.

In this article
* color_to_rgb
* color_to_hsl
* color_to_hex
* color_extract
* color_brightness
* color_modify
* color_lighten
* color_darken
* color_saturate
* color_desaturate
* color_mix
* color_contrast
* color_difference
* brightness_difference

## color_to_rgb
Converts a CSS color string to CSS rgb() format.

Input
```
{{ '#7ab55c' | color_to_rgb }}
```
Output
```
rgb(122, 181, 92)
```

If the input color has an alpha component, then the output will be in CSS rgba() format.
```
{{ 'hsla(100, 38%, 54%, 0.5)' | color_to_rgb }}
```
Output
```
rgba(122, 181, 92, 0.5)
```

## color_to_hsl
Converts a CSS color string to CSS hsl() format.

Input
```
{{ '#7ab55c' | color_to_hsl }}
```
Output
```
hsl(100, 38%, 54%)
```

If the input color has an alpha component, then the output will be in CSS rgba() format.
```
{{ 'rgba(122, 181, 92, 0.5)' | color_to_hsl }}
```

Output
```
hsla(100, 38%, 54%, 0.5)
```
## color_to_hex
Converts a CSS color string to hex6 format.

Input
```
{{ 'rgb(122, 181, 92)' | color_to_hex }}
```
Output
```
#7ab55c
```
Hex output is always in hex6 format. If there is an alpha channel in the input color, it will not appear in the output.
```
{{ 'rgba(122, 181, 92, 0.5)' | color_to_hex }}
```
Output
```
#7ab55c
```

## color_extract
Extracts a component from the color. Valid components are alpha, red, green, blue, hue, saturation and lightness.

Input
```
{{ '#7ab55c' | color_extract: 'red' }}
```
Output
```
122
```

## color_brightness
Calculates the perceived brightness of the given color. Uses W3C recommendations for calculating perceived brightness, for the purpose of ensuring adequate contrast.

Input
```
{{ '#7ab55c' | color_brightness }}
```

Output
```
153.21
```

## color_modify
Modifies the given component of a color.

Red, green and blue values should be a number between 0 and 255
Alpha should be a decimal number between 0 and 1
Hue should be between 0 and 360 degrees
Saturation and lightness should be a value between 0 and 100 percent.
Input 
```
{{ '#7ab55c' | color_modify: 'red', 255 }}
```
Output 
```
#ffb55c
```
The filter will return a color type that includes the modified format — for example, if you modify the alpha channel, the filter will return the color in rgba() format, even if your input color was in hex format.

Input
```
{{ '#7ab55c' | color_modify: 'alpha', 0.85 }}
```
Output
```
rgba(122, 181, 92, 0.85)
```

## color_lighten
Lightens the input color. Takes a value between 0 and 100 percent.

Input 
```
{{ '#7ab55c' | color_lighten: 30 }}
```
Output 
```
#d0e5c5
```

## color_darken
Darkens the input color. Takes a value between 0 and 100 percent.

Input 
```
{{ '#7ab55c' | color_darken: 30 }}
```
Output 
```
#355325
```
## color_saturate
Saturates the input color. Takes a value between 0 and 100 percent.

Input 
```
{{ '#7ab55c' | color_saturate: 30 }}
```
Output 
```
#6ed938
```

## color_desaturate
Desaturates the input color. Takes a value between 0 and 100 percent.

Input 
```
{{ '#7ab55c' | color_desaturate: 30 }}
```
Output 
```
#869180
```

## color_mix
Blends together two colors. Blend factor should be a value value between 0 and 100 percent.

Input  
```
{{ '#7ab55c' | color_mix: '#ffc0cb', 50 }}
```
Output 
```
#bdbb94
```
If one input has an alpha component, but the other does not, an alpha component of 1 will be assumed for the input without an alpha component.

Input  
```
{{ 'rgba(122, 181, 92, 0.75)' | color_mix: '#ffc0cb', 50 }}
```
Output 
```
rgba(189, 187, 148, 0.875)
```

## color_contrast
Calculates the contrast ratio between two colors. Returns the numerator part of the ratio, which has a denominator of 1. For example, for a contrast ratio of 3.5:1, the filter returns 3.5.

With regards to accessibility, WCAG 2.0 level AA requires a contrast ratio of at least 4.5:1 for normal text and 3:1 for large text. Level AAA requires a contrast ratio of at least 7:1 for normal text and 4.5:1 for large text.

The order in which you specify the colors does not matter. The filter will automatically detect the lighter and darker colors.

Input  
```
{{ '#495859' | color_contrast: '#fffffb' }}
```
Output
```
7.4
```

## color_difference
Calculates the color difference or distance between two colors. With regards to accessibility, the W3C suggests that the color difference should be greater than 500.

Input  
```
{{ '#ff0000' | color_difference: '#abcdef' }}
```
Output
```
528
```

## brightness_difference
Calculates the perceived brightness difference between two colors. With regards to accessibility, the W3C suggests that the brightness difference should be greater than 125.

Input  
```
{{ '#fff00f' | brightness_difference: '#0b72ab' }}
```
Output
```
129
```