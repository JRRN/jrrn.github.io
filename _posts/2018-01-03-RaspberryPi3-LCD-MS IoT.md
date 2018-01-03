---
layout: post
title: Raspberry Pi 3, LCD Display, C# y MS IoT
tags: MsIoT
---

### Raspberry Pi 3, LCD, C# y MS IoT

Hola hará un año o así, compré una Raspeberry Pi 3.

Mi idea era jugar un poco con ella tanto en su versión modo PC/Servidor como su versión IoT.

Durante este año, he jugado con ella, he probado varias distribuciones Raspbian, Arch Linux, Suse y Fedora, buscando cual era la más comoda, me ofrecía más prestaciones, etc...

En su día, este blog estuvo alojado con un nginx + PhP + postgreSQL + Wordpress, finalmente un día, se me quedó frita, y aunque tenía documentado paso por paso como levantarlo otra vez, decidí migrar a Github Pages.

Después de esta gran anécdota, decidí comprar un par de starter kits de elegoo, el Fun Kit y 37 Sensor Kit v 2.0 y ver si Microsoft había avanzado en este línea, que en sus comienzos era como una piedra, o la tenías de adorno o se la tirabas a alguien a la cabeza. Me sorprende que los sistemas Linux hayan podido montar todo el SO y Microsoft no, pero eso es otra charla, un ¿NANO Server?

En definitiva, os adjunto, el código y el esquema para poder enviar texto sobre una pantalla LCD desde la RPi3.

Esquema:

![lcddiagram](/img/lcdiot/lcddiagram.png "lcddiagram")

Por otro lado, el esquema en [Fritzing](http://fritzing.org/home/ "fritzing"), que si no lo conoceís, es un programa de código abierto que te permite crear los esquemas y diagramas con un montón de componentes.

[FritzingFile](/img/lcdiot/lcdfritzing.fzz "Fritzing File")

Y finalmente el código fuente:

[LCD](https://github.com/JRRN/MS_IoT "GitHub JRRN")

Nos vemos.