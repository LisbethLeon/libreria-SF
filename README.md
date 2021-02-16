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

 Convertir csv a puntos - st_as_sf()
 
      terremtos <- read.csv("data.csv")
      head(terremtos)
      str(terremtos)
      plot(terremtos)
![Rplot 2](https://user-images.githubusercontent.com/77855207/108010363-aeb75d80-6fd2-11eb-8db7-62ce4a520e76.png)

 Convertimos a un objeto sf
 (Codigo 4326 de la coordenada geografica WGS 84)
 
      data_terr <- st_as_sf(terremtos, coords = c("Longitude", "Latitude"), crs = st_crs(4326))
      head(data_terr)
      str(data_terr)

      plot(st_geometry(data_terr))
![Rplot 3](https://user-images.githubusercontent.com/77855207/108010435-da3a4800-6fd2-11eb-93ed-2b3920b3d0b8.png)

      mapview(st_geometry(data_terr))
      
![Rplot 4](https://user-images.githubusercontent.com/77855207/108011641-82e9a700-6fd5-11eb-9042-e61b978b87bd.png)

 Crear buffer - st_buffer()
 
      mapview(st_buffer(data_terr, 1))

 Extraer centroides - st_centroid()
 
      plot(st_geometry(data_departamento))
      centros <- st_centroid(data_departamento)
      plot(st_geometry(centros), add=T)

Crear contorno - st_bbox(), st_make_grid()

      st_bbox(data_departamento)
      plot(st_geometry(st_make_grid(data_departamento, n=1)), add=T)

Seleccionamos la provincia de nuestra preferencia

      prov <- st_read("Provincias/PROV/Provincias.shp")
      head(prov)
      mapview(st_geometry(prov))

      data_prov <- prov %>%
        filter( NOMBDEP == "CUSCO")

      mapview(st_geometry(data_prov))
