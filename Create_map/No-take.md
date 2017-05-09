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
Check out the No-take zone! The color is black as default setting. 
![result 1](http://i.imgur.com/GluEpvA.png)


## Style No-take Zone
Black is not very appealing in the map. I added different color in CSS style to make No-take zone looks more obvious. 
<pre>
.noTakeZone{fill:#e85a71; opacity:.75;}
</pre>
![result 2](http://i.imgur.com/CRJzi6M.png)

The [next step](Realtime_data) is to add real-time vessel location to our map.
