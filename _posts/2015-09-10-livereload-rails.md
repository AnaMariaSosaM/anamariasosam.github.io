---
title:  		"Usar Livereload en Rails"
permalink: 	blog/rails-livereload
categories: back-end
read_time: 2
feature_image: recommend-ruby
description: Si estás cansado de refrescar el navegador cada que haces un proyecto en rails, usa livereload
tags: "ruby on rails, livereload, refrescar"
layout: post-sidebar
---

Si eres de los míos, que estás cansado de refrescar la pantalla cada vez que realizas un cambio te sugiero seguir estos pasos para que utilices livereload en tu proyecto de rails.

Pasos:

1. Instalar [Livereload](https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei?hl=en)
1. En el Gemfile en el bloque de desarrollo pega esto `gem 'guard-livereload', require: false`
1. Escribe `guard init livereload el cual te va a crear un Guardfile
	1. Si quieres que te recargue tus estilos en sass añadelo esto al guardfile en el bloque de livereload al final `watch(%r{(app|vendor)(/assets/\w+/(.+\.(scss|css))).*}) { |m| "/assets/#{m[3]}" }` debe quedarte así
1. Reinicia el servidor de rails y en otra pestaña escribe `guard`
1. Activa livereload haciendo clic sobre el icono y ¡listo!

![livereload rails guard anamariasosa](/assets/img/posts/livereload.gif)
