# libreria-SF

Seleccionamos nuestro directorio de trabajo

setwd("C:/Users/LEO/Desktop/PROGRAMACION/sf")

Se cargan las librerías

      install.packages("sf")
      library(sf)

      install.packages("mapview")
      library(mapview)

      install.packages("dplyr")
      library(dplyr)

Se leen los datos shapefile

      data_departamento <- st_read("Departamentos/Departamentos.shp")
      class(data_departamento)
      head(data_departamento)

  Comienza el ploteo
  
      plot(st_geometry(data_departamento))

![Rplot 1](https://user-images.githubusercontent.com/77855207/108009675-30a68700-6fd1-11eb-8f94-b08a0013d613.png)

