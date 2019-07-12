# General Overview:

## Responsibilities of overall managing the chargers  
**TASK 1**- Evaluating the april tag’s position in order to understand in which direction the duckiebot went  
**TASK 2**- Gathering information on charger sizes and finding the next charger a duckiebot newly arriving the maintenance area should go  
**TASK 3**- Selecting the frequency with which the LED should blink 

In Modul 1, all the responsibilities are done by the charging manager. 
The output of tasks above feeds information to other tasks, for example, in task 1, it will be found out, which duckiebot entered or left the charger and this will be saved in a data structure that can be accessed by the charging manager. 
In task 2, charging manager will iterate over the data structure in order to discover how many duckiebots occupy the chargers. Through linear search, the most unoccupied charger will be determined and the frequency of LEDs corresponding charger id will be changed accordingly. In task 3 LEDs will blink with the mentioned frequency. 

In Modul 2, the tasks are completed in separate devices. Task 1 is accomplished by doorkeepers and the rest will be done by the charging manager. The output of task 1 will be shared with the charging manager through a communication server. For this objective, charging manager serves a python-dictionary of duckiebot Apriltags as keys and charger indices as values (initially all charger indices are set to zero to indicate that the duckiebot does not occupy any charger.). The clients, in this case the doorkeepers, will update this dictionary according to their evaluation of april tag positions, for example, if duckiebot with april tag 400 enters charger 3 then the doorkeeper will change the value of 400 from 0 to 3. 

_To give you a better understanding of the code, you are welcome to use the schema below. It uses the exact same variable names in the code._

[SCHEMA OF FUNCTIONS AND THEIR USAGE AND SHARED MEMORIES FOR MODUL 1 AND 2]



## Workflow in detail

### Preliminary information:
Every frequency with which the LED blinks, implies to which charger the duckiebot should go.
CSLAM Acquisiton node provides many information. Only the data about the position of the center on the image will be used by charging manager. 

### Modul 1:
#### Charging Manager

0. Charging Manager’s LED blinks with the initial frequency
1. (TASK 1) CSLAM Acquisition node provides information on the Apriltags in the scope of camera  
	In the scope of the camera, lies the reference tags and duckiebots’ Apriltags ,if there are any arrived to the intersection. 
	The positions of duckiebots’ Apriltags and reference tags will be saved and updated, as the node publishes the topic. 
	Upon receiving these, the closest neighbour reference tag and the timestamp will be computed and saved (Here, minimal distance is defined by the minimal euclidean distance of two points on the image.)
	(The first computed closest neighbour reference tag will be saved under the variable “first_neighbour” and the other results will be saved as “last_neighbour”.)
	
2. (TASK 1) Apriltag Evalutaion:  
	After not seeing an Apriltag of a duckiebot for more than threshold time, the “first_neighbor” and “last_neighbor” will be evaluated. 
	TAGS = {enter_tag,exit_tag,direction1_tag,direction2_tag}
	outcome element of  {(first_neighbor,last_neighbor) for first_neighbor, last_neighbor element of TAGS}
	Meaning of any possible outcome can be interpreted with the help of the following schema:
	[SCHEMA TAGS EVALUATION]
	According to this outcome the chargers dictionary will be updated and the tag of duckiebot which has entered/exited the charger i and the timestamp of entrance will be saved/deleted under/from charger i’s list. 
3. (TASK 2) Charger sizes will be updated according to step 2  
	If the most unoccupied charger is changed, it will be noticed and new frequency corresponding the new charger with the most free spaces will be determined

4. (TASK 3) LED blinks with the determined frequency in step 3

These steps will be repeated upon receiving the messages from acquisition node’s topic
	
	

### Modul 2:

#### Preliminary information:
In this module a dictionary where keys are the duckiebots Apriltags and values are the charger indices or zero(indicating that the duckiebot is currently not occupying any charger) is served by the charging manager. The clients, doorkeepers, will update this dictionary. 






#### Doorkeeper


1. **(TASK 1)** CSLAM Acquisition node provides information on the Apriltags in the scope of camera
	In the scope of the camera, lies the reference tags and duckiebots’ Apriltags ,if there are any arrived to the intersection.   
	The positions of duckiebots’ Apriltags and reference tags will be saved and updated, as the node publishes the topic.   
	Upon receiving these, the closest neighbour reference tag and the timestamp will be computed and saved _(Here, minimal distance is defined by the minimal euclidean distance of two points on the image.)_
	_(The first computed closest neighbour reference tag will be saved under the variable “first_neighbour” and the other results will be saved as “last_neighbour”.)_
2. **(TASK 1)** Apriltag Evalutaion:
	After not seeing an Apriltag of a duckiebot for more than threshold time, the “first_neighbor” and “last_neighbor” will be evaluated. 
	TAGS = {enter_tag,exit_tag,direction1_tag,direction2_tag}
	outcome element of  {(first_neighbor,last_neighbor) for first_neighbor, last_neighbor element of TAGS}
	Meaning of any possible outcome can be interpreted with the help of the following schema:
	[SCHEMA TAGS EVALUATION]

3. **(Communication Server)** Sharing the information where duckiebot went
	After finding out where a duckiebot went, its value in the served dictionary will be either set to the charger index if it entered a charger or to zero, if it left a charger. 


#### Charging Manager 


0. Charging Manager’s LED blinks with the initial frequency
1. **(Communication Server)** Charging Manager checks the dictionary updated by the doorkeepers periodically
	If the charger index of an Apriltag in the dictionary is changed, then the tag of duckiebot which has entered/exited the charger i and the timestamp of entrance will be saved/deleted under/from charger i’s list. 
	
3. **(TASK 2)** Charger sizes will be updated according to step 2
	If the most unoccupied charger is changed, it will be noticed and new frequency corresponding the new charger with the most free spaces will be determined

4. **(TASK 3)** LED blinks with the determined frequency in step 3


These steps will be repeated upon receiving the messages from acquisition node’s topic within doorkeepers



 
	

