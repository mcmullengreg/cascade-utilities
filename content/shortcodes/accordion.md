+++
title = "Accordion"
description = ""
+++

{{<lead>}}
`accordionsc` allows for accordion content to be dropped onto a page, without the need for a full data definition.
{{</lead>}}

<h2>Basic Usage</h2>

You will need to create an accordion block using Add Content > Blocks/Accordion. After which you will drop the following into the WYSIWYG editor.

{{<code lang="html">}}
<p>[accodionsc path="/_blocks/path-to-accordion"]</p>
{{</code>}}

Shortcodes require a paragraph tag to work successfully, so if this is the only item on the page, hit Enter to make sure you have a `p` on the page prior to using the shortcode itself.

The Cascade editor should show the p at the bottom of the editor window to indicate whether or not it is wrapped.
