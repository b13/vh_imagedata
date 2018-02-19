# EXT:vh_imagedata

## Viewhelper to build custom <img>-Tag

This viewhelper calculates an image based on <f:image> without rendering an image tag, making the data available in the
 content of the viewhelper for manual use or rendering custom image tags. The rendering takes all crop settings into 
 account. The Viewhelper is automatically registered into the `b` namespace.
 
### Basic useage example

```
<b:imagedata src="{file.uid}" treatIdAsReference="1" width="300" as="imageData">
    <div class="b_lazyloading__background" style="padding-bottom: {1 / imageData.ratio}%;">
        <img src="transparent.gif" data-imageurl="{imageData.uri}" width="{imageData.width}" height="{imageData.height}" 
            class="b_lazyloading__image bJS_lazyloading" 
            alt="{imageData.alt}" title="{imageData.title}" />
    </div>
</b:imagedata>
```

### Allowed attributes

The following attributes can be passed to the ViewHelper. All attributes normally allowed for `f:image` can be passed
but not all make sense.

Argument | Type | Info
:--- | :--- | :---
as | string | Name of variable to create. Defaults to `imageData`
alt | string | Specifies an alternate text for an image'
title | string | Tooltip text of element
src | string | a path to a file, a combined FAL identifier or an uid (int). If $treatIdAsReference is set, the integer is considered the uid of the sys_file_reference record. If you already got a FAL object, consider using the $image parameter instead
treatIdAsReference | bool | given src argument is a sys_file_reference record
image | object | a FAL object
crop | string|bool | overrule cropping of image (setting to FALSE disables the cropping set in FileReference
cropVariant | string | select a cropping variant, in case multiple croppings have been specified or stored in FileReference
width | string | width of the image. This can be a numeric value representing the fixed width of the image in pixels. But you can also perform simple calculations by adding "m" or "c" to the value. See imgResource.width for possible options.
height | string | height of the image. This can be a numeric value representing the fixed height of the image in pixels. But you can also perform simple calculations by adding "m" or "c" to the value. See imgResource.width for possible options.
minWidth | int | minimum width of the image
minHeight | int | minimum width of the image
maxWidth | int | minimum width of the image
maxHeight | int | minimum width of the image
absolute | bool | Force absolute URL
value | mixed | Value to assign. If not in arguments then taken from tag content


### Returned data

The ViewHelper returns an array with all the image data as `{imageData}` or the variable name you set in argument `as`.
The array contains these values:

Key | Info 
:--- | :---- 
width | Width of the rendered image 
height | Height of the rendered image
uri | URL of the image rendered
alt | Alt tag for the image, taken from the sys_file_record, the sys_file_reference or from the "alt"-argument of the viewhelper
title | Title tag for the image, taken from the sys_file_record, the sys_file_reference or from the "title"-argument of the viewhelper 
ratio | The ratio of the cropped/rendered image (width / height), meaning 1.77777 for an image with 16:9 ratio
heightRatio | The ratio of height to width, for use in inline styles of containers for responsive images
link | Value of the link field from sys_file_reference
processingInstructions | Original processing instructions used for image rendering (including crop-values as array)
processedImage | The processed file
originalImage | The original file 

## Installing

Use Composer to add to your project:

`composer require b13/vh_imagedata`

No further configuration needed.


 
