
# tinyColorPicker and colors

Looking for mobile first, tiny foot print, fast, scaleable, flexible and pluggable...<br>
This 4.5KB small HSB color picker is based on a subset of [colors.js](https://github.com/PitPik/colorPicker/blob/master/colors.js) from it's big brother [colorPicker](https://github.com/PitPik/colorPicker/), supports all modern features like touch and MS pointer, GPU accelerated rendering, battery friendly requestAnimationFrame and provides a lot of hooks for developers to write plugins.

##Demo
See **demo** at [dematte.at/tinyColorPicker](http://dematte.at/tinyColorPicker)

<img src="development/screen-shot-all.jpg" />

All the WCAG 2.0 calculations for readability are also based on opacity levels of all layers.<br>
Supported color spaces are: rgb, hsv(b), hsl, HEX

##colors.js

```javascript
Colors({ // all options have a default value...
    color: 'rgba(204, 82, 37, 0.8)', // initial color (#RGB, RGB, #RRGGBB, RRGGBB, rgb(r, g, b), ...)
    grey: {r: 0.298954, g: 0.586434, b: 0.114612}, // CIE-XYZ 1931
    luminance: {r: 0.2126, g: 0.7152, b: 0.0722}, // W3C 2.0
    valueRanges: {rgb: {r: [0, 255], g: [0, 255], b: [0, 255]}, hsv:...}, // skip ranges if no conversion required
    customBG: '#808080' // the solid bgColor behind the chosen bgColor (saved color)
    convertCallback: function(colors, type){}, // callback function after color convertion for further calculations...
});
```
##jqColorPicker.js

colorPicker uses an instance of Colors and passes the options to it, so some values are the same...

```javascript
ColorPicker({
    color: ..., // see Colors...
    customBG: '#FFF' // see Colors...
    animationSpeed: 150, // toggle animation speed
    GPU: true, // use transform: translate3d
    doRender: true, // manipulate color ans bgColor of input field
    opacity: true, // enable / disable alpha slider
    renderCallback: function($elm, toggled) {}, // this === instance
    buidCallback: function($elm) {}, // this === instance
    css: '', // replaces existing css
    cssAddon: '', // adds cdd to existing
    margin: '', // positioning margin
    preventFocus: false // prevent default on focus of input fields
});
```

##The color model, the methods and more

After initializing Color or ColorPicker you'll get a clean but rhich model of the instance:

```javascript
myColors: {
    colors: { all kinds of color values...  see later},
    options: { all the options you set or that are set as default... },
    __proto__: { // all methods Color uses
        setColor: function(newCol, type, alpha) {},
        setCustomBackground: function(col) {},
        saveAsBackground: function() {},
    }
}
```

```javascript
myColorPicker: {
    color: { // instance of Color inside colorPicker
        colors: { all kinds of color values... see later},
        options: { all the options you set or that are set as default... },
        __proto__: { all methods Color uses ... see above}
    },
    __proto__: { // all methods ColorPicker uses
        render: function() {},
        toggle: function() {}
    }
}
```


The color model

```javascript
HEX: // current color as HEX (upper case, 6 digits)
rgb: // current RGB color as normalized values (0 - 1)
    r: // red
    g: // green
    b: // blue
hsv: // current color values in normalized HSV (HSB) model
    h: // hue
    s: // saturation
    v: // value (brightness)
hsl: // current color values in normalized HSL model
    h: // hue
    s: // saturation
    l: // lightness
RND: // all above colors in their defined ranges
    rgb: // current RGB color, rounded between 0 and 255
        r: // red (0 - 255)
        g: // green (0 - 255)
        b: // blue (0 - 255)
    hsv: // see above
        h: // hue (0 - 360 degrees)
        s: // saturation (0 - 100 %)
        v: // value (brightness) (0 - 100 %)
    hsl: // see above
        h: // hue (0 - 360 degrees)
        s: // saturation (0 - 100 %)
        l: // lightness (0 - 100 %)
background: // saved (background) color (saveAsBackground(){})
    rgb: // color in RGB model
        r: // red
        g: // green
        b: // blue
    RGB: // RGB color, rounded between 0 and 255
        r: // red (0 - 255)
        g: // green (0 - 255)
        b: // blue (0 - 255)
    alpha: // alpha or opacity value (0 - 1)
    equivalentGrey: // r = g = b = (0 - 255)
    rgbaMixBlack: // saved (background) color mixed with solid black color
        r: // red
        g: // green
        b: // blue
        a: // resulting alpha or opacity value (0 - 1)
        luminance: // luminance of resulting mix (0 - 1)
    rgbaMixCustom: // saved (background) color mixed with custom (solid) color
        r: // red
        g: // green
        b: // blue
        a: // resulting alpha or opacity value (0 - 1)
        luminance: // luminance of resulting mix (0 - 1)
    rgbaMixWhite: // saved (background) color mixed with solid white color
        r: // red
        g: // green
        b: // blue
        a: // resulting alpha or opacity value (0 - 1)
        luminance: // luminance of resulting mix (0 - 1)
alpha: // alpha or opacity value (0 - 1) of current color
equivalentGrey: // r = g = b = (0 - 1)
HUELuminance: // luminance of hue (in full brightnes and saturation) (0 - 1)
RGBLuminance: // luminance of the current color
hueRGB: // rounded integer value of current color in rgb model with full saturation and brightness
    r: // red (0 - 255)
    g: // green (0 - 255)
    b: // blue (0 - 255)
saveColor: // '' or 'web smart' or 'web save', if so.
webSave: // closest web-save color
    r: // red (0 - 255)
    g: // green (0 - 255)
    b: // blue (0 - 255)
webSmart: // closest web-smart color
    r: // red (0 - 255)
    g: // green (0 - 255)
    b: // blue (0 - 255)
rgbaMixBG: // color mix result: current color above saved (background) color
    r: // red (0 - 1)
    g: // green (0 - 1)
    b: // blue (0 - 1)
    a: // resulting alpha or opacity value (0 - 1)
    luminance: // luminance of resulting mix (0 - 1)
rgbaMixBGMixCustom: // color mix result: current color above saved (background) color above solid custom color
    r: // red (0 - 1)
    g: // green (0 - 1)
    b: // blue (0 - 1)
    a: // resulting alpha or opacity value (0 - 1)
    luminance: // luminance of resulting mix (0 - 1)
    luminanceDelta: // luminance difference between current color and resulting saved-custom mix (0 - 1)
    hueDelta: // hue difference between current color and resulting saved-custom mix (0 - 1)
    WCAG2Ratio: // readability vale (1 - 21, 1:1 to 21:1)
rgbaMixBlack: // color mix result: current color above solid black
    r: // red (0 - 1)
    g: // green (0 - 1)
    b: // blue (0 - 1)
    a: // resulting alpha or opacity value (0 - 1)
    luminance: // luminance of resulting mix (0 - 1)
    WCAG2Ratio: // readability vale (1 - 21, 1:1 to 21:1)
rgbaMixWhite: // color mix result: current color above solid white
    r: // red (0 - 1)
    g: // green (0 - 1)
    b: // blue (0 - 1)
    a: // resulting alpha or opacity value (0 - 1)
    luminance: // luminance of resulting mix (0 - 1)
    WCAG2Ratio: // readability vale (1 - 21, 1:1 to 21:1)
```
