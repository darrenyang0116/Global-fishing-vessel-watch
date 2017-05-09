In the [previous step](Access_data), we have learned how to get access to data points from [My Ship Tracking](http://www.myshiptracking.com/) and draw vessel locations. In this step, I will teach you how to animate the data point by [D3](https://d3js.org) when clicking countries.

## D3 transition
D3 enables us to easily visual animate elements in the worldmap. In our case, I want users to be able to click country and see where are the location of its vessels. Let's take USA for example.

<br />

Do you remember how we [drew the worldmap](https://github.com/darrenyang0116/Global-fishing-vessel-watch/blob/master/Create_map/D3.md) in the previous step? We are going to add mroe lines of code under it, so when users click any country, thry are able to see its vessel location.
<pre>
d3.json("worldmap.json", function(error, geojson) {
       g.selectAll(path.country)
        .data(geojson.features)
	.enter()
	.append("path")
	.attr("d", path)
	.classed("country", true)
	;
});
.on("mouseover", function(d){
	tooltip
	.text(d.properties.name)//inside dispute.json, we are looking for BRK_NAME	
	.attr("x", (d3.event.pageX-80)+"px") //px is pixel
	.attr("y", (d3.event.pageY-30)+"px")
	.transition()//animate
	.duration(300)
	.attr("fill-opacity", "1")
	})

.on("mouseout", function(d){
	tooltip
	.transition()
	.duration(300)
	.attr("fill-opacity","0")
	})

</pre>


<pre>
//change color by changing class ".country" to id "#cSelected" when click
.on("click", function(d){
	g.selectAll("#cSelected")
	.attr("id","unSelected"); // because "unSelected" is not defined, so it will go back to default class "country"
this.setAttribute('id', 'cSelected');

if (d.properties.name == "USA"){
	g.selectAll("circle.USA")
	.style("stroke", function(d){
		if (d.TYPE==10) {return "fed4b8"} 
		else {return "#87ffeb"}
		})
	.style("stroke-width", 0.5)
	.style("fill-opacity", function(d){
		if (d.TYPE == 10){return "1"} 
		else {return ".2"}
		})
	.style("stroke-opacity", function(d){
		if (d.TYPE == 10){return "1"} 
		else {return ".15"}
		})
</pre>
	.transition()
	.duration(100)
	.attr("r", 5)
	.transition()
	.duration(100)
	.attr("r", function(d){
		if (d.TYPE == 10){return "3"} 
		else {return "3"}
		})
}      		
else{
	g.selectAll("circle.USA")
	.style("fill-opacity",function(d){
		if (d.TYPE==10) {return ".15"} 
		else {return ".05"}
		})	 
	.style("stroke-width", 0)
}

            });


			var tooltip = d3.select("g")
							.append("text")
							.attr("fill-opacity", "0")
							.text("tooltip!")
							.classed("tooltip",true)
							;

	});
</pre>
