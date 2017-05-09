In the [previous step](Choose_data.md), we choose [My Ship Tracking](http://www.myshiptracking.com/) to pull in our dataset. Now we need to get access to the dataset and use in our code.

## Region setting
We can construct queries with a latlong bounding box, but it will return null if the bounding box exceeds ~20 degrees each of latitude and longitude. Let's use the west coast of USA for example.

<pre>
var minlat = 10;
var maxlat = 30;
var minlon = -145;
var maxlon = -120;
</pre>

<br />

## Access to data
The site constructs data requests like this:
<pre>
http://www.myshiptracking.com/requests/vesselsonmap.php?type=json&minlat=10&maxlat=30&minlon=
-145&maxlon=-125&zoom=7
</pre>

<br />

Use above request in our code to draw vessel.
<pre>
//Undocumented API Notes
//d.MMSI = Unique Identifier with Embedded Country (https://help.marinetraffic.com/hc/en-us/
articles/205220087-Which-way-is-information-on-a-vessel-s-flag-found-)
//d.NAME = Vessel Name
//d.SOG = Speed in Knots
//d.COG = Heading in Clockwise Degrees (0 = North; 90 = West...)
//d.DEST = Destination Port
//d.TYPE = Vessel Type (7=Vehicle Carrier, 8:Tanker...)
//d.LAT = Current Latitude
//d.LNG = Current Longitude
//d.ARV = Projected Arrival Time, 201704272230 is 10:30PM on April 27, 2017 GMT

//Draw real-time vessel
d3.json("http://www.myshiptracking.com/requests/vesselsonmap.php?type=json&minlat=" + minlat +
"&maxlat=" + maxlat + "&minlon=" + minlon + "&maxlon=" + maxlon + "&zoom=7", function(err, boats){
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
		if ((countrycode == 303) || (countrycode == 338) || (countrycode >= 366 && countrycode <= 369))
		   {return "USA" }
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

<br />

The orange(#e47a33) dots represent fishing vessel and green(#018771) dots represent other types of vessel.
![North America](http://i.imgur.com/zlOYGiz.png)

<br />

You can apply the region setting to different areas in the globe. I list some areas below:
<pre>
//East Coast of North America
var ECminlat = 20;
var ECmaxlat = 40;
var ECminlon = -75;
var ECmaxlon = -55;

//South America
var SAMminlat = -40;
var SAMmaxlat = -30;
var SAMminlon = -70;
var SAMmaxlon = -50;

//Brazil
var BRminlat = 10;
var BRmaxlat = -10;
var BRminlon = -60;
var BRmaxlon = -40;

//East Asia
var EAminlat = 20;
var EAmaxlat = 40;
var EAminlon = 110;
var EAmaxlon = 130;

//South East Asia
var SEAminlat = -10;
var SEAmaxlat = 10;
var SEAminlon = 130;
var SEAmaxlon = 150;


//South Asia
var SAminlat = 0;
var SAmaxlat = 20;
var SAminlon = 90;
var SAmaxlon = 110;


//Australia
var AUminlat = -30;
var AUmaxlat = -10;
var AUminlon = 135;
var AUmaxlon = 155;

//South Europe
var SEUminlat = 30;
var SEUmaxlat = 40;
var SEUminlon = 10;
var SEUmaxlon = 20;

//North Europe
var NEUminlat = 50;
var NEUmaxlat = 60;
var NEUminlon = 10;
var NEUmaxlon = 30;

//West Africa
var WFminlat = 20;
var WFmaxlat = 40;
var WFminlon = -30;
var WFmaxlon = -10;

//South Africa
var SFminlat = -30;
var SFmaxlat = -10;
var SFminlon = 20;
var SFmaxlon = 40;
</pre>

<br />

The result of vessel location visualization\
![Worldmap](http://i.imgur.com/hgLWzsy.png)
