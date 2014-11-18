# Zass

**One mixin to rule them all**

Zass is a [Sass](http://sass-lang.com/ "Sass homepage") (CSS) fluid grid framework. Zass is 100% fluid, semantic, clean and allow infinite nesting of columns with the use of a single mixin.

* 100% fluid because it only uses percentage units to create grid dimensions.
* Semantic, because thanks to Sass CSS pre-processor there is no need to pollute HTML with design named classes (as `.col_4` to indicate 4 grid units width).
* Clean because it does not use any CSS hack neither uggly negative margins. Zass does not care about obsolete browsers like Internet Explorer 6.
* Zass can nest infinite levels of columns.
* And, what is more awesome, Zass can do all of this using one single mixin.

## Setup
Zass framework requires you are working with [Sass](http://sass-lang.com/ "Sass homepage").

With git, to get latest stable version:

    git clone https://github.com/waiting-for-dev/zass.git

Otherwise, download it from:

    https://github.com/waiting-for-dev/zass/zipball/master

Move zass files to your sass directory and import `sass/_zass.scss` from your sass stylesheet:

    @import 'sass/zass';

## How does it work?
First of all, you have to configure your grid through three variables. Here it is an example for a 960px grid:

    $zass-column-width: 60px; //Grid columns width
    $zass-gutter-width: 20px; //Grid gutters width
    $zass-grid-units: 12; //Grid number of columns

Then, you are ready to start creating and nesting as many columns as you want using the `zass-column()` mixin:

    zass-column($n, $parent-n, $position, $push, $pull);

Here it is an explanation of `zass-column` parameters:

* `$n`: amount of grid units that the column will take up.
* `$parent-n`: Only for nested columns, amount of grid units that the parent column takes up. 0 means it is not a nested column. `0 ` is the default.
* `$position`: Only for nested columns, it can be `left`, `right` or `inner` if a column is the left extreme one, the right extreme one or an inner one. `inner` by default.
* `$push`: Amount of grid units to push (left margin) the column
* `$pull`: Amount of grid units to pull (right margin) the column

So, let say you have following DOM structure:

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

With Zass, you could build quickly a grid layout:

    @import '../../zass';

    $zass-column-width: 60px;
    $zass-gutter-width: 20px;
    $zass-grid-units: 12;

    #col1 {
       @include zass-column(3); //Take up three grid units
    }

    #col2 {
       @include zass-column(7); //Take up seven grid units
       #col2-1 {
          @include zass-column(4, 7, 'left'); //Take up 4 grid units inside #col2. It's the left one.
       }
       #col2-2 {
          @include zass-column(3, 7, 'right'); //Take up 3 grid units inside #col2. It's the right one.
       }
    }

    #col3 {
       @include zass-column(1, $push: 1); //Take up one grid unit and push one more.
    }

Optionally, you can use a second mixin, `zass-grid()`, if you want to set grid width as the maximum width for a given container. That way, a perfect pixel photo of a design is achieved for resolutions greater or equal than grid pixel width while it is still 100% fluid for lower resolutions:

    zass-grid($em, $rfs)

* `$em`: If true, set that maximum width in em. In that case, the grid will increase its width if user increases text zoom level. Defaults to `true`.
* `$rfs`: Relevant font size to calculate maximum width in em units. Default to `16px`.

In our example:

    #wrapper {
      @include zass-grid(true, 16px); //It ouputs "max-width: 60em;" 
    }

or

    #wrapper {
      @include zass-grid(false); //Will ouput "max-width: 960px;"
    }

## More examples

Look at the `examples/` directory for more examples.

## Reference

Variables, functions and mixins are fully documented in the source code.

## Contact & Copyright

Copyright 2012, Marc Busqué Pérez, under GNU LESSER GENERAL PUBLIC LICENSE
marc@lamarciana.com - http://www.lamarciana.com
