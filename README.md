# NBA Snapshot

## Overview
[NBA Snapshot](https://alvink92.github.io/nba-snapshot/) is an interactive visualization users can use to explore and break down in-game player to team contributions for the selected game id.

![](https://github.com/alvink92/nba-snapshot/blob/master/docs/images/example.png)

## Features
- Two sunburst plots, one for each team
- Animated zoom was implemented using d3's interpolation techniques
```javascript
function click(d) {
  svg
    .transition()
    .duration(750)
    .tween("scale", function() {
      var xd = d3.interpolate(x.domain(), [d.x0, d.x1]),
        yd = d3.interpolate(y.domain(), [d.y0, 1]),
        yr = d3.interpolate(y.range(), [d.y0 ? 20 : 0, radius]);

      return function(t) {
        x.domain(xd(t));
        y.domain(yd(t)).range(yr(t));
      };
    })
    .selectAll("path")
    .attrTween("d", function(d) {
      return function() {
        return arc(d);
      };
    });
}
```

## Instructions
The basic layout is broken into two sunbursts where team 1 is represented by the left-side sunburst and team 2 is represented by the right-side sunburst. Hovering over nodes of the sunburst will active the breadcrumbs on the top, showing raw and percentage contributions to the chosen statistic. Clicking a node will zoom in and focus in the sunburst to the node so users can more deeply analyze the breakdown of select node and it's children nodes.

## Technologies
  * D3.js
  * jQuery
  * HTML5
  * CSS


## Todos
  * Dynamically able to search for game by ID and make API request to update charts
  * Possibly change sunburst's onHover to onClick and onClick to onDoubleClick to be able cache any depth of breadcrumb instead of just the deepest level
  * Specify what category is selected and implement ability to specify what category for sunburst's to represent(right now it's just points)
  * Add a meter to visually display which team won specified category
