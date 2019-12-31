+++
authors = ["aleix-murtra"]
date = "2019-12-31"
draft = false
excerpt = ""
hero = "/images/hero-terminal-ls-root.jpg"
timeToRead = 10
title = "Cómo instalar Home Assistant"

+++

Si has llegado hasta aquí, posiblemente sea porque también quieres instalar Home Assistant. En ese caso, déjame que te ayude :)

## Instalar Raspbian

Bien, lo primero será instalar el sistema operativo. Evidentemente puedes instalar el que quieras, incluso puedes instalar la imagen ofrecida por Home Assistant, [Hass.io](https://www.home-assistant.io/hassio/installation/), lo que te simplificará mucho la instalación, pero no podrás usar esa Raspberry para mucho más.

Os recomendaría instalar Raspbian siguiendo el [tutorial oficial de Raspberry](https://www.raspberrypi.org/documentation/installation/installing-images/README.md). Está disponible para *Windows*, *Linux* y *Mac*.

## Instalar Home Assistant

Verás que hay dos modos de instalar Home Assistant en tu Raspberry Pi:
* Usando Docker ([Link documentación](https://www.home-assistant.io/docs/installation/docker/))
* Usando Python virtualenv ([Link documentación](https://www.home-assistant.io/docs/installation/virtualenv/))

Como verás, cada método tiene sus ventajas e inconvenientes...

### Docker 

No soy muy partidario de usar Docker si únicamente vamos a alojar un único servicio. Tampoco soy de usar Docker en servidores ARM, ya que tengo la sensación (no demostrada) de que el rendimiento es malo... aunque posiblemente se deba a un error mío de configuración.

La **ventaja** de éste método es que es fácil y rápido de configurar. Por contra, excepto por la configuración, estaréis creando una nueva instancia de Home Assistant desde cero cada vez que arranquéis el servicio. Esto significa que, en el caso de que uséis integraciones que requieran instalar librerias de Python adicionales a las que vienen en la imagen de Docker (como [HACS](https://github.com/hacs/integration)), éstas se instalaran **cada vez que levantéis el servicio**, por lo que los arranques pueden tardar más que con el otro método. 

Lógicamente, actualizar de una versión de Home Assistant a otra será tan fácil como cambiar el tag de la versión de Docker.

Para usar este servicio, podéis crear el directorio dónde alojaréis la configuración (`/srv/homeassistant`) e instalar Docker con estos comandos:

```shell
$ mkdir -p /srv/homeassistant/
$ curl -s https://get.docker.com/ | bash
```

Una vez hecho esto, podéis configurar el siguiente [servicio en SystemD](https://github.com/alemuro/ha-conf/blob/master/home-assistant-docker.service) usando el siguiente comando:

```shell
$ cat << EOF > /etc/systemd/system/home-assistant.service
[Unit]
Description=Home Assistant container
After=docker.service
Requires=docker.service

[Service]
ExecStart=/usr/bin/docker run \
                        --init \
                        --privileged \
                        -itd \
                        --name="home-assistant" \
                        -v /srv/homeassistant:/config \
                        -v /etc/localtime:/etc/localtime:ro \
                        --net=host \
                        --restart=always \
                        homeassistant/home-assistant:0.103.5
ExecStop=/usr/bin/docker stop home-assistant
ExecStopPost=/usr/bin/docker rm -f home-assistant
Type=simple
Restart=always
RemainAfterExit=yes
TimeoutSec=infinit

[Install]
WantedBy=multi-user.target
EOF
```

Luego recargamos la configuración de SystemD, configuramos el servicio para que se levante cuando iniciemos la Raspberry, y ya podemos levantar el servicio por primera vez.

```shell
$ systemctl daemon-reload
$ systemctl enable home-assistant
$ systemctl start home-assistant
```

El servicio **se expone automáticamente en el puerto `8123`** de la Raspberry. Os recomiendo configurar un *nginx* o cualquier reverse proxy.

Para revisar los logs, podemos ejecutar:

```shell
$ docker logs -f home-assistant
```

¡Y ya está! Podéis modificar la configuración en `/srv/homeassistant`. La primera vez que arranque el servicio se crearán todos los ficheros por defecto.

Fijaros también que la versión está "hardcodeada" dentro del fichero del servicio. Esto es porqué las imágenes tardan mucho en ser descargadas y descomprimidas en Raspberry, no quiero que el servicio esté caído 20-30 minutos al reiniciarlo.


### Virtualenv

Para mi, éste es el método más limpio de instalar Home Assistant. Es el método que me dá mejores resultados en rendimiento, mi setup pasó de tardar 5-10 minutos usando Docker a 30 segundos usando Virtualenv, sobretodo por no necesitar instalar todas las dependencias de *[HACS](https://github.com/hacs/integration)* cada vez que arranca el sistema. Por contra, es más difícil de configurar, y muchas veces necesitamos instalar aplicaciones en nuestro sistema para que se puedan usar desde Home Assistant (por ejemplo *ffmpeg* o *mariadbclient*).

Primero deberíamos preparar el directorio y dependencias (*python3* y *virtualenv*). En vez de alojar la configuración en la home del usuario, usaremos el mismo directorio que en el ejemplo de Docker.

```shell
$ mkdir -p /srv/homeassistant
$ apt-get install python3 python3-dev python3-venv python3-pip libffi-dev libssl-dev
$ python3 -m venv /srv/homeassistant/.virtualenv
```

Home Assistant es un binario en Python que está alojado en [pypi](https://pypi.org/project/homeassistant/). Usamos el *virtualenv* para no "contaminar" el sistema operativo con las dependencias del servicio. Para instalar HA, haremos source del virtualenv e instalaremos la librería.

```shell
$ source /srv/homeassistant/.virtualenv/bin/activate
$ python -m pip install homeassistant
```

Creamos el [servicio en SystemD](https://github.com/alemuro/ha-conf/blob/master/home-assistant-venv.service):

```shell
$ cat << EOF > /etc/systemd/system/home-assistant.service
[Unit]
Description=Home Assistant venv
After=network-online.target

[Service]
Type=simple
ExecStart=/srv/homeassistant/.virtualenv/bin/hass -c "/srv/homeassistant"

[Install]
WantedBy=multi-user.target
EOF
```

Recargamos la configuración de SystemD, activamos el servicio para que arranque a cada arranque de Raspberry, y iniciamos el servicio por primera vez.

```shell
$ systemctl daemon-reload
$ systemctl enable home-assistant
$ systemctl start home-assistant
```

Para ver los logs, podemos consultar *journalctl*:

```shell
$ journalctl --no-tail -f -u home-assistant
```

Para actualizar el servicio deberemos eliminar el *virtualenv* y volverlo a crear.