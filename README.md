# Precipitation-data
from netCDF4 import Dataset
import numpy as np
import rasterio
import matplotlib.pyplot as plt
from mpl_toolkits.basemap import Basemap

data = Dataset(r'E:\dailyprecipitation\full_data_daily_v2020_10_2019.nc')
lats = data.variables['lat'][:]
lons = data.variables['lon'][:]
time = data.variables['time'][:]
#precipitation = data.variables['precip'][:]
precip = data.variables['precip'][:]
 
for i in range(0,1,1):
    c = precip[i,:,:] 
    driver = "GTiff"
    dim = c.shape 
    height = dim[0] 
    width = dim[1] 
    count = 1 
    dtype = c.dtype 
    from rasterio.crs import CRS 
    crs = CRS.from_epsg(2356)   
    from rasterio.transform import from_origin 
    transform = from_origin(180,90,1,1 ) 
    #sform = from_origin(180,90,1,1 ) 
    with rasterio.open("./separate/" +"G-day-"+str(i)+".tif", "w",
                  driver = driver,
                  height = height,
                  width = width,
                  count = count,
                  dtype = dtype,
                  crs = crs,
                  transform = transform) as dst: 
                dst.write(c, 1)
            
