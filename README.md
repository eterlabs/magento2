![alt text](https://eterlabs.com/media/github-docker-eterlabs.jpg)

Este repositorio fue generado para aprender a montar Magento 2.4 usando las imágenes de Docker de Eterlabs, estas imágenes las creamos basadas en los requerimientos internos para desarrollo por lo tanto no es recomendable usarlas para ambientes productivos.

La principal razón para crearlas fue reducir el tiempo de esfuerzo al momento de montar los ambientes y así estandarizarlo en todos los proyectos, fue así como mejoramos al dejar de invertir de 1 a 2 días para montar un ambiente, ahora cualquier miembro del equipo puede hacerlo en tan solo dos horas.

Si te gusta este repositorio y te gustaría poder obtener más herramientas de desarrollo, síguenos en nuestras redes sociales.

* [Facebook](https://www.facebook.com/eterlabsmx)
* [Instagram](https://www.instagram.com/eterlabsmx/)
* [LinkedIn](https://www.linkedin.com/company/eterlabs)


Si te gustaría sugerir contenido o módulos envíanos un correo a contacto@eterlabs.com

Para usar este repositorio sigue los siguientes pasos:

#### Requerimiento Previos

* Instalar Docker
* Instalar MySQL en máquina local


#### Montado del proyecto


1.- Clonar el proyecto en tu máquina
```
git clone https://github.com/eterlabs/magento2.git
```

2.- Cuando el proyecto se descargue en tu máquina, muévete al directorio creado
```
cd magento2
```

3.- Inicializa el ambiente de Docker para poder comenzar la instalación
```
docker-compose up -d
```

4.- Se ejecutará el comando para la descarga de Magento 2.4
```
bin/composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .
```

5.- Ejecutamos el comando de instalación de Magento.
```
bin/magento setup:install \
    --base-url="http://localhost:8070/"  \
    --db-host="mariadb"  \
    --db-name="magento2"  \
    --db-user="magento"  \
    --db-password="magentopass"  \
    --admin-firstname="admin"  \
    --admin-lastname="admin"  \
    --admin-email="admin@misitio.com"  \
    --admin-user="admin"  \
    --admin-password="admin123"  \
    --language="en_US"  \
    --currency="USD"  \
    --timezone="America/Chicago"  \
    --use-rewrites="1"  \
    --backend-frontname="admin" \
    --session-save=files \
    --use-sample-data \
    --elasticsearch-host=elasticsearch \
    --elasticsearch-port=9200
```

6.- Cuando la instalación termine será necesario reiniciar nginx para cargar la configuración de Magento
```
docker exec -ti magento2-nginx service nginx restart
```

7.- Con todos estos pasos estarás listo para ver un Magento 2.4 corriendo en tu máquina
```
http://localhost:8070
```
