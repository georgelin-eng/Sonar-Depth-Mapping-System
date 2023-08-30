# Sonar Depth Mapping System
 
___


## Project Overview

This is a system that would run off an Arduino collecting GPS and depth data from an waterproof ultrasonic distance sensor. Using the sensor data from a GPS module along with lake depth sensing, a bathymetric map could be plotted and visualized in python using libraries such as Matplotlib, Plotly, or using various GIS (Geospatial Information Systems) Libraries. 

GPS data can either be stored raw in longitude and latitude, or transformed into x and y displacements with one coordinate being considered the origin. 

Distance can be calculated as:
$$d=2r \arcsin \sqrt{(\sin^2(\frac{\Phi_{2}- \Phi_1}{2}​​)+\cos(\Phi_{1​)}\cos(\Phi_2​)\sin^2(\frac{\lambda_{2}- \lambda_1}{2} ​​)​)}$$

Where $\Phi$ is latitude and $\lambda$ is longitude.

Bearing can be calculated as:

$$θ = atan2( \sin (Δλ) \cos (\Phi_{2}) ,   \cos (\Phi_1) \sin (\Phi_2) − \sin (\Phi_1) \cos (\Phi_2) \cos (Δλ) )$$

with this bearing angle used to calculated x and y of each point with respect to the reference which is at (0, 0). This bearing angle is for an initial bearing angle and technically changes as you move from one point on a sphere to another, but but for small distances this effect is inconsequential. Using this measurement in conjunction with the magnetometer sensor data using sensor fusion techniques would allow for more accurate positional estimates. 


## Components List

| Component              | Purpose                                                                                                                         | Notes                                                                                                                                                       |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| JSN-SR04T              | Providing depth measurements                                                                                                    | Cheaper than alternatives and provided can provide readings up to 6m underwater                                                                             |
| BN-880                 | GPS module with magnetometer                                                                                                    | More expensive than BN-220 module but gives faster connection times to GPS and increased positional accuracy                                                |
| PDB                    | Simplified power connections to components                                                                                      | Developed in KiCAD                                                                                                                                          |
| MPU 6050               | Can be used for short time position estimations through dead reckoning                                                          | Suffers due to sensor drift due to summing sensor bias terms. Can be mitigated using multiple IMU modules and Kalman filtering but this is still imperfect. |
| I2C multiplexer        | Since MPU 6050s have the same I2C address, there would be a communications conflict so a multiplexer is required to manage this |                                                                                                                                                             |
| SD card module         | Allows for data logging                                                                                                         |                                                                                                                                                             |
| Liquid crystal display | Allows for simple visualization of sensor data logging and the user can see that the system is working as intended                                                                                                                               |                                                                                                                                                             |



## Power Distribution Board (PDB) Design


![](https://github.com/georgelin-eng/Sonar-Depth-Mapping-System/blob/main/PCB%20Board%20Image.png)



## Enclosures CAD

![](https://github.com/georgelin-eng/Sonar-Depth-Mapping-System/blob/main/Enclosures%20CAD%201.png)
![](https://github.com/georgelin-eng/Sonar-Depth-Mapping-System/blob/main/Enclosures%20CAD%202.png)


## Topographic Visualizations

Due to a lack of equipment (no boat), testing on a lack was not feasible. Instead, data was extracted from a 2d topographic image and used to create a 3d terrain model instead. (Input on right, visualization on left). https://github.com/georgelin-eng/topographic-map-to-3D-terrain-model

![](https://github.com/georgelin-eng/Sonar-Depth-Mapping-System/blob/main/topographic-map-to-3D-terrain-model.png)



## Conclusions and Future Work



http://www.movable-type.co.uk/scripts/latlong.html?from=49.243824,-121.887340&to=49.227648,-121.89631
