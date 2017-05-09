In the [previous step](Choose_data.md), we choose [My Ship Tracking](http://www.myshiptracking.com/) to pull in our dataset. Now we need to get access to the dataset and use in our code.

## Region setting
We can construct queries with a latlong bounding box, but it will return null if the bounding box exceeds ~20 degrees each of latitude and longitude. Let's use the west coast of USA for example.
<pre>
var minlat = 10;
var maxlat = 30;
var minlon = -145;
var maxlon = -120;
</pre>


## Access to data
The site constructs data requests like this:
<pre>
http://www.myshiptracking.com/requests/vesselsonmap.php?type=json&minlat=10&maxlat=30&minlon=-145&maxlon=-125&zoom=7
</pre>

Use above request in our code to draw vessel.
<pre>
//Undocumented API Notes
//d.MMSI = Unique Identifier with Embedded Country (https://help.marinetraffic.com/hc/en-us/articles/205220087-Which-way-is-information-on-a-vessel-s-flag-found-)
//d.NAME = Vessel Name
//d.SOG = Speed in Knots
//d.COG = Heading in Clockwise Degrees (0 = North; 90 = West...)
//d.DEST = Destination Port
//d.TYPE = Vessel Type (7=Vehicle Carrier, 8:Tanker...)
//d.LAT = Current Latitude
//d.LNG = Current Longitude
//d.ARV = Projected Arrival Time, 201704272230 is 10:30PM on April 27, 2017 GMT

//draw real-time boats
d3.json("http://www.myshiptracking.com/requests/vesselsonmap.php?type=json&minlat=" + minlat + "&maxlat=" + maxlat + "&minlon=" + minlon + "&maxlon=" + maxlon + "&zoom=7", function(err, boats){
	console.log(boats)
	g.selectAll("circle.vessel")
	.data(boats[0].DATA)
	.enter()
	.append("circle")
	.attr("transform", function(d) {return "translate(" + projection([d.LNG, d.LAT]) + ")";})
	.attr("r",2)
	.style("fill", function(d){if (d.TYPE == 10){return "#e47a33"} else {return "#018771"}})
	.style("fill-opacity", function(d){if (d.TYPE == 10){return "0.15"} else {return ".05"}})
	.classed("vessel", true)
	.attr("class", function(d){
		var mmsi = d.MMSI;  var countrycode = mmsi.slice(0,3);
		if ((countrycode == 303) || (countrycode == 338) || (countrycode >= 366 && countrycode <= 369)) {return "USA" }
		else{return countrycode}
		})
	.on("mouseover", function(d){
		tooltipBoat.text("Name: " + d.NAME + " | Heading: " + d.DEST + "| MMSI: " + d.MMSI)
		.attr("y", (d3.event.pageY)+"px")
		.attr("x",(d3.event.pageX)+"px")
		.transition()
		.duration(500)
		.attr("fill-opacity", "1")
		;
		})
	.on("mouseout", function(d){
		tooltipBoat
		.transition()
		.duration(500)
		.attr("fill-opacity", "0")
		})
	});

//make tooltip container
var tooltipBoat = d3.select("svg")
.append("text")
.attr("fill-opacity", "0")
.text("tooltip!")
.classed("tooltipBoat", true);
</pre>
