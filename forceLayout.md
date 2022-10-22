# Force Layout

## Force Layout properties

### Layout force

```javascript
//Set up the force layout
var force = d3.layout.force()
    .charge(-120)
    .linkDistance(30)
    .size([width, height]);
```

The force layout **d3.layout.force** has been renamed to **d3.forceSimulation**.

```javascript
const simulation = d3.forceSimulation()
                    .force('charge', d3.forceManyBody().strength(-20)) 
                    .force('center', d3.forceCenter(width / 2, height / 2))
```

```javascript
var simulation = d3.forceSimulation()
    .force("link", d3.forceLink().id(function(d) { return d.id; }))
    .force("charge", d3.forceManyBody().strength(-20))
    .force("center", d3.forceCenter(width / 2, height / 2));
```

```javascript
var edge = svg.append("g")
              .attr("class", "edges")
              .selectAll("line")
              .data(graph.edges)
              .enter().append("line")
              .attr("stroke-width", function(d) { return Math.sqrt(d.value); });
```

```javascript
// d3js v7
var node = svg.append("g")
                .attr("class", "nodes")
                .selectAll("circle")
                .data(graph.nodes)
                .enter().append("circle")
                .attr("r", 5)
                .attr("fill", function(d) { return color(d.group); })
                .call(d3.drag()
                .on("start", dragstarted)
                .on("drag", dragged)
                .on("end", dragended));
```

```javascript
// d3js v3
var node = svg.selectAll(".node")
                      .data(graph.nodes)
                      .enter().append("circle")
                      .attr("class", "node")
                      .attr("r", 8)
                      .style("fill", function (d) {return color(d.group);})
                      .call(force.drag); 
```

```javascript
  node.append("title")
      .text(function(d) { return d.id; });
```

```javascript
  simulation
      .nodes(graph.nodes)
      .on("tick", ticked);

  simulation.force("link")
      .links(graph.links);
```

```javascript
  function ticked() {
    link
        .attr("x1", function(d) { return d.source.x; })
        .attr("y1", function(d) { return d.source.y; })
        .attr("x2", function(d) { return d.target.x; })
        .attr("y2", function(d) { return d.target.y; });

    node
        .attr("cx", function(d) { return d.x; })
        .attr("cy", function(d) { return d.y; });
  }
```

```javascript
//Now we are giving the SVGs co-ordinates - the force layout is generating the co-ordinates which this code is using to update the attributes of the SVG elements
force.on("tick", function () {
    edge.attr("x1", function (d) {return d.source.x;})
        .attr("y1", function (d) {return d.source.y;})
        .attr("x2", function (d) {return d.target.x;})
        .attr("y2", function (d) {return d.target.y;});

    node.attr("cx", function (d) {return d.x;})
        .attr("cy", function (d) {return d.y;});
});
```

### Drag functions

```javascript
function dragstarted(d) {
  if (!d3.event.active) simulation.alphaTarget(0.3).restart();
  d.fx = d.x;
  d.fy = d.y;
}

function dragged(d) {
  d.fx = d3.event.x;
  d.fy = d3.event.y;
}

function dragended(d) {
  if (!d3.event.active) simulation.alphaTarget(0);
  d.fx = null;
  d.fy = null;
}
```


### Links or Edges

This is a feature of force simulations are connecting nodes.

```javascript
//Creates the graph data structure out of the json data
force.nodes(graph.nodes)
    .links(graph.links)
    .start();
```

## Force Layout parameters 

### size

### Charge

### link distance

## Node parameters

### Color

**d3.scaleOrdinal** creates an ordinal scale, with an empty domain and an empty range. It won’t do much unless we give it some values it can output — which we can do by specifying scale.range — or by using the shorthand notation **d3.scaleOrdinal(range)**

Ordinal coloring scale, using the standard color scheme d3.schemeCategory10. Ordinal.domain sets or reads the scale’s domain. (Caveat: the domain must be composed of numbers or strings, not objects.)
