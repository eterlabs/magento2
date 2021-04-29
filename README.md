![alt text](https://www.eterlabs.com/wp-content/uploads/2021/02/cropped-eterlabs-2.png)

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
* Instalar MySql en maquina local


#### Montado del proyecto


1.- Clonar el proyecto
```
git clone https://github.com/eterlabs/magento2.git
```

2.- Moverse al proyecto
```
cd magento2-docker
```

3.- Inicializa en ambiente de docker
```
docker-compose up -d
```

4.- Descarga magento 2 con composer
```
bin/composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .
```

5.- Crear base de datos limpia para instalar magento
```
mysql -u<user> -p -e 'CREATE DATABASE magento2;';
```

6.- Install Magento
```
bin/magento setup:install \
    --base-url="http://localhost:8070/"  \
    --db-host="host.docker.internal"  \
    --db-name="magento2"  \
    --db-user="root"  \
    --db-password="password"  \
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

7.- Reinicia nginx para cargar la configuración de magento
```
docker exec -ti magento2-nginx service nginx restart
```

8.- Probar el cambiente con entrando a la url:
```
http://localhost:8070
```
