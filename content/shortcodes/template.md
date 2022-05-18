+++
title = "Shortcode Template"
description = ""
+++

{{<lead>}}
This template file breaks down the basic code necessary for writing your first macro.
{{</lead>}}

{{<code lang="java">}}
#*
  This page serves as a template and guide to developing and/or editing new shortcodes
  Shortcodes should all be stored inside of the same site and folder, e.g. /macros/shortcodes/{name}.

  The shortcode, file and macro names should match exactly. The name is used as a check to:
  1. Import the macro file
  2. "Name" the macro itself
  3. Trigger a check for which macro to run (inside of do_shortcode)

  e.g. #macro form ; shortcode is [form id=""]; filename is form

  Basic structure:
    - Import the find_shortcode file, this allows you to search for a named shortcode.
    - Write your macro/shortcode
    - Use $contentString (or similar) to pass in the wysiwyg editor content. This is all that's needed to be passed in
    - Ensure you write out to $wysiwyg at the end of it all (setting the WYSIWYG editor to $wysiwyg, regardless of DD name or structured data is ideal)
    - Update do_shortcode with your new entry
*#

#macro ( _template $contentString )
  ## Gets the starting position of the shortcode
  ## Uses the curly brace, due to processing occurring higher in the chain
  #set ( $startPosPar = $contentString.indexOf('{_template') )
  ## IndexOf uses -1 if an item is not found; 0 or above if it is
  #if ( $startPosPar > 0 )
    ## Uses the String by Start and End macro to get the start and end of the shortcode
    #set ( $shortCode = "#strByStartEnd($contentString, '{form', '}')" )
    ## Sets the index of the closing brace for the shortcode
    #set ( $endPos = $contentString.indexOf('}', $startPosPar) )
    #set ( $endPos = $endPos + 1 )
    ## Gets the full shortcode entity for additional processing
    #set ( $fullShortCode = $contentString.substring($startPosPar, $endPos) )
    ## Start processing additional attributes (use as many as needed for your shortcode)
    ## The ending attribute, typically a double quote (")
    #set ( $endAtt = '"' )
    ## Your attributes, could be done differently, but this ensures we know what we get
    #set ( $attStart1 = 'att1="' )
    #set ( $attVal1   = "#strByStartEnd($shortCode, $attStart1, $endAtt)" )
    #set ( $attStart2 = 'att2="' )
    #set ( $attVal2   = "#strByStartEnd($shortCode, $attStart2, $endAtt)" )
    ## After getting all of your values, you can then start building whatever code is needed. It's recommend that you build it as a string, and replace whatever values are needed.
    ## The code {att1}, {att2} are placeholders for the real content we want dropped in.
    #set ( $embedCode = '<div id="{att1}">{att2}</div>' )
    ## If you have multiple instances of a replace, use replaceAll
    #set ( $embedCode = $embedCode.replace("\{att1\}", $attVal1) )
    #set ( $embedCode = $embedCode.replace("\{att2\}", $attVal2) )
    ## Replace the HTML content with your updated $embedCode
    #set ( $wysiwyg = $contentString.replace($fullShortCode, $embedCode) )

    ## Don't forget to update do_shortcode with a new elseif entry
  #else ## Nothing was found, just pass it through (ensures we don't try to process something that doesn't need it ). Also sets the $wysiwyg variable to be output on the desired content format
    #set ( $wysiwyg = $contentString )
  #end
#end
{{</code>}}
