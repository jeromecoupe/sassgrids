# Sass grids

Simple experiment to create grids in Sass

## Goals

I wanted a simple and quick way to design responsive grids in Sass so I built this little set of mixins that allow you to use namespaced classes and silent Sass selectors to create a mobile first grid very rapidly. Set goals:

- Responsive
- Mobile First
- Infinitely Nestable
- No .alpha or .omega classes to worry about
- Use proportional grids
- Mix a fluid grid with fixed gutters

## Demo

[Here is a small demo](http://jeromecoupe.github.io/sassgrids/) of a grid in action.
You can have a look at a sample SCSS file in the [gh-pages branch](https://github.com/jeromecoupe/sassgrids/tree/gh-pages) of this repo where the demo lives.

- The grid in the demo uses a nested grid along with "push" and "pull" classes
- The demo makes use of [modernizr.js](http://www.modernizr.com) / [respond.js](https://github.com/scottjehl/Respond) / [selectivizr.js](https://github.com/keithclark/selectivizr) to show support for IE8

## Usage

1. Import SCSS files
2. Define your gutters, breakpoints and namespaces
3. Use namespaced silent classes in your SCSS
4. Defined media queries and breakpoints can also be used "normally" in your Sass file

## Example: simple grid

### HTML

Since this is using inline-block and not floats, comments must be in there to alleviate the fact that [many browsers account for white-space between inline-block elements](http://css-tricks.com/fighting-the-space-between-inline-block-elements/).

	<div class="page">
		<div class="content-primary">
			<p>Primary Content</p>
		</div><!--

	 --><div class="content-secondary">
	 		<p>Secondary Content</p>
		</div>
	</div>

Benefits of using inline-block

- more flexible than floats in a responsive grid context
- no clearing to worry about
- no float drops

### SCSS

Provided you have defined two breakpoints and prefixed / namespaced one as "medium" and the other one as "large"

	.content-primary
	{
		@extend %grid-module;		// define as grid module
		@extend %medium-span-2of3;	// span 2/3 of its parent's width (medium breakpoint)
		@extend %large-span-7of12;	// span 7/12 of its parent's width (large breakpoint)
	}

	.content-secondary
	{
		@extend %grid-module;		// define as grid module
		@extend %medium-span-1of3;	// span 1/3 of its parent's width (medium breakpoint)
		@extend %large-span-5of12;	// span 5/12 of its parent's width (large breakpoint)
	}

## Available silent classes and proportions

The following silent classes are created for each media queries and namespaces you have created. We are talking about proportional grids so these classes mean "spanning [proportion] of its parent's width".

    %#{$namespace}span-1of2

    %#{$namespace}span-1of3
    %#{$namespace}span-2of3

    %#{$namespace}span-1of4
    %#{$namespace}span-2of4
    %#{$namespace}span-3of4

    %#{$namespace}span-1of5
    %#{$namespace}span-2of5
    %#{$namespace}span-3of5
    %#{$namespace}span-4of5

    %#{$namespace}span-1of6
    %#{$namespace}span-2of6
    %#{$namespace}span-3of6
    %#{$namespace}span-4of6
    %#{$namespace}span-5of6

    %#{$namespace}span-1of8
    %#{$namespace}span-2of8
    %#{$namespace}span-3of8
    %#{$namespace}span-4of8
    %#{$namespace}span-5of8
    %#{$namespace}span-6of8
    %#{$namespace}span-7of8

    %#{$namespace}span-1of10
    %#{$namespace}span-2of10
    %#{$namespace}span-3of10
    %#{$namespace}span-4of10
    %#{$namespace}span-5of10
    %#{$namespace}span-6of10
    %#{$namespace}span-7of10
    %#{$namespace}span-8of10
    %#{$namespace}span-9of10

    %#{$namespace}span-1of12
    %#{$namespace}span-2of12
    %#{$namespace}span-3of12
    %#{$namespace}span-4of12
    %#{$namespace}span-5of12
    %#{$namespace}span-6of12
    %#{$namespace}span-7of12
    %#{$namespace}span-8of12
    %#{$namespace}span-9of12
    %#{$namespace}span-10of12
    %#{$namespace}span-11of12

Grid modules have a default width of 100%. The %span-full class is also available should you need a grid module to span the full width of your grid at any given breakpoint

	%{$namespace}-span-full

## Proportional "push" and "pull" classes

Proportional "push" and "pull" classes are availble.
- Push classes nudge grid modules to the left by a certain proportion
- Pull classes nudge grid modules to the right by a certain proportion

Used in conjuction with grid classes, these allow for more complex content choreography. Your layout can diverge a little bit more from source order at non default screen sizes. The demo uses "push" an "pull" classes in conjucntion with one another.

    .content-primary
    {
        @extend %grid-module;       // define as grid module
        @extend %medium-span-2of3;  // span 2/3 of its parent's width (medium breakpoint)
        @extend %large-span-7of12;  // span 7/12 of its parent's width (large breakpoint)
        @extend %large-push-5of12;  // push 5/12 = width of .content-secondary (large breakpoint)
    }

    .content-secondary
    {
        @extend %grid-module;       // define as grid module
        @extend %medium-span-1of3;  // span 1/3 of its parent's width (medium breakpoint)
        @extend %large-span-5of12;  // span 5/12 of its parent's width (large breakpoint)
        @extend %large-pull-7of12;  // pull 7/12 = width of .content-primary (large breakpoint)
    }

Essentially, this visually swaps `.content-primary` and `.content-secondary` at large screen sizes, giving us a bit more flexibility in regards to HTML source order.

## Using defined breakpoints and media-queries in your SCSS

Obviously, you can also use defined breakpoints and media-queries in your SCSS files for something else than layout / grids

	body
	{
		background:#fff;
		@include mq(large)
		{
			background:#ccc;
		}
	}

## Shoutouts

### Harry Roberts

If you need a solid Sass framework, check out [inuit.css](http://inuitcss.com/) and [csswizardry-grids](https://github.com/csswizardry/csswizardry-grids). These were a huge inspiration for this and I share a lot of [Harry's views on proportional grids and namespaced classes](http://csswizardry.com/2013/02/responsive-grid-systems-a-solution/).

However, there were a few things that prompted me to create my own thing:

- the grid layout (gutters = number columns - 1) was not inuitive to me, I prefer to have even padding on each side of my modules.
- Harry's system, albeit simpler than many others I have seen, caters for many use cases that I don't need (silent classes or not, etc.). Buy developing my own thing, I could make it simpler and adapt it more easily to each project
- I wanted to understand this fully and it was a good excuse to learn some Sass

### Chris Coyier

Nice article on [how to handle white-space when using inline-block](http://css-tricks.com/fighting-the-space-between-inline-block-elements/) over at CSS-tricks

### Paul Irish

Using box-sizing:border-box; on elements [allows you to use percentage width coupled with fixed value padding / margins](http://paulirish.com/2012/box-sizing-border-box-ftw/).

### Trent Walton

The concept of [content choreography](http://trentwalton.com/2011/07/14/content-choreography/) is important with RWD projects. The demo includes a small example in the footer, with the first module beeing above the five others at large screen sizes.