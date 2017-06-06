---
title:  		"¿Cómo funciona el internet?"
permalink: 	 blog/como-funciona-internet
category:    front-end
feature_image: recommend-internet
read_time: 8
layout: post-sidebar
description: "¿Alguna vez te has preguntado, qué pasa desde que mandas un mensaje, hasta que el chulito queda en azul?"
tags:  "internet, ip, protocolos, paquetes"
---

Internet nos sirve en nuestro día a día para conocer el clima, las películas en cartelera, comunicarnos con nuestros amigos, hacer reservaciones en hoteles, comprar tiquetes aéreos, en fin, miles de cosas que quizá hasta nuestro tíos y abuelos han aprendido ha hacer poco a poco, porque familia colombiana que se respete tiene un grupo en WhatsApp donde siempre hay una tía que manda imágenes de Piolín u oraciones.

## ¿Alguna vez de has preguntado, que pasa desde que mandas un mensaje, hasta que el chulito queda en azul?
<br>
Cuando estás conectado a Internet tu computador/celular/tablet, tiene un código único(así como nosotros tenemos la cédula), ese código se llama la dirección IP(Protocolo de Internet), la cuál se compone de cuatro cifras de números, separados por puntos(.) y esos números son del 0 al 255, por ejemplo: 192.168.0.1

*Luego de que tu computador está conectado a Internet y tiene una IP única. ¿Cómo haces para mandarle un mensaje a una amiga?*

Digamos que por ejemplo tu tienes asignada la IP 1.2.3.4 y el tu amiga tiene la IP 5.6.7.8. para mandarle una "Hamburguesas a 10 mil en el [Burger Master Medellín](https://www.facebook.com/burgermasterco/)!!" a tu amiga, ese mensaje debe ser convertido a señales electrónicas, luego enviado por internet, y por último se vuelve a convertir en el texto normal, es decir: "Hamburguesas a 10 mil en el [Burger Master Medellín](https://www.facebook.com/burgermasterco/)!!".

¿Cómo es esto posible?

Esto es posible gracias al protocolo de conexión de redes TCP/IP. Un protocolo es un conjunto de reglas a las que se tiene que atener todas la compañías y productos de software con él fin de que todos sus productos sean compatibles entre ellos. Este protocolo está dividido por capas.

Así que para mandar el mensaje desde tu computador con la IP 1.2.3.4 a la de tu amiga con la IP 5.6.7.8 pasa lo siguiente:

**1.** El mensaje comenzaría en la capa superior e irá de manera descendente. Si el mensaje es muy largo, se divide en pequeñas partes, llamadas paquetes.

**2.** Los paquetes pasan por la capa de aplicación y continúan con la capa TCP. A cada paquete se le asigna un número de puerto, el puerto es muy importante porque necesitamos saber qué programa en el equipo de destino recibirá el mensaje.

**3.** Después de pasar por la capa TCP, los paquetes pasan a la capa IP. Aquí es donde cada paquete recibe su dirección de destino, en este caso 5.6.7.8.

**4.** Ahora que nuestros paquetes de mensajes tienen un número de puerto y una dirección IP, están listos para ser enviados a través de Internet. La capa de hardware se encarga de convertir nuestros paquetes que contienen el texto alfabético de nuestro mensaje en señales electrónicas y transmitirlos

**5.** En el otro extremo(en la casa de tu amiga), el ISP(proveedor de serivicios de internet: claro, UNE, etc) tiene una conexión directa a Internet. El enrutador ISPs examina la dirección de destino en cada paquete y determina dónde enviarlo.

**6.** Eventualmente, los paquetes llegan a la computadora 5.6.7.8. (la de tu amiga) Aquí, los paquetes comienzan comenzaría en la parte la capa inferior e irá de manera ascendente

**7.** A medida que los paquetes van hacia arriba, todos los datos de enrutamiento que la pila del equipo emisor(el tuyo) añadió, como dirección IP y número de puerto, se quitan de los paquetes.

**8.** Cuando los datos llegan a la capa superior, los paquetes han sido re-ensamblados en su forma original, "Hamburguesas a 10 mil en el [Burger Master Medellín](https://www.facebook.com/burgermasterco/)!!"

Y es así como tu y tu amiga se pudieron comunicar gracias a Internet y podrán ir a comer Hamburguesas a 10 mil en el [Burger Master Medellín](https://www.facebook.com/burgermasterco/)!!

Por último, escribe en tu navegador la IP 31.13.73.36, ¿te llevó a Facebook? Así es, a cada nombre de dominio(facebook.com) corresponde una dirección IP, pero puede haber varios nombres que compartan una dirección, pero de esto hablaremos en otra ocasión con más detalle, espero que te haya gustado mi artículo!
