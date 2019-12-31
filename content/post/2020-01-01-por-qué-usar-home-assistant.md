+++
authors = ["aleix-murtra"]
date = "2019-12-31"
draft = false
excerpt = "Recomiendo centralizar la gestión de vuestros dispositivos desde una Raspberry Pi. Podréis integrar dispositivos de distintas marcas, mejorar la privacidad y seguridad, conectar APIs, y un largo etc."
hero = "/images/home-assistant-screenshot.jpg"
timeToRead = 7
title = "Por qué uso Home Assistant"

+++
 
Aunque lo parezca, no me pagan nada por hacerles publicidad. De echo, existen alternativas a [Home Assistant](https://www.home-assistant.io/) como [OpenHab](https://www.openhab.org/) o [DomoticZ](https://www.domoticz.com/). Os sugiero probar las distintas opciones y quedaros con aquella que más os convenza. Para todas las soluciones se aplican las mismas ventajas. Al final como veréis es una cuestión de privacidad, seguridad e integración. Mientras controléis vuestros dispositivos desde una Raspberry Pi, estaréis protegidos :)

### Controlo mi localización

Me gusta crear automatismos según mi ubicación, tipo: desactivar la calefacción si estoy lejos de casa, encenderla cuando esté de camino a casa o activar la alarma cuando me vaya de casa. Lo que no me gusta es mandar mi ubicación a servicios de terceros, así que actualmente me mando la ubicación a [un servidor MQTT](https://www.home-assistant.io/integrations/owntracks/) que tengo configurado en mi Raspberry usando una aplicación de Android. Así pues, **solo mi Raspberry sabe dónde estoy**.

### Integro dispositivos de distintas marcas

Una cosa que suele pasar es que, ya sea por curiosidad o por necesidad, terminamos comprando dispositivos de distintas marcas. Tengo sensores de temperatura interiores de Xiaomi con Bluetooth, sensores exteriores BeeWi Bluetooth, sensores de movimiento de Xiaomi, luces de IKEA, rieles Sonoff, enchufes Wifi Broadcom... 

[Home Assistant dispone de más de 1500 integraciones](https://www.home-assistant.io/integrations/), con lo que podemos crear **automatismos usando dispositivos de distintas marcas**.

### Una única interfaz para controlarlo todo

Cada servicio suele tener su propia aplicación Android. *eWeLink* para los enchufes Sonoff, *IKEA Smart Home* para las luces de IKEA, *Xiaomi Home* para Xiaomi, y un largo etc. 

Con Home Assistant podemos usar su panel para controlar luces, enchufes, escenas, sensores, automatismos, etc. Yo, por ejemplo, tengo un tablet en la pared con la interfaz abierta 24/7.

### No quiero enviar datos a otras nubes

Para poder usar los enchufes/luces desde fuera de casa con sus aplicaciones nativas (*eWeLink*, *IKEA*, *Xiaomi*, ...), estos mandan/reciben información hacia/desde sus nubes privadas. Como mínimo sabemos que estas nubes saben cuando encendemos/apagamos luces, por lo que pueden saber nuestras rutinas. Pero es que además podríamos estar mandando más datos de los que creemos... 

Para todo esto, prefiero que Home Assistant hable con los gateways/hubs que tenemos en casa, y **bloquear el tráfico saliente desde los gateways/hubs o dispositivos**. Spoiler, aún no lo he hecho.

### Controlo cosas no-smart

Por ejemplo, mis sensores de temperatura interiores y exteriores son Bluetooth, y por defecto no se pueden integrar con absolutamente nada. Con la interfaz bluetooth de la Raspberry y Home Assistant podemos graficar las temperaturas y crear automatismos... ¡hasta podemos crear un climatizador con un sensor Bluetooth y enchufes Wifi!

### Para conectar APIs

![Home Assistant - Home to Work by Bus](/images/home-assistant-home-to-work-bus.jpg)

Tendemos a pensar que Home Assistant sirve para interconectar dispositivos, y no sirve únicamente para esto. En mi panel puedo revisar cuando pasará el siguiente bus que me lleva al trabajo, la disponibilidad de bicis Bicing a mi alrededor, la contaminación de mi zona y la de la zona del trabajo, el tiempo que tardo en ir en coche... y además puedo graficarlo todo, ¡por lo que hasta podría buscar patrones!

![Home Assistant - Bicing Llacuna](/images/home-assistant-bicing-llacuna.jpg)

### Sistema de seguridad

Cuando estamos de viaje nos gusta saber que nuestra casa está segura. Por eso tenemos un modo de alerta que pone sonidos en el Google Home, Alexa y Xiaomi Gateway mientras enciende y apaga las luces de casa, para que el ladrón se asuste y se vaya. En caso de que no lo haga, tenemos varias cámaras Xiaomi (hay que usar su app) y con Raspberry Pi Zero W (usando `ffmpeg`) que están grabando, por lo que en cualquier caso podemos ver quién ha entrado. A parte de esto, el sistema está configurado para mandar notificaciones al móbil si los sensores detectan movimiento, si se enciende cualquier luz, etc.