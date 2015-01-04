# Introducción

Este repositorio contiene un ejemplo del fichero de configuración [fig](http://www.fig.sh/index.html) para instanciar MySQL (servicio de Base de Datos). Está basado en el contenedor Docker [luispa/base-mysql](https://registry.hub.docker.com/u/luispa/base-mysql/) (GitHub [base-mysql](https://github.com/LuisPalacios/base-mysql)). Mi contenedor está basado en el oficial [aquí](https://registry.hub.docker.com/_/mysql/) y [aquí](https://github.com/docker-library/mysql).

Veamos el ejemplo de uso: montar varios contenedores para dar un servicio de Correo electrónico y que todos utilicen la misma base de datos. Consulta este [apunte técnico sobre varios servicios en contenedores Docker](http://www.luispa.com/?p=172) para acceder a todos los contenedores Docker y fuentes en GitHub.


## Ejecución con "fig"

Para automatizar con el programa [fig](http://www.fig.sh/index.html) y que arranquen el contenedor descarga y renombra el fichero fig-template.yml, modifica las variables y ejecuta el programa: 

    $ git clone https://github.com/LuisPalacios/servicio-db-correo.git
    :
    $ mv fig-template.yml fig.yml   (edita a tu gusto)
    :
    $ fig up -d


# Personalización

La primera vez que arranques el contenedor es muy importante porque analizará si es necesario crear la estructura MySQL en el Volumen. Si lo encuentra vacío la creará y la contraseña de root será la que indiquemos en la variable MYSQL_ROOT_PASSWORD. Si por el contrario encuentra una estructura ya existente entonces la utilizará.


### Volumen

Directorio persistente para la estructura MySQL, debe apuntar a un directorio de tu HOST (/Apps/data/correo/db/mysql) que se montará en el contenedor como /var/lib/mysql. En mi caso uso este servicio para BD de correo.

   - "/Apps/data/correo/db/mysql:/var/lib/mysql"  


### Variable: MYSQL_ROOT_PASSWORD

Contraseña del usuario "root" que se asignará a MySQL si descubre el directorio vacío y necesita crear la estructura inicial. 


### Puertos

Este servicio expone el puerto 33000 para acceder a MySQL. Por defecto MySQL escucha en el puerto 3306, pero en mi caso lo he cambiado porque este fichero fig.yml lo utilizo junto con varios contenedores para dar un servicio de correo y he elegido este puerto de manera específica. 

	- "33000" - Puerto a emplear para que otros contenedores externos conecten. 
	
