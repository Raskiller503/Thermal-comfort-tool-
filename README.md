# Introduction
PMV calculation is very complex due to it itneary and time consuming. In this part, we proposed one method could calculate it in real-time.

## Calculation flow
Pysical quantities such as (indoor air temperature, black globe temperature, relative humidity, air velocity) are collected and pre-processed by the sensors and combined with the clothing insulation selected according to the seasons and the metabolic rate daily to form the dataset. The PMV data were finally obtained by calculating the higher order equations and general equations using Sympy and Math libraries, respectively, through the Python program.
![flow](Image/Flow.png)

