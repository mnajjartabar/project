# Implementing an exponential filter model to estimate soil water content in the entire root-zone

**Name**: Pedro Rossini <br/>
**Semester**: Spring 2019 <br/>
**Project area**: Agronomy


## Objective

Implement a python code to estimate daily soil water content of the entire root-zone from surface observations using an exponential filter model.

## Outcomes

The model would likely predict daily soil moisture for the entire profile (0 to 80 cm) from daily soil moisture measurements at the surface (0 to 5 cm) depth. 
The final pipeline will generate an output file .csv with daily API index, daily root-zone moisture predictions and the prediction accuracy of the model. Moreover, it will create a figure showing the root-zone water content predicted by the model vs. the observed root-zone water content from Mesonet station.

## Rationale and methodology

Accurate measurements of soil water content at root-zone remains decisive in agriculture, hydrology, ecology, and climatology. An innovative approach to tackle this is using an exponential filter model to predict the entire root-zone moisture from soil moisture observations at the surface (0-5 cm) (Albergel et al, 2008).  

An exponential filter model is a semi-mechanistic model that is useful to estimate soil water index (SWI) of the root-zone from the soil observations at the surface. The model has only 3 parameters, SWCSURF that represents the soil moisture observed at the surface, SURFMAX that represents the maximum amount of water that the surface can hold and K that is related to the gaps between observations and it can take values between 0 and 1.

The exponential filter model equation:

<br/>
<img src="SWI_eq.JPG" alt="sketch_image" width="500"/>
<br/>
 

The initial SWI (t=1) will be estimated using soil moisture observations from a Mesonet station (0-5 cm depth) divided by the maximum amount of water that the layer can hold.
Daily soil moisture observations at 5 cm depth from Kansas Mesonet will be use as a main input of the model (SWCSURF(t)). On the other hand, daily soil moisture observations at 10, 20, and 50 cm depth will be used to calibrate and validate the model predictions.


## Sketch
 
<img src="Soil_2.JPG" alt="sketch_image" width="500"/>

Figure 1. Sketch summary the workflow proposed for this project.

## References
Albergel, C., Rudiger, C., Pellarin, T., Calvet, J.-C., Fritz, N., Frois-sard, F., Suquia, D., Petitpa, A., Piguet, B., and Martin, E.(2008) From near-surface to root-zone soil moisture using an exponential filter: an assessment of the method based on in-situ observations and model simulations, Hydrol. Earth Syst. Sci., 12, 1323–1337,
doi:10.5194/hess-12-1323-2008



