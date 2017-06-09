---
title:  		"Autenticación con redes sociales en Rails"
permalink: 	 blog/rails-autenticar-con-redes-sociales
category:    back-end
feature_image: recommend-omniauth
read_time: 15
description: "Aprende a hacer una aplicación donde el usuario se autentique con su red social favorita: Facebook, Twitter, Github, Instagram"
tags:  "autenticación, rails, twitter, github"
---

En este post te enseñaré a autenticar en Rails con una red social, en este ejemplo lo haré para auntenticarse con GitHub, tu lo puedes hacer con la red social que prefieras: Facebook, Twitter, Instagram, Linkedin, etc.

¿No tienes instalado Rails? Visita este link donde según tu sistema operativo sabrás qué debes instalar. [Clic aquí para instalar rails](http://installrails.com/steps/choose_os)

**Paso 1. Crear un nuevo proyecto:** Yo le pondré *github_login*, para esto, en la terminal escribimos: `rails new github_login`

**Paso 2. Instalamos la Gemas:** Existe una gema llamada [Devise](https://github.com/plataformatec/devise/) que nos permite hacer la autenticación de usuarios de una manera muuy fácil, la usaremos para integrarla con la otra gema que necesitamos que depende de la red social que queramos usar, por ejemplo yo usaré github entonces necesitaré la gema de [omniauth-github](https://github.com/intridea/omniauth-github), si tu vas a usar por ejemplo facebook, debes instalar poner `omniauth-facebook`

Para que veas todas las redes sociales disponibles para realizar la autenticación ingresa a este [link](https://github.com/omniauth/omniauth/wiki/List-of-Strategies)

```ruby
# Gemfile
gem 'devise'
gem 'omniauth-github'
```
En la terminal escribimos `bundle install`, para instalar las nuevas gemas

**Paso 3. Configuramos Devise:** Nuestro modelo se va a llamar User, Devise nos creará formularios para iniciar sesión, registarse, editar información de usuario y la lógica asociada, para esto en la terminal escribimos:

```
rails generate devise:install
rails generate devise User
rake db:migrate
```

**Paso 4. Creamos una migración:** Añadiremos cuatro columnas nuevas en nuestro modelo User que acabmos de crear, serán: provider, uid, name, image. Desde la terminal escribimos:
`rails g migration AddColumnsToUsers provider uid name image`

**Paso 5. Obtener credenciales de desarrollador en la red social:**
Busca en la red social que quieras usar, en las opciones de desarrollador, como registrar una aplicación, en mi caso para hacerlo con github visité [https://github.com/settings/developers](https://github.com/settings/developers)

Cuando la estés registrando, cuando te pregunten por callback URL, escribes http://localhost:3000/users/auth/github/callback, si es otra red social solo debes cambiar **github** , por ejemplo:

[Facebook](https://developers.facebook.com/docs/apps/register#): http://localhost:3000/users/auth/facebook/callback

[Twitter](https://apps.twitter.com/): http://localhost:3000/users/auth/twitter/callback

**Paso 6. Editar el archivo devise.rb:** En este archivo se encuentra la configuración de Devise, aquí debemos guardar la información que nos generó el registro de la aplicación (Client ID y Client Secret), se debe poner dentro de comillas, aunque yo te recomiendo usar variables de entorno, para que no pongas esa información publica, si quieres saber cómo visita este [link](https://github.com/laserlemon/figaro)

```ruby
# /config/initializers/devise.rb
config.omniauth :github, "CLIENT_ID", "CLIENT_SECRET"
```

**Paso 7. Editar el modelo user.rb:**
```ruby
# /app/models/user.rb
class User < ApplicationRecord
  # Include default devise modules. Others available are:
  # :confirmable, :lockable, :timeoutable and :omniauthable
  devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :trackable,
         :omniauthable, :omniauth_providers => [:github]


  def self.from_omniauth(auth)
    where(provider: auth.provider, uid: auth.uid).first_or_create do |user|
      user.email = auth.info.email
      user.name = auth.info.nickname
      user.image = auth.info.image
      user.password = Devise.friendly_token[0,20]
    end
  end
end
```


**Paso 8. Editar el archivo routes.rb:** Debemos añadir la ruta del callback
```
#/config/routes.rb
devise_for :users, controllers: { omniauth_callbacks: "users/omniauth_callbacks" }
```
**Paso 9. Crear controlador omniauth_callbacks_controller.rb:** Primero dentro de la carpeta controllers, creamos otra carpeta llamada *users* y dentro de users, creamos un archivo *omniauth_callbacks_controller.rb* y dentro de este archivo vamos a poner:
```ruby
# /app/controllers/users/omniauth_callbacks_controller.rb
class Users::OmniauthCallbacksController < Devise::OmniauthCallbacksController
  def github
    @user = User.from_omniauth(request.env["omniauth.auth"])

    if @user.persisted?
      sign_in_and_redirect @user, :event => :authentication #this will throw if @user is not activated
      set_flash_message(:notice, :success, :kind => "Github") if is_navigational_format?
    else
      session["devise.github_data"] = request.env["omniauth.auth"]
      redirect_to new_user_registration_url
    end
  end
end
```

**Paso 10. Pegar el link de inciar sesión:** Creamos un controlador con el nombre de *pages* y con una acción llamada *home* donde vamos a pegar nuestro link, dese la terminal creamos el controlador: `rails g controller pages home`

Añadimos en el archivo home.html.erb lo siguiente:
```HTML
# /app/views/pages/omniauth_login.html.erb
<div class="wrapper">
  <div class="container">
    <h1 class="title">Github OmniAuth Login</h1>
    <div class="user__container">
      <% if user_signed_in? %>
        <img src="<%= current_user.image %>" alt="profile picture" class="user__image">
        <p class="user__info">Username: <%= current_user.name %></p>
        <p class="user__info">Email: <%= current_user.email %></p>

        <%= link_to 'Logout', destroy_user_session_path, method: :delete , class: "user__link" %>
      <% else %>
        <%= link_to "Sign in with GitHub", user_github_omniauth_authorize_path, class: "user__link" %>
      <% end %>
    </div>
  </div>
</div>
```

En la terminal corre: `rails server` y visita http://localhost:3000/pages/home y listo!

[![github login devise omniauth anamariasosa](/assets/img/posts/omniauth_login.gif)](http://railstutoriales.herokuapp.com/pages/omniauth_login)

Así me quedó el [mío](http://railstutoriales.herokuapp.com/pages/omniauth_login), si le quieres añadir css o revisar mi código te dejo el link del repositorio  [aquí](https://github.com/anamariasosam/omniauth_rails_example), si tienes alguna pregunta no dudes en escribirme!!
