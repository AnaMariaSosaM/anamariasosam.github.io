---
title:  		"Despliega páginas web con Surge.sh"
permalink: 	 blog/deploy-con-surge
category:    front-end
feature_image: recommend-surge
read_time: 5
description: "Surge nos permite desplegar nuestra página web, en solo tres pasos y lo mejor, sin salirnos de la terminal. Aquí te enseñaré como hacerlo"
tags:  "html, css, js, deploy, página web"
---

Surge nos permite desplegar nuestra página web, en solo tres pasos y lo mejor, sin salirnos de la terminal.

## Pasos para hacer nuestro primer deploy:
Desde nuestra terminal con npm lo instalamos de forma global para que desde cualquier carpeta de proyecto local podamos hacer uso de los comandos de surge.

` npm install --global surge`

Luego desde la terminal, buscamos nuestro proyecto que tiene html, css y js. Si lo quieres hacer desde una aplicación hecha con `create-react-app` recuerda que primero debes, correr el build `npm run build`

Luego que ya estés ubicado en la terminal en el proyecto que quieres publicar solo debes correr

`surge`

La primera vez te pedirá un email y contraseña, recuerda que todo esto es desde la terminal, luego si deseas puedes cambiarle el dominio, pero **no olvides** que debes dejar .surge.sh, es decir, solo puedes personalizar lo que hay antes de eso.

Por ejemplo en mi caso, creé un mini juego en react así que publico mi carpeta build y luego cuando en el dominio yo decidí llamarlo *devgame* así que escribo *devgame.surge.sh*

Así lo hice yo con mi proyecto de React js:

![react js deploy surge anamariasosa](/assets/img/posts/deploySurge.gif)

Eso es todo!, ahora puedo ingresar a mi nueva página a [devgame.surge.sh](http://devgame.surge.sh)


También puedes configurar tu propio dominio, puedes ver más información puedes visitar su página [surge.sh](https://surge.sh/) o me puedes preguntar a mí.
