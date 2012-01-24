# Zass

**One mixin to rule them all**

Zass is a [Sass](http://sass-lang.com/ "Sass homepage") (CSS) fluid grid framework. Zass is 100% fluid, semantic, clean and allow infinite nesting of columns with the use of a single mixin.

* 100% fluid because it only uses percentage units to create grid dimensions.
* Semantic, because thanks to Sass CSS pre-processor there is no need to pollute HTML with design named classes (as `.col_4` to indicate 4 grid units width).
* Clean because it doesn't use any CSS hack neither uggly negative margins. Zass doesn't care about obsolete browsers like Internet Explorer 6.
* Zass can nest infinite levels of columns.
* And what is more awesome, Zass can do all of this using one single mixin.

## Setup
Zass framework requires you are working with [Sass](http://sass-lang.com/ "Sass homepage").

With git, to get latest stable version:

    git clone https://github.com/laMarciana/zass.git

Otherwise, download it from:

    https://github.com/laMarciana/zass/zipball/master

Move zass files to your sass directory and import `sass/_zass.scss` from your sass stylesheet:

    @import 'sass/zass';

## How it works?
First you have to configure your grid dimensions through three variables. Here it's an example for a 960px grid:

    $zass-column-width: 60px; //Grid columns width
    $zass-gutter-width: 20px; //Grid gutters width
    $zass-grid-units: 12; //Grid number of columns

Then, you are ready to start creating and nesting as many columns as you want using the `zass-column()` mixin:

    zass-column($n, $parent-n, $position, $push, $pull);

Here it is an explanation of `zass-column` parameters:

* `$n`: number of grid units that the column will spread.
* `$parent-n`: For nested columns, number of grid units that the parent column spreads. 0 means it's not a nested column. `0 ` is default.
* `$position`: For nested columns, it can be `left`, `right` or `inner` if a column is the left extreme one, the right extreme one or an inner one. No needed for not nested columns. `inner` by default.
* `$push`: Number of grid units to push (left margin) a column
* `$pull`: Number of grid units to pull (right margin) a column

So, let's say you have following DOM structure:

    <div id="col1">
      <p>Column 1</p>
    </div>

    <div id="col2">
      <div id="col2-1">
        <p>Column 2-1</p>
      </div>
      <div id="col2-2">
       <p>Column 2-2</p>
      </div>
     </div>

     <div id="col3">
       <p>Column 3</p>
     </div>

You could build a quickly a grid layout that way:

    @import '../../zass';

    $zass-column-width: 60px;
    $zass-gutter-width: 20px;
    $zass-grid-units: 12;

    #col1 {
       @include zass-column(3); //Spread three grid units
    }

    #col2 {
       @include zass-column(7); //Spread seven grid units
       #col2-1 {
          @include zass-column(4, 7, 'left'); //Spread 4 grid units inside #col2. It's the left one.
       }
       #col2-2 {
          @include zass-column(3, 7, 'right'); //Spread 3 grid units inside #col2. It's the right one.
       }
    }

    #col3 {
       @include zass-column(1, $push: 1); //Spread one grid unit, and push one more.
    }

Optionally, you can use a second mixin, `zass-grid()` if you want to set pixels grid width as the maximum width for a container. That way, a perfect pixels photo of a design is achieved for resolutions greater or equal than grid's pixels width while it's still 100% fluid for lower resolutions:

    zass-grid($em, $rfs)

* `$em`: If true, set that maximum width in relevant font size units ('em'). In this case, grid will increase its width if user increases text zoom level. Default to `true`.
* `$rfs`: Relevant font size to calculate maximum width in em units. Default to `16px`.

In our example:

    #wrapper {
      @include zass-grid(true, 16px); //Will ouput "max-width: 60em;" in the CSS
    }

or

    #wrapper {
      @include zass-grid(false); //Will ouput "max-width: 960px;" in the CSS
    }

## More examples

Look at the `examples/` directory for more examples.

## Reference

Variables, functions and mixins are full documented in source code.

___

If you want more control with your grid layout, you can check [fluidizer](https://github.com/laMarciana/fluidizer)

___

Copyright 2012, Marc Busqué Pérez, under GNU LESSER GENERAL PUBLIC LICENSE
marc@lamarciana.com - http://www.lamarciana.com
