---
title: "Indonesia Tourism (Week 2 Assignment)"
author: "Stephanie_Lee_S"
date: "4/14/2021"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
The map shows ten tourism objects in Indonesia. All of them are natural wonders you can go to when you come to Indonesia (certainly after the pandemic is over :D). Indonesia has many beautiful places, so I had a hard time narrowing it down to only ten. I selected these places because some of these are very famous among foreigners, and some of them are unique. One of the places, Mount Tangkuban Perahu, is famous in Indonesia because that mountain has its own legend/folk story. I hope this tiny map could give you an idea of what kind of trip you could have here.

```{r}
library(dplyr); library(leaflet)
```

```{r data}
latitude <- c(-7.9425, -6.7596, -7.5407, 2.7861, 
              -1.0915, 1.6235, -2.8709, -8.6012, 
              -8.5277, -8.5920)
longitude <- c(112.9530, 107.6098, 110.4457, 98.6161, 
               130.8779, 124.7603, 107.9532, 119.5198,
               119.4833, 115.2666)
places <- c('Mt.Bromo', 'Mt.Tangkuban Perahu', 'Mt.Merapi', 'Lake Toba', 
            'Raja Ampat', 'Bunaken', 'Belitung Island', 'Pink Beach', 
            'Komodo National Park', 'Bali Zoo')
imgfiles <- c('https://upload.wikimedia.org/wikipedia/commons/8/8e/Bromo-Semeru-Batok-Widodaren.jpg',
              'https://cdn.shopify.com/s/files/1/1531/9251/products/the-top-of-tangkuban-perahu-volcano_grande.jpg?v=1571439386',
              'https://upload.wikimedia.org/wikipedia/commons/thumb/9/9d/Mount_Merapi_in_2014.jpg/320px-Mount_Merapi_in_2014.jpg',
              'https://www.indoindians.com/wp-content/uploads/2018/07/24035963054_47a60a71b7_b.jpg',
              'https://blue.kumparan.com/image/upload/fl_progressive,fl_lossy,c_fill,q_auto:best,w_640/v1532665836/photo1_lldamc.jpg',
              'https://indonesiadestinations.com/wp-content/uploads/2017/11/underwater-beauty-of-bunaken.jpg',
              'https://javaindoecotourism.com/wp-content/uploads/image_batu.jpg',
              'https://asset.kompas.com/crops/O1-Fz_6DqwjFwgak8_CWWiebFeQ=/0x83:1000x750/750x500/data/photo/2020/02/24/5e538e7bda8fd.jpg',
              'https://upload.wikimedia.org/wikipedia/commons/thumb/3/3a/Komodo_dragon_at_Komodo_National_Park.jpg/284px-Komodo_dragon_at_Komodo_National_Park.jpg',
              'https://bb.trvcdn.net/uploads/galleries/ef43c4ee94ee38bb93cb4668b8d5591c.jpg')
```

```{r}
#create links for inserting images
links <- sapply(imgfiles, function(x) paste0('<img src = ', x, ' width = 600>'))

#create icon
mount <- makeIcon(iconUrl = 'https://cdn.iconscout.com/icon/free/png-256/mountains-1436867-1212936.png', 
                  iconWidth = 40, iconHeight = 40, iconAnchorX = 20, iconAnchorY = 20)
water <- makeIcon(iconUrl = 'https://i.pinimg.com/originals/26/e6/74/26e674c35cb7c8e0a679fe071b5507cf.png', 
                  iconWidth = 40, iconHeight = 40, iconAnchorX = 20, iconAnchorY = 20)
animal <- makeIcon(iconUrl = 'https://image.flaticon.com/icons/png/128/2093/2093843.png', 
                   iconWidth = 40, iconHeight = 40, iconAnchorX = 20, iconAnchorY = 20)
```

```{r map}
dest <- leaflet() %>% 
        addTiles() %>% 
        addMarkers(lat = latitude[1:3], lng = longitude[1:3], 
                   popup = paste(links[1:3], places[1:3]), icon = mount,
                   popupOptions = popupOptions(minWidth = 200)) %>%
        addMarkers(lat = latitude[4:8], lng = longitude[4:8],
                   popup = paste(links[4:8], places[4:8]), icon = water,
                   popupOptions = popupOptions(minWidth = 200)) %>%
        addMarkers(lat = latitude[9:10], lng = longitude[9:10],
                   popup = paste(links[9:10], places[9:10]), icon = animal,
                   popupOptions = popupOptions(minWidth = 200))

dest
```

