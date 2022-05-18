+++
title = "Shortcodes"
description = ""

+++

{{< lead >}}
Shortcodes within Cascade CMS function similarly to those found in WordPress. The biggest difference is when they render.

Cascade CMS shortcodes will not automatically trigger in the WYSIWYG editor, but will once the page has been submitted
from editing.
{{< /lead >}}

## How to use

Using a WYSIWYG editor, uses would type `[shortcode var="attribute"]`. Following the template as a guide you can then
process the WYSIWYG content to replace the shortcode with code that can use the variable. Such as:

```java
#macro ( shortcode $contentString )
  ...
  #set ( $attribute1 = #strByStartEnd($shortcode, 'var=", '"') )
  ## attribute1 would be 'attribute' set within the shortcode
  ...additional code...
#end
```

## Use Cases

- **YouTube embeds:** Instead of allowing users to embed content directly you can create a shortcode for how developers
  and brand ambassadors want these videos to be embedded on your site.
- **Form embeds:** Forms can be a nightmare, especially with Slate (for HighEdWebbers). Allow your users to only have to
  enter the form ID and you can handle the rest.
- **Other Applications:** Sometimes you just want to embed a Facebook post, Twitter feed or maybe process a CSV into
  an accessible table. This is what writing shortcodes can help with.

## Code samples
{{< childpages >}}
