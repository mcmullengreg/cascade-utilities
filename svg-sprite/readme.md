# SVG Sprite
This script helps take a folder of SVG files and combines them into a single SVG, to be used as a Sprite. The files
can live anywhere on your site. In this example we are also using a default object called `$framework` to pull in
the location of the framework site and/or folder.

## Sample Structure

```
Site://Name
│
└───images
│   └───icons
│       │   file.svg
│       │   file2.svg
│       │   ...
│
└───formats
    │   svg-sprite.vm
```

## Usage

Setup your template to utilize this format as a region, or import it as you see fit. The first variable finds the location
of the SVGs to build out the sprite. Set your default site as you see fit

```
#set ( $icons = $_.locateFolder("/path-to/svgs", $svgSite) )
```

We then utilize the `cleanSVG` macro to clean the SVG items, customize as you see fit, ensuring we keep the viewBox
and swapping the `svg` element for `symbol`.

At the moment, SVG's should be placed into your Cascade CMS instance _without_ comments. Comments are not filtered out,
but could be added to the list in your installation.

### Example SVG

```
<svg xmlns="***" viewBox="***" ...>
  <path|group|etc>
</svg>
```
