+++
title = "Find Codes"
description = ""
+++

{{<lead>}}
The default file contains `find_shortcode` and a utility macro called `strByStartEnd`. `find_shortcode` is the actual workhorse, but wouldn't be possible without the utility macro also included in this file.
{{</lead>}}

{{<code lang="java">}}
## Import all known shortcode Formats
#set ( $siteName = "YourSiteName" )
#set ( $folder = $_.locateFolder("shortcodes", $siteName) )
#set ( $codes = [] )
#set ( $shortcodes = [] )
## Import the shortcode files
#foreach ( $child as $folder.children )
    #set ( $formatPath = "site://${siteName}/" + $child.path )
    #if ( $child.name != "default" || $child.name != "_template" )
        #import($formatPath)
        #set ( $null = $codes.add($child.name) )
    #end
#end
#macro ( findCodes $contentString )
  #set ( $startPosPar = $contentString.indexOf('[') )
  #if ( $startPosPar > 0 )
    ## To avoid some conflicts, we replace the square brackets with curly here.
    #set ( $scFull = "#strByStartEnd($contentString, '[', ']')" )
    #set ( $scName = $scFull.split("\s") )
    #set ( $scName = $scName[0] )
    #if ( $codes.contains($scName) )
      #set ( $replace = "["+$scFull+"]" )
      #set ( $new = "{"+$scFull+"}" )
      #set ( $contentReplace = $contentString.replace($replace,$new) )
      #set ( $void = $shortcodes.add($new) )
      #set ( $wysiwyg = $contentReplace )
      #findCodes($wysiwyg)
    #else
      #foreach ( $item in $shortcodes )
        #do_shortcode($item, $wysiwyg)
      #end
    #end
  #else
    #foreach ( $item in $shortcodes )
      #do_shortcode($item, $wysiwyg)
    #end
  #end
#end
{{</code>}}

### Utility Macro

{{<code lang="java">}}
#*
Macro to get a substring by a start and end string, e.g.
  Full String           Start String    End String  Return
  [getBlock settings]   [getBlock       ]           settings
  attribute="your/path" attribute="     "           your/path
*#
#macro ( strByStartEnd $contentString $startString $endString )
  #set ( $startPos = $contentString.indexOf($startString) )
  #if ( $startPos > 0 )
    #set ( $startPosExc = $startPos + $startString.length() )
    $contentString.substring($startPosExc, $contentString.indexOf($endString, $startPosExc))
  #end
#end
{{</code>}}
