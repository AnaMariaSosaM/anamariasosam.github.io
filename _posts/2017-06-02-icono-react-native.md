---
title:  		"Crear un ícono para tu App de React Native"
permalink: 	 icono-react-native
category:    front-end
feature_image: recommend-native-icon
description: Aprende a añadirle el ícono en solo 7 pasos a tu aplicación de iOs y Android hecha con React Native.
tags: "react native, aplicación, icono, android, ios"
---

Con solo 7 pasos aprenderás a crear el ícono para tu aplicación hecha en react native.

Pasos:
1. En la terminal `npm install -g yo generator-rn-toolbox`
2. Instalar ImageMagick, [clic aquí para descargar](http://www.imagemagick.org/script/download.php), si tienes mac lo puedes instalar via Brew, en la terminal escribe: `brew install imagemagick`
3. Busca el ícono que quieres, el tamaño puede ser de 200x200px, puedes usar este de abajo:
<br>
![reactnative icon generator anamariasosa](/assets/img/posts/icon.png)
4. Creas una carpeta src en el root y lo guardas ahí
5. En la terminal `yo rn-toolbox:assets --icon src/icon.png`
6. Cuando te pregunten **Name of your react-native project** presionas enter
7. Luego cuando diga **Overwrite ios/nombreDelProyecto/Images.xcassets/AppIcon.appiconset/Contents.json?** escribes: `Y`

¡Listo, ahora tu aplicación de iOS y android tienen el ícono!

![reactnative icon generator anamariasosa](/assets/img/posts/iconReactNative.gif)
