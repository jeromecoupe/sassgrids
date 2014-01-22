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

## Use classes in HTML

Since this is using inline-block and not floats, comments must be in there to alleviate the fact that [many browsers account for white-space between inline-block elements](http://css-tricks.com/fighting-the-space-between-inline-block-elements/).

Benefits of using inline-block

- more flexible than floats in a responsive grid context
- no clearing to worry about
- no float drops

Every `.grid__module` has to live within a `.grid`.

    <div class="grid">
        <div class="grid__module  medium-span-1of2  large-span-2of3">
            <p>Content</p>
        </div><!--

     --><div class="grid__module  medium-span-1of2  large-span-1of3">
            <p>Content</p>
        </div>
    </div>

You can nest those grids to your heart's content.

    <div class="grid">
        <div class="grid__module  medium-span-1of2  large-span-2of3">

            <div class="grid">
                <div class="grid__module  medium-span-1of3">
                    <p>Content</p>
                </div><!--

             --><div class="grid__module  medium-span-1of3">
                    <p>Content</p>
                </div><!--

             --><div class="grid__module  medium-span-1of3">
                    <p>Content</p>
                </div>
            </div>

        </div><!--

     --><div class="grid__module  medium-span-1of2  large-span-1of3">
            <p>Content</p>
        </div>
    </div>

## Use Sass silent classes

If you don't like classes in your HTML and want to use Sass silent classes and `@extend`, there is a simple true or false switch in the variables you can turn on or off.

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
        @extend %grid__module;
        @extend %medium-span-1of2;
        @extend %large-span-2of3;
    }

    .content__secondary
    {
        @extend %grid__module;
        @extend %medium-span-1of2;
        @extend %large-span-1of3;
    }

## Available classes and proportions

We are talking about proportional grids so these classes mean "spanning [proportion] of its parent's width".

    .#{$namespace}span-1of2

    .#{$namespace}span-1of3
    .#{$namespace}span-2of3

    .#{$namespace}span-1of4
    .#{$namespace}span-2of4
    .#{$namespace}span-3of4

    .#{$namespace}span-1of5
    .#{$namespace}span-2of5
    .#{$namespace}span-3of5
    .#{$namespace}span-4of5

    .#{$namespace}span-1of6
    .#{$namespace}span-2of6
    .#{$namespace}span-3of6
    .#{$namespace}span-4of6
    .#{$namespace}span-5of6

    .#{$namespace}span-1of8
    .#{$namespace}span-2of8
    .#{$namespace}span-3of8
    .#{$namespace}span-4of8
    .#{$namespace}span-5of8
    .#{$namespace}span-6of8
    .#{$namespace}span-7of8

    .#{$namespace}span-1of10
    .#{$namespace}span-2of10
    .#{$namespace}span-3of10
    .#{$namespace}span-4of10
    .#{$namespace}span-5of10
    .#{$namespace}span-6of10
    .#{$namespace}span-7of10
    .#{$namespace}span-8of10
    .#{$namespace}span-9of10

    .#{$namespace}span-1of12
    .#{$namespace}span-2of12
    .#{$namespace}span-3of12
    .#{$namespace}span-4of12
    .#{$namespace}span-5of12
    .#{$namespace}span-6of12
    .#{$namespace}span-7of12
    .#{$namespace}span-8of12
    .#{$namespace}span-9of12
    .#{$namespace}span-10of12
    .#{$namespace}span-11of12

Grid modules have a default width of 100%. The `.span-full` class is also available should you need a grid module to span the full width of your grid at any given breakpoint

	.{$namespace}-span-full

## Proportional "push" and "pull" classes

Proportional "push" and "pull" classes are availble.
- Push classes nudge grid modules to the left by a certain proportion
- Pull classes nudge grid modules to the right by a certain proportion

Used in conjuction with grid classes, these allow for more complex content choreography. Your layout can diverge a little bit more from source order at non default screen sizes. The demo uses "push" an "pull" classes in conjucntion with one another.

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

When defining a breakpoint, you can prevent it from beeing used to generate grids and namespaced (silent) grid classes. Just set the third parameter in the sass list defintion in `_variables.scss` to `false`

    $breakpoints:(
        "below-medium"   "(min-width:1em) and (max-width:46.875em)"   false,
        "medium"         "(min-width:46.875em)"                       true,
        "large"          "(min-width:71.25em)"                        true
    )!default;

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

The concept of [content choreography](http://trentwalton.com/2011/07/14/content-choreography/) is important with RWD projects. The demo includes a small example in the footer, with the first module beeing above the five others at large screen sizes.