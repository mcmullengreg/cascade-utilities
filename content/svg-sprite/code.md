+++
title = "Velocity Code"
description = ""
weight = 1
+++

{{< lead >}}
The below script may be used as is, see [svg-sprite]({{< ref "svg-sprite" >}}) for more details.
{{< /lead >}}

{{< code lang="java" >}}
#import("_versioning/_defaults")
#set ( $icons = $_.locateFolder("/global-assets/social-icons", $framework.get("site")) )
<svg xmlns="http://www.w3.org/2000/svg">
#foreach ( $icon in $icons.getChildren() )
    #cleanSVG($icon)
#end
</svg>
#macro ( cleanSVG $icon )
    #set ( $iconId = $icon.label.toLowerCase().replaceAll("\.", "_" ) )
    #set ( $icon = $icon.text )
    #set ( $viewBox = 'viewBox="')
    #set ( $startPos = $icon.indexOf($viewBox) )
    #if ( $startPos > 0 )
        #set ( $startPosExc = $startPos + $viewBox.length() )
        #set ( $viewBoxValue = $icon.substring($startPosExc, $icon.indexOf('"', $startPosExc)) )
    #end
    #set ( $symbol = '<symbol viewBox="' + ${viewBoxValue} + '" id="'+ ${iconId} +'"' )
    #set ( $icon = $icon.replaceAll("<(/?)svg(.*\s.*)?>", '<$1symbol>') )
    #set ( $icon = $icon.replaceAll("<title>(.*?)</title>", "") )
    #set ( $icon = $icon.replace("<symbol", $symbol) )
    $icon
#end
{{< /code >}}
