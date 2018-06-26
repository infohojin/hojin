# Section tags

Section tags are used for providing settings, styles, and scripts that are unique to a section file. These tags can only be used in section files.

In this article
* javascript
* schema
* stylesheet

## javascript
Wraps scripts in a self-executing anonymous function and places them in a single file loaded in content_for_header. The scripts are only executed when the section is rendered on the page.

## schema
The schema tag is used in section files to define the settings and properties of that section.
```
{% schema %}
  {
    "name": "Header",
    "settings": [
      {
        "type": "image_picker",
        "id": "logo",
        "label": "Logo image"
      }
    ]
  }
{% endschema %}
```
The schema tags must contain valid JSON and cannot be nested inside another theme tag. Read more about building schema in the section schema documentation.

## stylesheet
Concatenates styles into a single stylesheet loaded in content_for_header.

### stylesheet tag parameters
#### scss
Allows Sass support for styles within the stylesheet tag.

Input
```
{% stylesheet 'scss' %}
  $brandColor: #7ab55c;

  .cta__heading {
    font-size: 2.25em;
    color: $brandColor;
  }
{% endstylesheet %}
```

Output
```
.cta__heading{font-size:2.25em;color:#7ab55c}
```