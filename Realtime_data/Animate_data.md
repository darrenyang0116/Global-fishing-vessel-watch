In the [previous step](Access_data), we have learned how to get access to data points from [My Ship Tracking](http://www.myshiptracking.com/) and draw vessel locations. In this step, I will teach you how to animate the data point by [D3](https://d3js.org) when clicking countries.

## D3 transition
D3 enables us to easily visual animate elements in the worldmap. In our case, I want users to be able to click country and see where are the location of its vessels. Let's take USA for example.

<br />

Remember how do we [draw the worldmap](D3.md)? in the Add style the vessel 

<pre>
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
</pre>
