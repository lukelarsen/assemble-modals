[Assemble]:                http://assemblecss.com
[Assemble Core]:           https://github.com/lukelarsen/assemble-core
[postcss-constants]:       https://github.com/macropodhq/postcss-constants

# Assemble Modals
Assemble Modals is a component of the [Assemble] CSS Framework. It will give you a solid base for modals in your project. It has some default styles that can easily be overridden so you can add your own look.

## Requirements
Assemble Buttons requires [Assemble Core].

## Installation
npm install assemble-modals --save-dev

## Usage
### Gulp
```js
var gulp = require('gulp');
var postcss = require('gulp-postcss');
var assembleCore = require('assemble-core');
var assembleModals = require('assemble-modals');

gulp.task('css', function () {
    var processors = [
        assembleCore({
            zLayerValues: {
                'modal': 9,
                'tip': 10
            }
        }),
        assembleModals
    ];
    return gulp.src('./src/*.css')
        .pipe(postcss(processors))
        .pipe(gulp.dest('./dest'));
});
```

## Options
Options are set with variables. These variables are already set with their default values so they will just work out of the box. If you wish to change them just define the variable you want to change before you load the _assemble-modals.css file. You may wish you see [Assemble Core] for more examples and directions for setting up a Assemble project.

### Design Variables

##### $modal-overlay-color
- Default: rgba(0, 0, 0, 0.6);
- Type: Color
```css
$modal-overlay-color: rgba(0, 0, 0, 0.6);
```

##### $modal-inner-padding
- Default:  15px;
- Type: Number
- It will take any number witha unit type.
```css
$modal-inner-padding: 5px;
```

##### $modal-inner-background-color
- Default: #FFF;
- Type: Color
```css
$btn-padding: 5px 10px;
```

##### Modal z-index
This component makes use of the [postcss-constants] plugin to set the z-index. [postcss-constants] is included with [Assemble Core] so you are good to go. This helps keep all our z-index values in one place. Do get this working you will need to:
1- Create a 'constants.js' file and add this to it
```js
module.exports = {
  zindexes: {
    modal: 99,
    modalInner: -1,
    modalInnerVisible: 100,
    modalClose: 2,
  }
};
```
2- Then in your main css file add this towards the top:
```css
~zindexes: "./constants.js";
```

Now the assemble-modal plugin will pull the z-index values from the constants.js file. You can add more values there and call them in your css with
```css
z-index: ~zindexes.tip;
```


##### $modal-close-background-color
- Default: #000;
- Type: Color
```css
$modal-close-background-color: #333;
```

##### $modal-close-color
- Default: #FFF;
- Type: Color
```css
$modal-close-color: #EEE;
```

##### Modal Widths
You can set all the widths you need for your modals in a .modal-widths class. The first value is the name and the second is what the max width should be. See the example below.

###### Example
```css
.modal-widths{
    large: 500px;
    medium: 300px;
    half: 50%;
}
```
Will output:
```css
.modal__block-large {
  max-width: 500px;
}

.modal__block-medium {
  max-width: 300px;
}

.modal__block-half {
  max-width: 50%;
}
```
