# Final Exercise BWSI Remote Sensing 2022

Starter resources for students

# bwsi-rs-finalProject 

Google Doc with responsibilities : https://docs.google.com/document/d/15JU8v1LRuyBc-AGVk0grp5lKXXk-uK2KHfd3BwOfrf4/edit?usp=sharing
All data was retrived from : Index of /data/final_2024 (bwsi-remote-sensing.net)


# Planning Team(my team) 
Index of /data/final_2024 (bwsi-remote-sensing.net)
# Planning Team

The planning team is responsible for creating data products to visualize and prepare for the oncoming storm. This team will work with GIS and remote sensing. You will need to use the various tools we have learned to use this class in order to perform these tasks
 
 
Create visualizations of storm likely paths from forecasts for each day's projections
Calculate the central projected storm path by finding the centroid of each forecast time's projections
Create cone of uncertainty which encompasses all of the projected paths - like this:
https://www.nhc.noaa.gov/images/cone_5day_with_wind.png 

Create map for probability of tropical storm winds
Assess wind probabilities for hurricane-force winds, strong tropical storm winds, and tropical storm winds in a graphic like this: https://www.nhc.noaa.gov/images/wind_probs_34.png 
Create three graphics: probability of hurricane force, strong tropical storm, and tropical storm force winds
Hurricane-force winds can extend up to 80 km radius from the center of the hurricane when the hurricane is Cat 1 or greater
Strong tropical storm (STS) winds up to 160 km radius
Tropical storm (TS) winds up to 300 km radius
To do this, take each of the projected paths and buffer them by the respective radius for the winds
Then calculate in each area how many of the projected areas overlap, and convert this into a percentage of total projections to get a probability. You may find this function for counting overlapping =polygons useful: Count overlapping features using Geopandas - Geographic Information Systems Stack Exchange 

Create a flood depth map for various levels of storm surge for the central projection using a DEM
There will be different levels of storm surge depending on distance from hurricane center
Within 80 km of the center, storm surge may be up to 6m
within 80-160 km, storm surge may be up to 4m
within 160-300 km, storm surge may be up to 3m
Storm surge will only affect the areas near the coast - find coastline and buffer 5 km to apply "bathtub" flooding model
Bathtub flooding model selects all areas under storm surge height, and calculates the flooding depth as `storm surge height - elevation`
You may find the intersection operation helpful for this analysis. Take the intersection between the buffered storm surge area around the central projection and the buffered coastline. https://geopandas.org/en/stable/docs/user_guide/set_operations.html 
Select only the part of the DEM corresponding to the intersection areas.

Create a map of population density
Assess most affected regions and plan accordingly
Account for population vulnerability using SVI
this data may be useful: https://sedac.ciesin.columbia.edu/data/set/usgrid-summary-file1-2010
https://developers.google.com/earth-engine/datasets/catalog/CIESIN_GPWv411_GPW_Population_Count  
Designate evacuation zones based on projected damage areas
Each zone is limited to 1.5 million people
Evacuation of a zone takes 1 day. 
For each day of the exercise, you must designate one zone to evacuate.
Need to choose enough shelters for evacuees (~5% of total evacuated)
Shelters must not be in flooded areas
Assign evacuees to shelters based on distance and capacity
If there is not a listed capacity (EVACUATION_CAPACITY), assume it is 200
Mapped 
Using remote sensing (Landsat or Sentinel 2) and Digital Elevation Maps, identify regions at risk of inland flooding by computing a soil moisture index
Areas with higher soil moisture are at higher risk of flooding during heavy rains, since there is already a lot of water in the ground

# Logistics Team
The Logistics Team is responsible for moving resources to the locations that require them. This team will work with network optimization, routing, and GIS
You will receive a game grid with transportation scores for each cell
Convert Game Grid into routing network (provided)
Travel time in minutes between two cells x, y: T(x,y) = 20/(x.transport_score + y.transport_score)
Each grid cell can be connected only to immediate neighbors (up to 8: NW, N, NE, E, SE, S, SW, W)
The hurricane will affect the transport scores of various cells. You will not know the exact state of the network until after the hurricane hits (Friday)
Designate up to 5 distribution centers throughout the map and pre-allocate supplies there before the hurricane hits.
One of those distribution centers must be Westover Air Reserve Base, at coordinates 42.1991° N, 72.5436° W
Use OSMnx to find other available public airfields
Gauge flooding distribution with the Planning Team and determine resource pre-allocation accordingly
You have 150,000 units of resources to stage at your chosen distribution centers (see below about resource needs). 
You will be provided a list of hospitals and shelters that require assistance on day 3 of the exercise (Friday). Create an algorithm that generates truck shipping routes which provide as many resources necessary within the given time frame. Hospitals require 500 resource units to be supplied, and shelters require 200.
You have 40 trucks. You must pre-allocate the trucks at your distribution centers prior to the storm onset
Each truck can carry up to 1200 units of resources per trip
It takes 20 minutes to unload up to 200 resources. Any amount less than 200 still takes the full 20 minutes. For example, unloading 500 resources will take an hour: 20 minutes each for the first and second 200, and 20 minutes for the last 100.
Truck routes can not take longer than 12 hours (shift length constraint)
Trucks must start and end their journey at one of your distribution centers
Resources must arrive within 72 hours after the storm's arrival in order to be useful
Visualize the routes that your trucks are taking
This is an example of the vehicle routing problem, which is a generalization of the TSP
Notably, this is an example of a capacitated vehicle routing problem, since the vehicles can only carry a finite amount of resources

# Operations Team
The Operations Team is responsible for providing situational awareness. This team will complete computer vision tasks using SfM and deep learning.
Build and train classifiers to identify damage types, some type of infrastructure (buildings, roads)
Use your classifier to identify images of damage, infrastructure, and others that were not in your training dataset 
Use these images to tell some stories about the response. For example, you can make up a search and rescue operation based on what you learned from MA-TF1, or report on the state of infrastructure. Get creative with it.
Report the classification performance of your classifiers
Using the xview exercise, create segmentation masks and classification of buildings affected by hurricanes
Create a geodataframe with the building footprints and the classifications
Tell a story about the images you have analyzed - get creative with it
Create a small-scale representation of hurricane damage using craft materials, toys, minecraft, or whatever materials you have
Use structure from motion to create a 3D representation of the scene
You may use OpenSfM or any other tool to generate the data/visualize

# Public Information Team
The public information team is responsible for interacting with the press. They will periodically update the press via press conferences with the teams’ progress in dealing with the hurricane— especially as the hurricane progresses. 
Inform the press of most affected regions (with planning team)
What regions did planning think to be most affected (at greatest risk), what action was taken
Most affected includes population density, flooding, location in regard to hurricane path, access to medical supplies/nearby hospitals, power outages/access to electricity, potential for power outages, persons with disabilities & senior citizens, etc… 
Inform press of evacuation plans/efforts
What regions will be evacuated based off flooding predictions & hurricane path predictions
How are teams aiding in evacuation efforts, plans in allocating persons to shelters 
Frequent updates regarding the weather (maybe designate a weatherperson!) 
Inform press as to periodic progress of each team
Interview each team 
What is the focus of each team as the hurricane progresses
Be ready to answer audience questions
Be in charge of creating videos with the other subteams 
Explain what the public can do to stay safe
share items to buy, precautionary measures, and plans of action
Inform as to where supplies are sent (With Logistics Teams)
Both medical supplies and gas— where are supplies being sent and why
How are the teams allocating/transporting supplies


