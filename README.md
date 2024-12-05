# Aquifer properties function
## Objetive
Develop a code that shows some of the relevant characteistics of an aquifer (water table altitude and vadose zone tickness) and create a geodata base that contains the layers with this information. As inputs for this code, the user needs to supply well points with the depth to water and a Digital Elevation Model (DEM). The output layers are intended to generate a quick visualization of the aquifer conditions, but the results should be verified because the code uses a generic interpolation model thac couldn't adjust in a valid way to the input data. For this reason, the results for this script also include a Standard Error Map that shows to the user the accuracy of the interpolation model.
## Relevance
Generally, the analysis of the conditions of an aquifer starts with the collection of data such as the depth to the water level. However, this information is difficult to interpret quickly because the topographic altitude is generally not linked to the altitude of the water level and it is necessary to perform spatial interpolation analysis to have an approximation of the conditions of the aquifer, which is usually time-consuming and requires resources. Therefore, a model that helps to visualize and generate data on the conditions of the aquifer quickly is very useful to generate deeper analysis or to know the areas in which a greater amount of data is required to be analyzed.
## Flow process
### Analyze the spatial reference for the input layer
  -Review if the cordinate system for both layers is the same
    -If the coordinate system is diferent ask to the user a EPSG code for reproject the layers and save this layers in the output geodatabase.
{
 "cell_type": "code",
 "execution_count": 4,
 "id": "50c6f2dd-cd6f-481e-9a1c-cf864daf4607",
 "metadata": {},
 "outputs": [
  {
   "name": "stdout",
   "output_type": "stream",
   "text": [
    "The coordinate system for the Well data points is: Albers_NHG (0) and the coordinate system for the DEM is: GCS_North_American_1983 (4269)\n",
    "A reprojection is needed for develop this analysis\n"
   ]
  },
  {
   "name": "stdin",
   "output_type": "stream",
   "text": [
    "Enter the EPSG code to project both layers:  102003\n"
   ]
  }
 ],
 "source": [
  "desc_fc = arcpy.Describe(wellData)\n",
  "desc_raster = arcpy.Raster(DEM)\n",
  "if desc_fc.spatialReference.factoryCode != desc_raster.spatialReference.factoryCode:\n",
  "    print(f\"The coordinate system for the Well data points is: {desc_fc.spatialReference.name} ({desc_fc.spatialReference.factoryCode}) and the coordinate system for the DEM is: {desc_raster.spatialReference.name} ({desc_raster.spatialReference.factoryCode})\")\n",
  "    print(\"A reprojection is needed for develop this analysis\")\n",
  "    CS = int(input(\"Enter the EPSG code to project both layers: \"))\n",
  "    arcpy.management.Project(wellData,\"AquiferProperties.gdb\\\\welldData_RP\",arcpy.SpatialReference(CS))\n",
  "    arcpy.management.ProjectRaster(DEM, \"AquiferProperties.gdb\\\\DEM_RP\", arcpy.SpatialReference(CS))\n",
  "    wellData = \"AquiferProperties.gdb\\\\welldData_RP\"\n",
  "    DEM = \"AquiferProperties.gdb\\\\DEM_RP\""
 ]
},

###Calculate the water table altitude
  -List the fields in the well data points layer for select the field that contains the water depht
  

