# Sass grids

Simple experiment to create grids in Sass

## Goals

I wanted a simple and quick way to design responsive grids in Sass so I built this micro grid framework. It allows you to use namespaced (silent) classes to create a mobile first grid very rapidly. Set goals:

- Responsive
- Mobile First
- Infinitely Nestable
- No .alpha or .omega classes to worry about
- Use proportional grids
- Mix a fluid grid with fixed gutters
- Allow both normal classes in the HTML or silent classes and @extend

## Demo

[Here is a small demo](http://jeromecoupe.github.io/sassgrids/) of a grid in action.

- The grid in the demo uses a nested grid along with "push" and "pull" classes
- The demo makes use of [modernizr.js](http://www.modernizr.com) / [respond.js](https://github.com/scottjehl/Respond) / [selectivizr.js](https://github.com/keithclark/selectivizr) to support IE8

## Available classes and proportions

We are talking about proportional grids so these classes mean "spanning [proportion] of its parent's width". The default configuration allows you to combine 2 grids (10 and 12 units) but you can easily create your own grid or combination of grids.

    .grid__unit--#{$namespace}full

    .grid__unit--#{$namespace}1of10
    .grid__unit--#{$namespace}2of10
    .grid__unit--#{$namespace}3of10
    .grid__unit--#{$namespace}4of10
    .grid__unit--#{$namespace}5of10
    .grid__unit--#{$namespace}6of10
    .grid__unit--#{$namespace}7of10
    .grid__unit--#{$namespace}8of10
    .grid__unit--#{$namespace}9of10

    .grid__unit--#{$namespace}1of12
    .grid__unit--#{$namespace}2of12
    .grid__unit--#{$namespace}3of12
    .grid__unit--#{$namespace}4of12
    .grid__unit--#{$namespace}5of12
    .grid__unit--#{$namespace}6of12
    .grid__unit--#{$namespace}7of12
    .grid__unit--#{$namespace}8of12
    .grid__unit--#{$namespace}9of12
    .grid__unit--#{$namespace}10of12
    .grid__unit--#{$namespace}11of12

Grid modules have a default width of 100%. The `.grid__unit--#{$namespace}full` classes are also available should you need a grid module to span the full width of your grid at any given breakpoint

## Grid variants

Grid variants are available:

- `.grid--gutterless`: no gutters
- `.grid--right`: right aligned grid units
- `.grid--left`: left aligned grid units
- `.grid--center`: center aligned grid units
- `.grid--middle`: grid units aligned vertically to the middle
- `.grid--bottom`: grid units aligned vertically to the bottom


## Use classes in HTML

Since this is using inline-block and not floats, comments must be in there to alleviate the fact that [many browsers account for white-space between inline-block elements](http://css-tricks.com/fighting-the-space-between-inline-block-elements/).

Benefits of using inline-block

- more flexible than floats in a responsive grid context
- no clearing to worry about
- no float drops

Every `.grid__unit` has to live within a `.grid`. Provided you have defined `medium` and `large` breakpoints, here is a simple grid.

    <div class="grid">
        <div class="grid__unit  grid__unit--medium-1of2  grid__unit--large-2of3">
            <p>Content</p>
        </div><!--

     --><div class="grid__unit  grid__unit--medium-1of2  grid__unit--large-1of3">
            <p>Content</p>
        </div>
    </div>

You can nest grids to your heart's content.

    <div class="grid">
        <div class="grid__unit  grid__unit--medium-1of2  grid__unit--large-2of3">

            <div class="grid">
                <div class="grid__unit  grid__unit--medium-1of3">
                    <p>Content</p>
                </div><!--

             --><div class="grid__unit  grid__unit--medium-1of3">
                    <p>Content</p>
                </div><!--

             --><div class="grid__unit  grid__unit--medium-1of3">
                    <p>Content</p>
                </div>
            </div>

        </div><!--

     --><div class="grid__unit  grid__unit--medium-1of2  grid__unit--large-1of3">
            <p>Content</p>
        </div>
    </div>

## Use Sass placeholder classes

If you don't like grid classes in your HTML and want to use Sass placeholder classes and `@extend`, there is a simple true or false switch in the `_variables.scss` allowing you to use placeholder classes.

### HTML

    <div class="content">
        <div class="content__primary">
            <p>Content</p>
        </div><!--

     --><div class="content__secondary">
            <p>Content</p>
        </div>
    </div>

### Sass

Provided that you have defined `medium` and `large` breakpoints

    .content
    {
        @extend %grid;
    }

    .content__primary
    {
        @extend %grid__unit;
        @extend %grid__unit--medium-1of2;
        @extend %grid__unit--large-2of3;
    }

    .content__secondary
    {
        @extend %grid__unit;
        @extend %grid__unit--medium-1of2;
        @extend %grid__unit--large-1of3;
    }

## Proportional "push" and "pull" classes

Proportional "push" and "pull" classes are available:

- Push classes nudge grid units to the left by a certain proportion
- Pull classes nudge grid units to the right by a certain proportion

Used in conjunction with grid classes, these allow for more complex content choreography. Your layout can diverge a little bit more from source order at non default screen sizes. The demo uses "push" an "pull" classes.

    <div class="grid">
        <div class="grid__unit  grid__unit--medium-1of2  grid__unit--large-2of3  grid__unit--large-push-1of3">
            <p>Content</p>
        </div><!--

     --><div class="grid__unit  grid__unit--medium-1of2  grid__unit--large-1of3  grid__unit--large-pull-2of3">
            <p>Content</p>
        </div>
    </div>

## Using defined breakpoints and media-queries for something else than grids

You can also use defined breakpoints and media-queries in your SCSS files for something else than layout / grids

    body
    {
        background:#fff;
        @include mq(large)
        {
            background:#ccc;
        }
    }

When defining a breakpoint, you can prevent it from being used to generate grids and namespaced (silent) grid classes. Just set the `generate-grid-classes` parameter in the sass maps in `_variables.scss` to `false`

    $breakpoints-list: (
      "small": (
        query: "all and (min-width: 31.25em)",
        generate-grid-classes: true
      ),
      "medium": (
        query: "all and (min-width: 47.5em)",
        generate-grid-classes: true
      ),
      "large": (
        query: "all and (min-width: 64em)",
        generate-grid-classes: true
      ),
      "xlarge": (
        query: "all and (min-width: 71.25em)",
        generate-grid-classes: false
      )
    );

## Browser Support

Tested with:

- latest versions of Opera / Firefox / Chrome / Safari
- IE8 and above
- IE7 does not support box-sizing nor display:inline-block. I generally serve a linearised version of the page to IE7 and IE6 users.

## Shoutouts

### Harry Roberts

If you need a solid Sass framework, check out [inuit.css](http://inuitcss.com/) and [csswizardry-grids](https://github.com/csswizardry/csswizardry-grids). These were a huge inspiration for this and I share a lot of [Harry's views on proportional grids and namespaced classes](http://csswizardry.com/2013/02/responsive-grid-systems-a-solution/).

However, there were a few things that prompted me to create my own thing:

- Harry's system, albeit simpler than many others I have seen, caters for many use cases that I don't need. By developing my own thing, I could make it simpler and adapt it more easily to each project.
- I wanted to understand this fully and it was a good excuse to learn some Sass

### Chris Coyier

Nice article on [how to handle white-space when using inline-block](http://css-tricks.com/fighting-the-space-between-inline-block-elements/) over at CSS-tricks

### Paul Irish

Using box-sizing:border-box; on elements [allows you to use percentage width coupled with fixed value padding / margins](http://paulirish.com/2012/box-sizing-border-box-ftw/).

### Trent Walton

The concept of [content choreography](http://trentwalton.com/2011/07/14/content-choreography/) is important with RWD projects. The demo includes a small example in the footer, with the first module being above the five others at large screen sizes. Switching the visual order of main and secondary content is done using push and pull classes.
