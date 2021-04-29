#### Requerimiento Previos

* Instalar Docker
* Instalar MySql en maquina local

![alt text](https://www.eterlabs.com/wp-content/uploads/2021/02/cropped-eterlabs-2.png)

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

7.- Probar el cambiente con entrando a la url:
```
http://localhost:8070
```