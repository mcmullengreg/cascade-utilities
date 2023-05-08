+++
title = "Do Shortcode"
description = ""
weight = 1000
+++

{{<lead>}}
`do_shortcode` is the most basic macro within the entire set. While there are ways to enhance this functionality, the below
sample will get you started.
{{</lead>}}

{{<code lang="java">}}
#*
  * Macro do_shortcode ( $shortcodeName, $content )
  * Processes the actual shortcode, and attaches the macro to it
*#
#macro ( do_shortcode $shortcodeName, $content )
    #if ( $shortcodeName.contains("shortcodeName") )
      #shortcode($content)
    ## This entry is an example, and should never be uncommented
    ##elseif ( $shortcodeName.contains("_template") )
      ##_template($content)
    #else
        #set ( $wysiwyg = $content )
        ## I'm the else...I run if no shortcodes exist.
    #end
#end
{{</code>}}
