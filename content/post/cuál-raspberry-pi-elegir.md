+++
authors = []
date = ""
draft = true
excerpt = ""
hero = ""
timeToRead = 10
title = "¿Cuál Raspberry Pi elegir?"

+++
Antes de empezar a automatizar nuestra casa necesitamos tomar una decisión que nos perseguirá en el futuro: **cuál Raspberry Pi queremos**. Por suerte no hay muchas... pero hay las suficientes como para que tengamos que tomar una decisión lo más acertada posible.

La decisión la debemos tomar teniendo en cuenta el uso que le queremos dar, nuestro nivel de conocimiento en el área y el uso que le queramos dar.

Tened en cuenta que a parte del precio de las placas, es necesario comprar el adaptador de corriente, carcasa, microSD... con lo que el precio suele subir bastante. 

Todas las placas pueden levantar Home Assistant, disponen de Wifi (2.4G/5G) y Bluetooth (¡ideal para domótica!).

## Raspberry Pi Zero W (11€)

Empezamos con la que es la más barata del mercado. ¡Yo empecé con esta! Va muy bien para configurar unas pocas integraciones con Home Assistant, aunque su procesador no es suficiente potente como para dar un buen rendimiento. Los reinicios del Home Assistant pueden demorar bastante y hay que intentar tener la configuración lo más óptima posible, lo que implica **no usar docker**, aplicar una retención en los eventos de Home Assistant de **1 dia** para no hacer la base de datos demasiada larga, y más optimizaciones de las que hablaremos más adelante. 

Esta Raspberry es ideal para complementar otra Raspberry Pi. Con esta podéis crear una cámara de seguridad o usarlo de homebridge para un Apple Homekit.

## Raspberry Pi 3A+ (27€)

Esta ha sido la segunda Raspberry que he comprado. Una vez comprada, migré mi configuración de la ZeroW a esta, con una notable mejora de rendimiento. Aún no tengo claro que haya llegado a exprimir esta placa al 100%. Uno de sus defectos sería la cantidad de memória con la que viene, 512MB, y es que con esta memoria es fácil que el sistema empiece a hacer swapping, o termine matando los procesos que consumen demasiada memoria...

## Raspberry Pi 4B 4GB (61€)

Aún la estoy configurando. Podemos considerar que esta es la Raspberry más potente (y cara) disponible actualmente. Por su elevado precio podéis imaginaros que con esta Raspberry no tendremos problemas de rendimiento, será capaz de servir Home Assistant, Plex, Deluge, Nextcloud y una base de datos **al mismo tiempo**. Eso sí, tendréis que comprar un ventilador y disipadores para que no se queme. 

Lo mejor de esta Raspberry es que con tanta memoria es difícil que el sistema empiece a hacer swapping. 

## Tabla comparativa