
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

********************************************************************************************************************
Drawing an SVG Straight Line using D3.js

<svg width="50" height="50">
 <line x1="5" y1="5" x2="40" y2="40" stroke="gray" stroke-width="5"  />
</svg>

We can probably guess that to build a straight line, you will need a "x1", "y1", "x2" and "y2".

We can then make the process of drawing a straight line as two step process:
1) Make an SVG container (the SVG Coordinate Space)
2) Draw the straight line

So in the simplest case, our JavaScript code would look like:

//Make an SVG Container
 var svgContainer = d3.select("body").append("svg")
                                     .attr("width", 200)
                                     .attr("height", 200);
 
 //Draw the line
 var circle = svgContainer.append("line")
                          .attr("x1", 5)
                          .attr("y1", 5)
                         .attr("x2", 50)
                         .attr("y2", 50);
(Wait a second?! Where is the line????? The SVG element is there, however we cannot see it in our browser.
It turns out because the SVG ‘line’ elements are single lines and thus are geometrically one-dimensional, that is - they have no interior.

Which means that ‘line’ elements are never filled (see the ‘fill’ property).
Which means that our line does not take up space - so we do not actually see anything.

To fix this, make sure to give the line:

.attribute("stroke-width", NUMBER), where NUMBER is how wide the line is in units.
.attribute("stroke", "COLOR"), where COLOR is a color to used to color the line.

So fixing our simplest case, our JavaScript code would look like:
        //Make an SVG Container
 var svgContainer = d3.select("body").append("svg")
                                     .attr("width", 200)
                                     .attr("height", 200);
 
 //Draw the line
 var circle = svgContainer.append("line")
                          .attr("x1", 5)
                          .attr("y1", 5)
                         .attr("x2", 50)
                         .attr("y2", 50)
                         .attr("stroke-width", 2)
                         .attr("stroke", "black");

Fantastic - now the line is visible!

The necessary SVG attributes for drawing a straight line are the "x1", "y1", "x2", "y2", "stroke" and "stroke-width".
Note - We do not use a style method with the line. Because ‘line’ elements are single lines and thus are geometrically one-dimensional, 
       they have no interior. 
Which is why to style them we need to deal with the "stroke" color and "stroke-width".
Notice that the important attributes we need to draw an SVG Straight Line in D3.js are - x1, y1, x2, y2, stroke-width and stroke.

****************************************************************************************************************************************
Drawing Polyline & Polygon SVG Basic Shapes using D3.js

Polyline Example & Code:

<svg width="50" height="50">
   <polyline fill="none" stroke="blue" stroke-width="2"
     points="05,30
             15,30
             15,20
             25,20
             25,10
             35,10" />
 </svg>

Polygon Example & Code:

<svg width="50" height="50">
  <polygon fill="yellow" stroke="blue" stroke-width="2"
    points="05,30
            15,10
            25,30" />
</svg>

Using the Circle, Rectangle, Ellipse, and Straight Line examples, you can probably guess that to
  build a Polyline and Polygon, you will need a "stroke", "stroke-width" and "points". And "fill" for the Polygon.

However, as you can see from the examples above - the points attribute contains a list of points 
  where the x and y are separated by comas and different x and y coordinates are separated by spaces.

Building this out easily in D3.js is not pretty. Because D3.js loves data visualization and pretty things, 
  the D3.js convention is to use the D3.svg.line() generator for polylines and polygons.
  
  
*****************************************************************************************************************************
More Information
https://www.dashingd3js.com/svg-basic-shapes-and-d3js

