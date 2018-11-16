
title:svg basic shapes using d3.js

We can then make the process of drawing a circle as two step process:
1. Make an SVG container (the SVG Coordinate Space).
2. Draw the circle

HTML file contains -

  <svg width="50" height="50">
    <circle cx="25" cy="25" r="25" fill="purple" />
  </svg>
  
When there is JSON data, our javascript file would look like this:

var jsonCircles = [
   { "x_axis": 30, "y_axis": 30, "radius": 20, "color" : "green" },
   { "x_axis": 70, "y_axis": 70, "radius": 20, "color" : "purple"},
   { "x_axis": 110, "y_axis": 100, "radius": 20, "color" : "red"}];
 
var svgContainer = d3.select("body").append("svg")
                                     .attr("width", 200)
                                     .attr("height", 200);
 
var circles = svgContainer.selectAll("circle")
                          .data(jsonCircles)
                          .enter()
                          .append("circle");

var circleAttributes = circles
                       .attr("cx", function (d) { return d.x_axis; })
                       .attr("cy", function (d) { return d.y_axis; })
                       .attr("r", function (d) { return d.radius; })
                       .style("fill", function(d) { return d.color; });

So in the simplest case, our JavaScript code would look like:

//Make an SVG Container
var svgContainer = d3.select("body").append("svg")
                                    .attr("width", 200)
                                    .attr("height", 200);
 
 //Draw the Circle
 var circle = svgContainer.append("circle")
                          .attr("cx", 30)
                          .attr("cy", 30)
                          .attr("r", 20);

The necessary SVG attributes for drawing a circle are the "cx", "cy" and "r".

Note - If we leave off the style method, then we get a black circle. Which is fine, we care about making a circle first and foremost, 
then after that we can style it.

Notice that the important attributes we need to draw an SVG Circle in D3.js are - cx, cy and r.

*************************************************************************************************************************************
Drawing an SVG Rectangle using D3.js

<svg width="50" height="50">
  <rect x="0" y="0" width="50" height="50" fill="green" />
</svg>

We will need an "x", "y", "width" and "height".

We can then make the process of drawing a rectangle as two step process:
1) Make an SVG container (the SVG Coordinate Space)
2) Draw the rectangle

So in the simplest case, our JavaScript code would look like:

 //Make an SVG Container
 var svgContainer = d3.select("body").append("svg")
                                     .attr("width", 200)
                                     .attr("height", 200);
 
 //Draw the Rectangle
 var rectangle = svgContainer.append("rect")
                             .attr("x", 10)
                             .attr("y", 10)
                             .attr("width", 50)
                             .attr("height", 100);

The necessary SVG attributes for drawing a rectangle are the "x", "y", "width" and "height".

Two important things to pay attention to

1. The SVG word for rectangle is rect. Which makes the append operator .append("rect") not .append("rectangle").
2. The SVG Coordinate system is in place so the height starts from the TOP and moves down.

Notice that the important attributes we need to draw an SVG Rectangle in D3.js are - x, y, width and height.
