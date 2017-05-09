In the [previous step](Access_data), we have learned how to get access to data points from [My Ship Tracking](http://www.myshiptracking.com/) and draw vessel locations. In this step, I will teach you how to animate the data point by [D3](https://d3js.org) when clicking countries.

## D3 transition
D3 enables us to easily visual animate elements in the worldmap. In our case, I want users to be able to click country and see where are the location of its vessels. Let's take USA for example.

<br />

Do you remember how we [drew the worldmap](https://github.com/darrenyang0116/Global-fishing-vessel-watch/blob/master/Create_map/D3.md) in the previous step? We are going to add mroe lines of code under it, so when users click any country, thry are able to see its vessel location.

## Add CSS style to country and text
<pre>
.country:hover{fill:white; stroke:#fff; stroke-width:.25px; opacity:.2;}
.country{fill:#0B121F; opacity:0.45; stroke:#203a53; stroke-width:1.5px;}
#cSelected{fill:#0B121F; opacity:0.8; stroke:#537483; stroke-width:2px;}
text.tooltip {fill:white; font-family: frutiger; font-size: 12px;}  
</pre>

<br />

## Add country text when mouseover
<pre>
d3.json("worldmap.json", function(error, geojson) {
       g.selectAll(path.country)
        .data(geojson.features)
	.enter()
	.append("path")
	.attr("d", path)
	.classed("country", true)
	.on("mouseover", function(d){
		tooltip
		.text(d.properties.name)//inside worldmap.json, we are looking for country name	
		.attr("x", (d3.event.pageX-80)+"px") //event means mouse event, px is pixel
		.attr("y", (d3.event.pageY-30)+"px")
		.transition() //add animation
		.duration(300) //0.3 seconds
		.attr("fill-opacity", "1") //show text
		})

	.on("mouseout", function(d){
		tooltip
		.transition()
		.duration(300)
		.attr("fill-opacity","0") //hide text
		})
</pre>

![Mouseover](http://i.imgur.com/s0b26eW.png)

<br />

## Show vessel location when clicking country
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

