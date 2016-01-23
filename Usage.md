**For questions or support, please visit the [SLIR Google Group](http://groups.google.com/group/smart-lencioni-image-resizer/topics). If you have found a bug, please [use the bug tracker](http://code.google.com/p/smart-lencioni-image-resizer/issues/list).**

# Usage #
To use, place an img tag with the src pointing to the path of SLIR (typically "/slir/") followed by the parameters, followed by the path to the source image to resize. All parameters follow the pattern of a one-letter code and then the parameter value:
| **Parameter** | **Meaning** |
|:--------------|:------------|
| w             | Maximum width |
| h             | Maximum height |
| c             | Crop ratio  |
| q             | Quality     |
| b             | Background fill color |
| p             | Progressive |

Filenames that include special characters must be URL-encoded (e.g. plus sign, +, should be encoded as %2B) in order for SLIR to recognize them properly. This can be accomplished by passing your filenames through PHP's `rawurlencode()` or `urlencode()` function.

## Examples ##

### Resizing an image to a max width of 100 pixels and a max height of 100 pixels ###

`<img src="/slir/w100-h100/path/to/image.jpg" alt="Don't forget your alt text" />`

### Resizing and cropping an image into a square ###

`<img src="/slir/w100-h100-c1:1/path/to/image.jpg" alt="Don't forget your alt text" />`

### Resizing and cropping an image to exact dimensions ###

To do this, you simply need to make the crop ratio match up with the desired width and height. For example, if you want your image to be exactly 150 pixels wide by 100 pixels high, you could do this:

`<img src="/slir/w150-h100-c150:100/path/to/image.jpg" alt="Don't forget your alt text" />`

Or, more concisely:

`<img src="/slir/w150-h100-c15:10/path/to/image.jpg" alt="Don't forget your alt text" />`

However, SLIR will not enlarge images. So, if your source image is smaller than the desired size you will need to use CSS to make it the correct size.

### Resizing a JPEG without interlacing (for use in Flash) ###

`<img src="/slir/w100-p0/path/to/image.jpg" alt="Don't forget your alt text" />`

### Matting a PNG with #990000 ###

`<img src="/slir/b900/path/to/image.png" alt="Don't forget your alt text" />`

### Without mod\_rewrite (not recommended) ###

`<img src="/slir/?w=100&amp;h=100&amp;c=1:1&amp;i=/path/to/image.jpg" alt="Don't forget your alt text" />`

### An image with a + in its filename ###

`<img src="/slir/w100/path/to/image%2Bfile.jpg" alt="Don't forget your alt text" />`

# Troubleshooting #

## Call to undefined function unixtojd() ##

If you see an error message like this in your logs:

```
PHP Fatal error:  Call to undefined function unixtojd() in
/xxx/xxx/slir/pel-0.9.1/PelEntryAscii.php on line 313
```

PHP is missing some calendar functions and needs to be recompiled with `--enable-calendar`.