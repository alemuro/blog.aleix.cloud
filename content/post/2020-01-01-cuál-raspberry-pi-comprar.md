+++
authors = ["aleix-murtra"]
date = "2019-12-31"
draft = false
excerpt = "Antes de empezar a automatizar nuestra casa necesitamos tomar una decisión importante, y es que hay que elegir la placa que mejor nos conviene."
hero = "/images/usb-technology-green-microchip-57007.jpg"
timeToRead = 10
title = "¿Cuál Raspberry Pi comprar?"

+++
Antes de empezar a automatizar nuestra casa necesitamos tomar una decisión que nos perseguirá en el futuro: **cuál Raspberry Pi queremos**. Por suerte no hay muchas... pero hay las suficientes como para que tengamos que tomar una decisión lo más acertada posible. 

La decisión la debemos tomar teniendo en cuenta el uso que le queremos dar, nuestro nivel de conocimiento en el área y el uso que le queramos dar.

Tened en cuenta que a parte del precio de las placas, es necesario comprar el adaptador de corriente, carcasa, microSD... con lo que el precio suele subir bastante. 

Todas las placas pueden levantar Home Assistant, disponen de Wifi y Bluetooth, así que són ideales para domótica.

### Raspberry Pi Zero W (11€)

![Raspberry Pi Zero W photo](/images/raspberry-pi-zero-w.jpg)

Empezamos con la que es la más barata del mercado. ¡Yo empecé con esta! Tiene un único core y 512MB de RAM. Va muy bien para configurar unas pocas integraciones con Home Assistant, aunque su procesador no es suficiente potente como para dar un buen rendimiento. Los reinicios del Home Assistant pueden demorar bastante y hay que intentar tener la configuración lo más óptima posible, lo que implica **no usar docker**, aplicar una retención en los eventos de Home Assistant de **1 día** para no hacer la base de datos demasiada larga, y más optimizaciones de las que hablaremos más adelante. 

Esta Raspberry es ideal para complementar otra Raspberry Pi. Con esta podéis crear una cámara de seguridad o usarla de bridge para un Apple Homekit. Debería comprarla gente que no quiera gastarse mucho dinero porque no sabe si le va a rentar la inversión. 

### Raspberry Pi 3A+ (27€)

![Raspberry Pi 3A+ photo](/images/raspberry-pi-3-a-plus.jpg)

Esta ha sido la segunda Raspberry que he comprado (para domótica). Tiene 4 cores pero sigue teniendo la misma RAM que la Zero W. Una vez comprada, migré mi configuración de la Zero W a esta, con una notable mejora de rendimiento. Aún no tengo claro que haya llegado a exprimir esta placa al 100%. Uno de sus defectos sería la cantidad de memoria con la que viene, 512MB, y es que con esta memoria es fácil que el sistema empiece a hacer swapping, o termine matando los procesos que consumen demasiada memoria...

Sin duda recomiendo comprar esta placa para esa gente que quiera empezar o que quiera dedicar una única Raspberry para domótica.

### Raspberry Pi 4B 4GB (61€)

![Raspberry Pi 4B photo](/images/raspberry-pi-4-b.jpg)

Aún la estoy configurando. Podemos considerar que esta es la Raspberry más potente (y cara) disponible actualmente. Por su elevado precio podéis imaginaros que con esta Raspberry no tendremos problemas de rendimiento, será capaz de servir Home Assistant, Plex, Deluge, Nextcloud y una base de datos **al mismo tiempo**. Eso sí, tendréis que comprar un ventilador y disipadores para que no se queme. 

Lo mejor de esta Raspberry es que con tanta memoria es difícil que el sistema empiece a hacer swapping, por lo que el servicio no se degrada con tanta facilidad.

Recomiendo esta Raspberry a aquella gente que no le importe invertir más al principio, y es que con sólo una Raspberry como ésta podréis montar servidores de domótica, Torrent, y demás cosas.

## Tabla comparativa

| Modelo                 | CPU                   | RAM   | Conectividad                 | Precio | Comprar |
|------------------------|-----------------------|-------|------------------------------|--------|---------|
| Raspberry Pi Zero W    | 1GHz, 1-core CPU | 512MB | Wifi b/g/n, Bluetooth 4.1/BLE |    11€ | [Kubii](https://www.kubii.es/raspberry-pi-3-2-b/1851-raspberry-pi-zero-w-kubii-3272496006997.html)   |
| Raspberry Pi 3A+       | 1.4GHz, 4-core CPU | 512MB | Wifi b/g/n/ac, Bluetooth 4.2/BLE |    27€ | [Kubii](https://www.kubii.es/raspberry-pi-3-2-b/2334-raspberry-pi-3-modelo-a-kubii-652508442181.html)   |
| Raspberry Pi 4B (2GB)    | 1.5GHz, 4-core CPU | 2048MB | Wifi b/g/n/ac, Bluetooth 5.0/BLE, 1x Gigabit Ethernet |    49€ | [Kubii](https://www.kubii.es/raspberry-pi-3-2-b/2771-nuevo-raspberry-pi-4-modelo-b-2gb-0765756931175.html)   |
| Raspberry Pi 4B (4GB)    | 1.5GHz, 4-core CPU | 4096MB | Wifi b/g/n/ac, Bluetooth 5.0/BLE, 1x Gigabit Ethernet |    61€ | [Kubii](https://www.kubii.es/raspberry-pi-3-2-b/2772-nuevo-raspberry-pi-4-modelo-b-4gb-0765756931182.html)   |
