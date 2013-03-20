# SASS grids

Simple experiment to create grids in SASS

# Goals

I wanted a simple and quick way to design responsive grids in SASS so I built this little set of mixins that allow you to use namespaced classes and silent SASS selectors to create a mobile first grid very rapidly. Set goals:

- Responsive
- Mobile First
- Infinitely Nestable
- No .alpha or .omega classes to worry about
- Use proportional grids
- Mix a fluid grid with fixed gutters
- Be able to apply a backgrounds to grid modules directly

# Demo

[Here is a small demo](http://jeromecoupe.github.com/sassgrids/) of a grid in action.

A **sample scss** file is included in the gh-pages branch of this repo where the demo lives.

1. Import _grid.scss in your scss file
2. Define your gutter, breakpoints and namespaces
3. Use namespaced silent classes in your scss
4. Defined media queries and breakpoints can also be used "normally" in your SASS file

## Example of a simple grid

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

### SCSS

Provided you have defined two breakpoints and prefixed / namespaced one as "medium" and the other one as "large"

	.content-primary
	{
		@extend %grid-module; // define as grid module
		@extend %medium-span-2of3; // span two third of its parent's width at medium screen sizes
		@extend %large-span-7of12; // span seven twelfths of its parent's width at large screen sizes
	}

	.content-secondary
	{
		@extend %grid-module; // define as grid module
		@extend %medium-span-1of3; // span one third of its parent's width at medium screen sizes
		@extend %large-span-5of12; // span five twelfths of its parent's width at large screen sizes
	}

### Available silent classes and proportions

The following silent classes are created for each media queries and namespaces you have created.
Remember that we are talking about proportional grids. Each of these classes mean "spanning [proportion] of its parent's width"

	%{$namespace}-span-1of3
	%{$namespace}-span-2of3
	%{$namespace}-span-1of4
	%{$namespace}-span-2of4
	%{$namespace}-span-3of4
	...
	%{$namespace}-span-11of12

Grid modules have a default width of 100%. The %span-full class is also available should you need a grid module to span the full width of your grid at any given breakpoint

	%{$namespace}-span-full

### Using defined breakpoints and media-queries in your SCSS

Obviously, you can also use defined breakpoints and media-queries in your SCSS files for something else than layout / grids

	body
	{
		background:#fff;
		@include mq(large)
		{
			background:#ccc;
		}
	}

# References

## Harry Roberts

If you need a solid SASS framework, check out [inuit.css](http://inuitcss.com/) and [csswizardry-grids](https://github.com/csswizardry/csswizardry-grids). These were a huge inspiration for this and I share a lot of [Harry's views on proportional grids and namespaced classes](http://csswizardry.com/2013/02/responsive-grid-systems-a-solution/).

However, there were two things that didn't quite suit my workflow:

- you have to use nested elements to apply backgrounds to grid modules
- the grid layout (gutters = number columns - 1) was not inuitive to me, I prefer to have even padding on each side of my modules.

## Chris Coyier

Nice article on [how to handle white-space when using inline-block](http://css-tricks.com/fighting-the-space-between-inline-block-elements/) over at CSS-tricks

## Paul Irish

Using box-sizing:border-box; on elements [allows you to use percentage width coupled with fixed value padding / margins](http://paulirish.com/2012/box-sizing-border-box-ftw/).

## Trent Walton

The concept of [content choreography](http://trentwalton.com/2011/07/14/content-choreography/) is important with RWD projects. The demo includes a small example in the footer, with the first module beeing above the five others at large screen sizes.