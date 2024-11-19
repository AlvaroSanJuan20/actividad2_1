# Ejercicio 1: Introducción a Jekyll
`por Alvaro San Juan - ASIR2 (2024/2025)`

En esta actividad aprenderemos a crear nuestra propia página web de Jekyll mediante el uso de una máquina virtual de Debian, GitHub y VS code.



## Preparación de la MÁquina Virtual Debian

> Primero vamos a tener que poner la red correcta para que nos podamos conectar a VS code, para ello vamos a /etc/network/interfaces y configuramos el archivo interfaces con la siguiente configuración:

```
auto lo
iface lo inet loopback

#Configuración IPv4
auto enp0s3
#allow-hotplug enp0s3
iface enp0s3 inet static
#iface enp0s3 inet dhcp
address 10.0.22.2XX
netmask 255.255.255.0
gateway 10.0.22.254
dns-nameservers 10.0.1.48 10.0.1.54
```

> Con la máquina creada tendremos que instalar SSH para asegurarnos que podemos conectarnos a VS code, se usará **sudo apt-get install openssh-server**. Cuando lo tengamos pasaremos a instalar lo requerido para hacer el server. Para conectarnos a la máquina de Debian tendremos que hacer F1 > New SSH host y pondremos **ssh "usuario"@"ip"**.

> Instalaremos ruby en nuestra máquina Debian para poder tener la base para la creación de la página de Jekyll, para instalar ruby usaremos este comando:

```
sudo apt-get install ruby-full build-essential zlib1g-dev
```

> Para evitar que los paquetes ruby en el usuario root tendremos que configurar un directorio de instalación "gem", usaremos los siguientes comandos.

```
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

> Con todo esto podremos usar **gem install jekyll bundler** para instalar el bundler de jekyll.


## Creación de un sitio de Jekyll

> Para empezar creando la página de Jekyll vamos a tener que crear un repositorio llamado "myblog" con el complemento **Add .gitignore | .gitignore template Jekyll**. Al hacer esto se nos creará una rama main con un archivo llamado ".gitignore".
>
> Ahora que tenemos creado el repositorio en GitHub haremos un clone en VS code donde trabajaremos en el, es recomendable crear una carpeta donde guardes los repositorios.

```
git clone *url de myblog repositorio*
```

> Con el repositorio clonado entraremos con un **cd /myblog** y crearemos la rama "gh-pages" con un **git branch "nombre"** y luego para usarla **git checkout "nombre"**. En la rama gh-pages tendremos que crear la página de Jekyll, para eso usaremos lo siguiente:

```
jekyll new .
o
jekyll new . --force
```

## Probar el sitio localmente

> Para probar el nuevo sitio Jekyll usaremos **bundle exec jekyll serve** lo cual procesará toda la información y al final nos dará la URL de nuestro sitio web, en mi caso la URL que me dio es la IP:Puerto/myblog que al hacer click y tener la conexión activa nos funcionará, en el momento que se cierre la sesión la página dejará de funcionar.

## Lo ultimo que se debe hacer

> Como ya sabemos que funciona podremos editarlo en "_config.yml" para que se vea más personalizado y propio, esto es la configuración que se debería seguir:
```
title: *tu titulo*
email: *tu email*
description: >- # this means to ignore newlines until "baseurl:"
  *tu descripción*
baseurl: "/myblog" # the subpath of your site, e.g. /blog
url: "https://*nombre de GitHub*.github.io" # the base hostname & protocol for your site, e.g. http://example.com
github_username: *tu GitHub username*

# Build settings
theme: minima
plugins:
  - jekyll-feed
```
> Vamos a tener que hacer lo siguiente si queremos que los cambios al repositorio aparezcan en GitHub:

```
git add .

git commit -m "*comentario*"

git push -u origin gh-pages
```

> Al hacer esto el repositorio clonado subirá los nuevos archivos al repositorio creado en GitHub, aunque la página todavía queda por verla y para tenerla tendremos que ir a la configuración del repositorio, ir a pages y darle click al enlace de la página.
