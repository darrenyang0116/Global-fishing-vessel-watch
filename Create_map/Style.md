## Style your map

Now we want to add color to countries, oceans and graticules. Let's set up the style in html head section as below.


## Option 1
<pre>
<head>
<style>
.country{fill:#3a80b6; opacity:0.4; stroke:#fff; stroke-width:.3px;}
#sphere{fill:#051944; stoke:#fff; stroke-width:.2px;}	
.grat{fill:none; stroke:#fff; stroke-width:.1px;}
</style>
<head>
</pre>

![worldmap with style](http://i.imgur.com/mW0OMrK.png)


## Option 2
<pre>
<head>
<style>
.country{fill:#0B121F; opacity:0.45; stroke:#203a53; stroke-width:1.5px;}
#sphere{fill:#354f69;} 
.grat{fill:none; stroke:#0B121F; stroke-width:.3px; opacity:.75;}  
</style>
<head>
</pre>

![worldmap with style](http://i.imgur.com/w2Y1L9d.png)


## Option 3
<pre>
<head>
<style>
.country{fill:#0B121F; opacity:0.45; stroke:#203a53; stroke-width:1.5px;}
#sphere{fill:#354f69;} 
.grat{fill:none; stroke:#0B121F; stroke-width:.3px; opacity:.75;}  
</style>
<head>
</pre>

![worldmap with style](http://i.imgur.com/IKJQg1d.png)


I decided to go with Option 2. Next step is to add No-take Zone in our map.
