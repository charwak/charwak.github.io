---
title: "Stories"
layout: archive
permalink: "/stories/"
author_profile: true
header:
  image: "/images/fort point.png"
---

Lorem ipsum dolor sit amet consectetur adipiscing elit sollicitudin nunc, quam id libero suscipit fusce mauris eleifend venenatis velit tellus, ornare ut sagittis in senectus lacus nulla tristique. Aptent adipiscing eget mollis morbi cum platea parturient, massa per viverra tellus dictumst torquent, quisque feugiat conubia iaculis diam vulputate. Vulputate taciti facilisi elit ridiculus vitae id curae nullam habitasse, integer metus lectus dignissim natoque curabitur massa sapien, nam odio scelerisque per enim fringilla cubilia elementum. Hac consectetur elit potenti aenean viverra nibh ipsum, mattis facilisi enim vel odio nullam commodo tristique, in himenaeos bibendum eget primis suscipit.

Pulvinar accumsan iaculis porta tempus convallis hendrerit, interdum cras fermentum urna sem sodales, suspendisse ac ligula vitae imperdiet. Metus aenean pretium vitae ullamcorper eget mus diam euismod rhoncus netus, penatibus felis orci eleifend facilisi urna justo fames tempus lobortis lacus, sem vivamus nibh sociis ridiculus augue condimentum nam rutrum. Malesuada consectetur libero curabitur parturient leo proin convallis, pulvinar class sed ipsum facilisi fames, sodales sagittis sociis integer suscipit pellentesque. Curae molestie condimentum blandit elementum augue hendrerit, vivamus justo erat tempor class. Ante aliquam sodales conubia nostra dui sociis iaculis sollicitudin, platea a dis facilisis varius euismod pretium ultrices, velit mauris hendrerit curae ipsum vel ad.

Eget sit purus potenti dictum nibh feugiat lobortis risus fermentum, erat commodo accumsan laoreet cubilia facilisis odio ipsum nascetur elit, porta donec luctus ligula nisi magna diam condimentum. Sollicitudin orci sociosqu ad id consequat torquent libero diam, duis augue condimentum enim nisl ullamcorper sapien, elit ipsum nascetur fusce lacus habitant sem. Tristique vel nisl lacus a pharetra eros dignissim aliquam fames erat nascetur ultrices, tellus arcu senectus pretium eleifend cum laoreet bibendum urna cursus in hendrerit, et facilisis maecenas ornare mattis etiam massa risus dapibus morbi semper. Laoreet facilisi vel vivamus nam augue torquent pretium odio est, primis ad iaculis sapien velit convallis viverra lacus congue, malesuada egestas scelerisque auctor maecenas mus urna platea.


<style>

.node {
  stroke: #fff;
  stroke-width: 1.5px;
}

.link {
  stroke: #999;
  stroke-opacity: .6;
}

</style>

<div id='d3div'></div>

<script src="//d3js.org/d3.v3.min.js"></script>
<script>

var width = $("#d3div").width(),
    height = 500;

var color = d3.scale.category20();

var force = d3.layout.force()
    .charge(-120)
    .linkDistance(30)
    .size([width, height]);

var svg = d3.select("#d3div").append("svg")
    .attr("width", width)
    .attr("height", height);

d3.json("../../../../scripts/miserables.json", function(error, graph) {
  if (error) throw error;

  force
      .nodes(graph.nodes)
      .links(graph.links)
      .start();

  var link = svg.selectAll(".link")
      .data(graph.links)
    .enter().append("line")
      .attr("class", "link")
      .style("stroke-width", function(d) { return Math.sqrt(d.value); });

  var node = svg.selectAll(".node")
      .data(graph.nodes)
    .enter().append("circle")
      .attr("class", "node")
      .attr("r", 5)
      .style("fill", function(d) { return color(d.group); })
      .call(force.drag);

  node.append("title")
      .text(function(d) { return d.name; });

  force.on("tick", function() {
    link.attr("x1", function(d) { return d.source.x; })
        .attr("y1", function(d) { return d.source.y; })
        .attr("x2", function(d) { return d.target.x; })
        .attr("y2", function(d) { return d.target.y; });

    node.attr("cx", function(d) { return d.x; })
        .attr("cy", function(d) { return d.y; });
  });
});

</script>
