# Adv-GIS_presentation.io
# Aquifer properties
## Objetive
Develop a code that shows some of the relevant characteistics of an aquifer (water table altitude and vadose zone tickness) and create a geodata base that contains the layers with this information. As inputs for this code, the user needs to supply well points with the depth to water and a Digital Elevation Model (DEM). The output layers are intended to generate a quick visualization of the aquifer conditions, but the results should be verified because the code uses a generic interpolation model thac couldn't adjust in a valid way to the input data. For this reason, the results for this script also include a Standard Error Map that shows to the user the accuracy of the interpolation model.
## Relevance
Generally, the analysis of the conditions of an aquifer starts with the collection of data such as the depth to the water level. However, this information is difficult to interpret quickly because the topographic altitude is generally not linked to the altitude of the water level and it is necessary to perform spatial interpolation analysis to have an approximation of the conditions of the aquifer, which is usually time-consuming and requires resources. Therefore, a model that helps to visualize and generate data on the conditions of the aquifer quickly is very useful to generate deeper analysis or to know the areas in which a greater amount of data is required to be analyzed.
## Flow process
### Review the 
