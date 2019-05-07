## Estimation of soil water content in the entire root-zone

**Name**: Pedro Rossini <br/>
**Project area**: Agronomy - soil water ralations


## Objective
Implement in python an exponential filter equation to estimate daily soil water content (SWC) of the entire root-zone from daily surface observations.

<a href="https://www.codecogs.com/eqnedit.php?latex=$$SWI_{2(t)}&space;=&space;SWI_{2(t-1)}&space;&plus;&space;K_t&space;[\text{vwc}_{(t)}&space;-&space;SWI_{2(t-1)}]$$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$$SWI_{2(t)}&space;=&space;SWI_{2(t-1)}&space;&plus;&space;K_t&space;[\text{vwc}_{(t)}&space;-&space;SWI_{2(t-1)}]$$" title="$$SWI_{2(t)} = SWI_{2(t-1)} + K_t [\text{vwc}_{(t)} - SWI_{2(t-1)}]$$" /></a>


## Motivation and Methodology

Water stress is considered one of the main limiting factors in summer crop yield. Monitoring SWC of the entire root- zone during the crop seasson is a key factor to improve management irrigation practices and reduce the yield gaps. Solutions like multy depth soil moisture sensors within a field are laborious and expensive for farmers to implemmet.

The exponential filter equation is a known analytical method, that is widely used to predict a SWC of the root-zone from time series surface soil moisture observations. Briefly, the soil profile is divided in two layers: surface (first) and sub-surface (second), and the equation is used to predict the sub-surface soil moisture from observed measurements at the surface layer (Wagner et al., 1999).  

Albergel et. al., (2008) presented a recursive equation to simplify the calculations:

$$SWI_{2(t)} = SWI_{2(t-1)} + K_t [\text{vwc}_{(t)} - SWI_{2(t-1)}]$$
  
Where $SWI_2$ represents the soil water index of the second layer, $\text vwc$ represents the measured soil moisture at the surface layer, $K$ is the gain of the exponential filter that gets values between 0 and 1, and $t$ is the day of measurement. $SWI_2$ is a scaled soil moisture content and ranges between 0 to 1 based on the minimum and maximum values of each time series.  

In order to get the estimated soil water content at the second layer $SWC_{2(t)}$ is necessary to re-scale the $SWI_2$ by using the maximum $W_{2 max}$ and minimum $W_{2 min}$ soil moisture from the second layer as follows:


\(SWC_{2(t)} = SWI_{2(t)}(W_{2 max} - W_{2 min}) + W_{2 min}\)

Finaly, to predict the entire root-zone SWC ($profileSWC_{(t)}$) will be obteined by coupling the observed soil moisture at surface $\text vwc_{(t)}$ and the re-scaled $SWC_{2(t)}$ as:


\begin{equation}
profileSWC_{(t)} = SWC_{2(t)} * L2 + \text vwc_{(t)} * L1 
\end{equation}

where L1 and L2 are the thick of first and second soil layer in milimeters.

#### Sketch
 
<img src="sketch.JPG" alt="sketch_image" width="500"/>

Figure 1. Sketch summarizing the workflow proposed for this project.


#### Initial parameters

The initial $SWI_2$ ($t=1$) is obtained from a soil moisture observation at 0-5 cm depth at initial time divided by the maximum amount of water that the layer can hold. 

The initial value for $profileSWC$ ($t=1$) is obtained from a soil moisture observation at 0-5 cm depth at initial time multiplied by the length of the first layer (mm) plus the diference between maximum and minimum water holding capacity of the sub-surface layer multiply by the length of the second layer (mm).


#### Data used to test the model

In this work, daily soil moisture observations at 5 cm depth ($\text vwc_{(t)}$) from Kansas mesonet stations were used as model input to predict profile soil moisture from 0 to 50 cm depth (also know as root-zone). In addition, soil moisture observations at 10, 20, and 50 cm depth from Kansas mesonet stations were used to test the model output.

The model was tested in eight stations during 2018 between April to November because we are focused on testing the model during summer crop season, and to avoid interference of freezing temperatures during the winter in soil moisture readings.


#### Kansas mesonet stations and geographic distribution

Eight Mesonet stations across the state were selected taking into consideracion variability of soils types, soil texture, average anual precipitation and land use (rainfed crops, irrigated crops, natural granssland)  

- Cherokee_2018_to_2019 
<img src="ksmap.jpg" alt="sketch_image" width="500" align="right"/>
- Colby_2018_to_2019
- GardenCity_2018_to_2019       
- Gypsum_2018_to_2019  
- Hays_2018_to_2019
- Hodgeman_2018_to_2019
- LakeCity_2018_to_2019
- Lane_2018_to_2019

Figure 2. Map of the state of Kansas showing the location and distribution of the Mesonet stations (orange dots) selected for this study. 


## Results and Discussion

Soil water content for the entire root-zone (0 to 50 cm) was predicted successfully for all the selected Mesonet stations, showing consistent results and reasonable accuracy. Figure 3 shows the result of the model predictions against the observed data for two of the selected stations during the study period.  

<br/>

<img src="results3.JPG" alt="sketch_image" width="600" aling="middle"/> 
<img src="results1.JPG" alt="sketch_image" width="615" aling="middle"/> 

Figure 3: Observed and predicted $SWC$ in milimeters across time at Hays Mesonet station. 



comentarios varios......



Table 1:

|Station  |RMSE|MSE  |SWC_ave|SWC_min|SWC_max|
|:------- |:--:|:---:|:-----:|:-----:|:-----:|
|Hodgeman|16.64|12.59|164|118|219|    
|Lake City|8.97|6.61|54|26|119|
|Lane    |16.32|13.84|179|107|244|
|Hays    |14.49|12.45|184|119|252|
|Cherokee|18.44|14.66|170|89|226|
|Colby   |20.6|18|210|92|239|
|Garden City|15.99|13.25|100|71|157|
|Gypsum  |23.98|20.6|142|104|194|
















## References
Albergel, C., Rudiger, C., Pellarin, T., Calvet, J.-C., Fritz, N., Frois-sard, F., Suquia, D., Petitpa, A., Piguet, B., and Martin, E.(2008) From near-surface to root-zone soil moisture using an exponential filter: an assessment of the method based on in-situ observations and model simulations, Hydrol. Earth Syst. Sci., 12, 1323–1337,
doi:10.5194/hess-12-1323-2008

Wagner, W., Lemoine, G., & Rott, H. (1999). A method for estimating soil moisture from ERS scatterometer and soil data. Remote sensing of environment, 70(2), 191-207.

