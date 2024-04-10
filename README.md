# How-to-make-STATA-graphs-look-nice-or-a-little-bit-like-R-s-ggplot2-graphs-
Stata’s default graphs are not the best, but before you jump ahead and switch to R’s ggplot2 just to produce an eye-popping graph, consider the Stata package grstyle. The package offers a consistent and relatively easy way to adjust graph settings globally, meaning you don’t have to adjust the code of each graph separately, something that comes in handy if you are preparing multiple graphs e.g. for a publication.

1. 1)	A default Stata graphics scatter graph might look like Figure 1. 

sysuse auto

scatter mpg headroom turn weight
![graphs1](https://github.com/csae-coders-corner/How-to-make-STATA-graphs-look-nice-or-a-little-bit-like-R-s-ggplot2-graphs-/assets/148211163/21684b47-3689-4da5-a723-4c73f4723a28)

2. 2)	A defaut Stata graphics coefplot might look like Figure 2.

ssc install coefplot, replace				// install coefplot

sysuse auto, clear

regress price mpg trunk length turn if foreign==0

estimates store D

regress price mpg trunk length turn if foreign==1

estimates store F

coefplot D F, drop(_cons) xline(0)

![graphs2](https://github.com/csae-coders-corner/How-to-make-STATA-graphs-look-nice-or-a-little-bit-like-R-s-ggplot2-graphs-/assets/148211163/12bbec1d-b71d-448c-b354-fb56a9c1719a)

## Step-by-step guide to nice grstyle graphs:

3. Install grstyle and colorpalettes packages.
4. 	
ssc install grstyle, replace

ssc install palettes, replace	

4. Follow the documentation or use the example code to begin with.

5. First, initiate grstyle and run the code. I would recommend a separate “graph_settings.do” file. 

set scheme s2color		// sets Stata design scheme to default s2color
grstyle init			// initiates grstyle


The following lines are design suggestions:
		
grstyle set horizontal 				// set tick labels horizontal 
grstyle set compact					// overall design compact
grstyle set size small: subheading axis_title // subtitle and axis title set to small
grstyle set size vsmall: small_body 		// margin around notes
grstyle set legend 6, nobox			//legend position on 6 o'clock, removes box

grstyle set linewidth thin: major_grid 		// set grid line thickness to thin
grstyle set linewidth thin: tick 	      		// set tick thickness to thin
grstyle set linewidth thin: axisline 	       // set axislines thickness to thin
grstyle set linewidth vthin: xyline 			// reference line at 0


To adjust the appearance of the plotting area, outer lines and boxes, change the colour and opacity.

grstyle color background white 			// set overall background to white

grstyle set color black*.7: tick tick_label 		// set tick and tick label color
grstyle set color black*.08: plotregion plotregion_line	//set plot area background color
grstyle set color White: axisline  major_grid 	// set axis and grid line color

grstyle set color black*.7: small_body 			// set note color 
grstyle set color white*.08, opacity(0): pbarline 	// graph bar outline transparent



To get an overview of available colour designs type “help colorpalette”. Choose a colour scheme for your data plots.


For example, the “economist” scheme mimics the colour palette used by The Economist. I would recommend changing the order in which colours will appear though.

grstyle set color economist, order(10 1 8 2 3 4 5 6 7 9 11 12 13 14 15)

Adjust the size of the individual plots drawn (e.g. bars, scatter points, lines) by identifying their respective plot number by opening the graph in Statas graph editor.

![graphs3](https://github.com/csae-coders-corner/How-to-make-STATA-graphs-look-nice-or-a-little-bit-like-R-s-ggplot2-graphs-/assets/148211163/dc3453a8-e29e-4947-a857-b5087ead70d0)


Then specify the size for the individual plot element e.g.

grstyle linewidth p1 vthin 
grstyle textsize p1 vsmall 

grstyle linewidth p2 vthin 
grstyle textsize p2 vsmall    

and so on…

![graphs4](https://github.com/csae-coders-corner/How-to-make-STATA-graphs-look-nice-or-a-little-bit-like-R-s-ggplot2-graphs-/assets/148211163/3ab486f5-9cc5-4dc4-a141-87181363b5bd)

6. Let’s run the same graphs again:
![graphs5](https://github.com/csae-coders-corner/How-to-make-STATA-graphs-look-nice-or-a-little-bit-like-R-s-ggplot2-graphs-/assets/148211163/72ae4d0f-bd66-4e80-9bac-560cee9af9fb)

7. Finally, to reset your global graphic settings to Stata default settings run :
grstyle clear		 // sets off grstyle

![graphs6](https://github.com/csae-coders-corner/How-to-make-STATA-graphs-look-nice-or-a-little-bit-like-R-s-ggplot2-graphs-/assets/148211163/6d6f4738-52ba-4b22-9a73-2718f6c7ee1c)


For further help and syntax overview, see: http://repec.sowi.unibe.ch/stata/grstyle/help-grstyle-set.html

