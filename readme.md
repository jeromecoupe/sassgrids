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

[Here is a small demo](http://jeromecoupe.github.com/sassgrids/) of a grid in action

# References

## Harry Roberts

If you need a solid SASS framework, check out [inuit.css](http://inuitcss.com/) and [csswizardry-grids](https://github.com/csswizardry/csswizardry-grids). These were a huge inspiration for this and I share a lot of [Harry's views on proportional grids and namespaced classes](http://csswizardry.com/2013/02/responsive-grid-systems-a-solution/).

However, there were two things that didn't quite suit my workflow:

- use nested elements to apply backgrounds to grid modules
- the grid layout (gutters = number columns - 1) was not inuitive to me, I prefer to have even padding on each side of my modules.

## Chris Coyier

Nice article on [how to handle white-space when using inline-block](http://css-tricks.com/fighting-the-space-between-inline-block-elements/) over at CSS-tricks

## Paul Irish

Using box-sizing:border-box; on elements [allows you to use percentage width coupled with fixed value padding / margins](http://paulirish.com/2012/box-sizing-border-box-ftw/).