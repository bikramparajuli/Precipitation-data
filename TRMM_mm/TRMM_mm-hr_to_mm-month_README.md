# Precipitation-data 
# converting unit of TRMM precipitation from mm/hour to mm/month
import os
from netCDF4 import Dataset,num2date
import netCDF4
import numpy as np
import matplotlib.pyplot as plt
import rasterio
from rasterio.plot import show
from rasterio.plot import show_hist
from matplotlib.colors import ListedColormap
import matplotlib.colors as colors


for files in os.listdir(r'C:\Users\bikra\Desktop\Thesis_Final\Precipitation Data\TRMM\TRMMtc'):
    if files[9:11] == '01' or files[9:11] == '03' or files[9:11] == '05'or files[9:11] == '07'or files[9:11] == '08'or files[9:11] == '10'or files[9:11] == '12':
        print(files)
        data = Dataset(files)
        lats = data.variables['nlat'][:]
        lons = data.variables['nlon'][:]
        precipitation = data.variables['precipitation'][:]
        d = precipitation[:,:]
        c = d*24*31 #to convert unit of precipitation from mm/hour to mm/month
        driver = "GTiff"
        dim = c.shape
        height = dim[1] 
        width = dim[0]
        count = 1 
        dtype = c.dtype 
        from rasterio.transform import from_origin 
        transform = from_origin(71,32,0.25,0.25 ) #origin, cell size
        #saving array as a tif
        with rasterio.open("./Op1/TRMM" + files[5:11] + ".tif", "w",
                   driver = driver, 
                   height = height, 
                   width = width, 
                   count = count, 
                   dtype = dtype,
                   transform = transform) as dst: 
            dst.write(c, 1)
    elif files[9:11] == '04' or files[9:11] == '06' or files[9:11] == '09' or files[9:11] == '11' :
        print(files)
        data = Dataset(files)
        lats = data.variables['nlat'][:]
        lons = data.variables['nlon'][:]
        precipitation = data.variables['precipitation'][:]
        d = precipitation[:,:]
        c = d*24*30
        driver = "GTiff"
        dim = c.shape
        height = dim[1] 
        width = dim[0]
        count = 1 
        dtype = c.dtype 
        from rasterio.transform import from_origin 
        transform = from_origin(71,32,0.25,0.25 )
        with rasterio.open("./Op1/TRMM" + files[5:11] + ".tif", "w",
                   driver = driver, 
                   height = height, 
                   width = width, 
                   count = count, 
                   dtype = dtype,
                   transform = transform) as dst: 
            dst.write(c, 1)
    elif files[9:11] == '02':
        print(files)
        data = Dataset(files)
        lats = data.variables['nlat'][:]
        lons = data.variables['nlon'][:]
        precipitation = data.variables['precipitation'][:]
        d = precipitation[:,:]
        c = d*24*28
        driver = "GTiff"
        dim = c.shape
        height = dim[1] 
        width = dim[0]
        count = 1 
        dtype = c.dtype 
        from rasterio.transform import from_origin 
        transform = from_origin(71,32,0.25,0.25 )
        with rasterio.open("./Op1/TRMM" + files[5:11] + ".tif", "w",
                   driver = driver, 
                   height = height, 
                   width = width, 
                   count = count, 
                   dtype = dtype,
                   transform = transform) as dst: 
            dst.write(c, 1)
