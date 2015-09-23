# Sass grids

Simple grid framework I use on client projects

## Goals

I wanted a simple and quick way to design responsive grids in Sass so I built this micro grid framework. It allows you to use namespaced (silent) classes to create a mobile first grid very rapidly. Set goals:

- Responsive
- Mobile First
- Infinitely Nestable
- No .alpha or .omega classes to worry about
- Use proportional grids
- Mix a fluid grid with fixed gutters
- Allow both normal classes in the HTML or silent classes and @extend

## Browser Support

This version uses [Flexbox](http://caniuse.com/#feat=flexbox). Provided you install [Autoprefixer](https://github.com/postcss/autoprefixer), it will give you a [fairly good support across modern browsers](http://caniuse.com/#feat=flexbox).

- latest versions of Opera / Firefox / Chrome / Safari
- IE10 and above

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

Grid units have a default width of 100%. The `.grid__unit--#{$namespace}full` classes are also available should you need a grid module to span the full width of your grid at any given breakpoint.

By default `.grid__unit` will wrap on different lines. You can change that behaviour using the `.grid--nowrap` variation. When using that variant, `.grid__unit` have equal proportions on the same row and that proportion will change depending on the number of `.grid__unit` in the row.

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

## Order classes

Flexbox allows you to change the order of flexbox-items independently from source order using the `order` property. This framework provides namespaced order classes allowing you to change the order in which grid units are displayed at various breakpoints.

Used in conjunction with grid classes, these allow for more complex content choreography. Your layout can diverge from source order.

    <div class="grid">
        <div class="grid__unit  grid__unit--medium-1of2  grid__unit--large-2of3  grid__unit--large-order2">
            <p>Content</p>
        </div><!--

     --><div class="grid__unit  grid__unit--medium-1of2  grid__unit--large-1of3  grid__unit--large-order1">
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

## Shoutouts

### Harry Roberts

If you need a solid Sass framework, check out [inuit.css](http://inuitcss.com/) and [csswizardry-grids](https://github.com/csswizardry/csswizardry-grids). These were a huge inspiration for this and I share a lot of [Harry's views on proportional grids and namespaced classes](http://csswizardry.com/2013/02/responsive-grid-systems-a-solution/).

However, there were a few things that prompted me to create my own thing:

- Harry's system, albeit simpler than many others I have seen, caters for many use cases that I don't need. By developing my own thing, I could make it simpler and adapt it more easily to each project.
- I wanted to understand this fully and it was a good excuse to learn some Sass

### Chris Coyier

Nice article on [how to handle white-space when using inline-block](http://css-tricks.com/fighting-the-space-between-inline-block-elements/) over at CSS-tricks

Chris is also the author of [one of the most comprehensive article on flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/).

### Paul Irish

Using box-sizing:border-box; on elements [allows you to use percentage width coupled with fixed value padding / margins](http://paulirish.com/2012/box-sizing-border-box-ftw/).

### Trent Walton

The concept of [content choreography](http://trentwalton.com/2011/07/14/content-choreography/) is important with RWD projects. The demo includes a small example in the footer, with the first module being above the five others at large screen sizes. Switching the visual order of main and secondary content is done using push and pull classes.
