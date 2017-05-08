## Download No-take Zone file

Global Fishing Watch uses No-take zone data from [MPAtlas](http://mpatlas.org/data/), you can download the file first. 


## Draw No-take Zone
We can draw No-take zone with D3 as we drew the worldmap. 

<pre>
d3.json("noTakeZone.json", function(error, geojson) {

		   g.selectAll("path.noTakeZone")
			    .data(geojson.features)
			    .enter()
			    .append("path")
			    .attr("d", path)
			    .classed("noTakeZone", true)
			    .on("mouseover", function(d){
					if (d.properties.designation_eng == ""){
						var engdes = "Protected Area";
					}
					else{
						var engdes = d.properties.designation_eng;
					}

					if (d.properties.no_take_area == null){
						var notake = "Status Unknown";
					}
					else{
						var notake = d.properties.no_take_area + "km^2";
					}


					tooltip.text(
							d.properties.name + " | " + engdes + " | " + "No-Take Area: " + notake
						)
						.attr("y", (d3.event.pageY)+"px")
						.attr("x",(d3.event.pageX)+"px")
						.transition()
						.duration(500)
						.attr("fill-opacity", "1")
					;

				})
				.on("mouseout", function(d){
					tooltip
					.transition()
					.duration(500)
					.attr("fill-opacity", "0")
				})
				
				;


				//make tooltip container
				var tooltip = d3.select("svg")
				.append("text")
				.attr("fill-opacity", "0")
				.text("tooltip!")
				.classed("tooltip", true);

	});
</pre>

## Style No-take Zone
<pre>
</pre>
