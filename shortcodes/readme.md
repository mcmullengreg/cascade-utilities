# Shortcodes

This collection helps to integrate WordPress style shortcodes into the Cascade CMS. Shortcodes are quick
and easy ways for end users to be able to add functionality, without the need to understand all of the
code happening behind the scenes.

Editors will enter a shortcode, similar to: `[shortcode var="content"]` and while the code will be retained
this way in the WYSIWYG editor, the shortcode will render once the page has been submitted and/or published.

## Developing Shortcodes

Checkout the [template](https://github.com/mcmullengreg/cascade-utilities/tree/main/shortcodes/template.vm) for basic
documentation. Those standards should be followed to ensure accurate representation of your shortcode.

**Note:** Outputting content directly from your shortcode will result in the remaining content being rendered AFTER your
shortcode. To ensure in-place replacement, replace your shortcode with whatever variable is storing your "returned" string.

## Shortcode Example:

In content:
```html
<p>I am content</p>
<p>[shortcode variable="thing"]</p>
<p>I am additional content</p>
```

Small section of shortcode:
```java
#set ( $embedCode = "I make things happen!" )
#set ( $wysiwyg = $contentString.replace($fullShortCode, $embedCode) )
```

Rendered content:
```html
<p>I am content</p>
<p>I make things happen!</p>
<p>I am additional content</p>
```
