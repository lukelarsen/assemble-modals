[Assemble]:                http://assemblecss.com
[Assemble Base]:           https://github.com/lukelarsen/assemble-base
[postcss-map]:             https://github.com/pascalduez/postcss-map

# Assemble Modals
Assemble Modals is a component of the [Assemble] CSS Framework. It will give you a solid base for modals in your project. It has some default styles that can easily be overridden so you can add your own look.

## Requirements
- Assemble Modals requires [Assemble Base].
- The Vanilla Modal javascript file (vanilla-modal.js). It is inluded in this repo.
- This will need to run after the page is loaded.
```js
var modal = new vanillaModal.VanillaModal({});
```

## Installation
npm install assemble-modals --save-dev

## Usage
### Gulp
```js
var gulp = require('gulp');
var postcss = require('gulp-postcss');
var assembleBase = require('assemble-base');
var assembleModals = require('assemble-modals');

gulp.task('css', function () {
    var processors = [
        assembleBase,
        assembleModals
    ];
    return gulp.src('./src/*.css')
        .pipe(postcss(processors))
        .pipe(gulp.dest('./dest'));
});
```
Then import the _assemble-modals.css file from your css file.
```css
@import '../node_modules/assemble-base/base';

/*
Override variables here before the Assemble Components are loaded.
*/

@import '../node_modules/assemble-modals/assemble-modals';
```

### HTML
This only need to appear once in your app. All modals will be injected inside of it. Put it at the bottom of the DOM.
```html
<div class="modal">
    <div class="modal-inner">
        <a class="modal-close" rel="modal:close">×</a>
        <div class="modal-content"></div>
    </div>
</div>
```
Contents of the modal
```html
<div id="modal-1" class="modal-block">
    <div class="modal-header">
        <h2>Headline</h2>
    </div>
    <div class="modal-body">
        <div class="modal-body__inner">
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Natus obcaecati optio reprehenderit consequuntur, dignissimos sit sint animi explicabo vitae deserunt facere dolores nam. Illo iusto pariatur dolore, officiis unde saepe.</p>
        </div>
    </div>
    <div class="modal-footer">
        <button class="btn">Submit</button>
    </div>
</div>
```
What triggers the modal
```html
<a href="#modal-1" rel="modal:open">Open Modal One</a>
```

## Options
Options are set with variables. These variables are already set with their default values so they will just work out of the box. If you wish to change them just define the variable you want to change before you load the _assemble-modals.css file. You may wish you see [Assemble Base] for more examples and directions for setting up a Assemble project.

### Design Variables

##### $modal-overlay-color
- Set the overlay color for your modals.
- Default: rgba(0, 0, 0, 0.6);
- Type: Color
```css
$modal-overlay-color: rgba(0, 0, 0, 0.6);
```

##### $modal-header-padding
- Set the header padding for your modals.
- Default: 0 30px;
- Type: Number
- It will take any number with a unit type.
```css
$modal-header-padding: 0 15px;
```

##### $modal-body-padding
- Set the body padding for your modals.
- Default: 0 30px;
- Type: Number
- It will take any number with a unit type.
```css
$modal-body-padding: 0 15px;
```

##### $modal-footer-padding
- Set the footer padding for your modals.
- Default: 30px;
- Type: Number
- It will take any number with a unit type.
```css
$modal-footer-padding: 15px;
```

##### $modal-body-height
- Set the max height for the .modal-body__inner div.
- Default: 400px;
- Type: Number
- It will take any number with a unit type. It is recommended that you use media queries to adjust this value when you need.
```css
$modal-body-height: 500px;
```

##### $modal-body-margin-bottom
- Set margin-bottom for the .modal-body__inner div.
- Default: 78px;
- Type: Number
- It will take any number with a unit type.
```css
$modal-body-margin-bottom: 85px;
```

##### $modal-inner-background-color
- Set the inner background color for your modals.
- Default: #FFF;
- Type: Color
```css
$btn-padding: 5px 10px;
```

##### Modal z-index
This component makes use of the [postcss-map] plugin to set the z-index. [postcss-map] is included with [Assemble Base] so you are good to go. This helps keep all our z-index values in one place. To get this working you will need to:
1- Create a 'constants.json' file and add this to it
```js
{
    "zIndexes": {
        "modal": 99,
        "modalInner": -1,
        "modalInnerVisible": 100,
        "modalClose": 2,
    }
}
```
2- Then in your main gulp file provide the path to the newly created constants.json in the assembeCore options.
```js
assembleCore({
    basePath: 'src/',
    maps: [ 'constants.json' ]
})
```

Now the assemble-modal component will pull the z-index values from the constants.js file. You can add more values there and call them in your css with
```css
z-index: map(constants, zIndexes, something);
```


##### $modal-close-background-color
- Set the background color of your modal close icon.
- Default: #000;
- Type: Color
```css
$modal-close-background-color: #333;
```

##### $modal-close-color
- Set the color of your modal close icon.
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
body[data-current-modal*="_large"] .modal-inner{
    max-width: 500px;
}

body[data-current-modal*="_medium"] .modal-inner{
  max-width: 300px;
}

body[data-current-modal*="_half"] .modal-inner{
  max-width: 50%;
}
```
Usage
```html
<div id="modal-1_large" class="modal-block">
    <div class="modal-header">
        <h2>Headline</h2>
    </div>
    <div class="modal-body">
        <div class="modal-body__inner">
            <ul class="form-thirds">
                <li>
                    <label>Input Field 1</label>
                    <input type="text">
                </li>
                <li>
                    <label>Input Field 2</label>
                    <input type="text">
                </li>
                <li>
                    <label>Input Field 3</label>
                    <input type="text">
                </li>
            </ul>
        </div>
    </div>
    <div class="modal-footer">
        <button class="btn">Submit</button>
    </div>
</div>
```

##### Modal Heights
To set the modal height you will need to change the max-height of the .modal-body__inner div.
