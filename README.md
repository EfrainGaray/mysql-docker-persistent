# Mysql - Docker - Persistente

Explicare breve mente como crear una imagen Docker con un volumen persistente que puedas acceder desde tu ambiente local 127.0.0.1:3606

## Pre requisitos

Para poder crear esta imagen necesitaras tener Docker instalado.
Instacion en Windows por [chocolatey](https://chocolatey.org/) [docker-desktop](https://chocolatey.org/packages/docker-desktop)

```bash
choco install docker-desktop --pre 
```

Instacion en Mac por [Homebrew](https://brew.sh/index_es)

```bash
brew install docker
```


## Creacion de la instancia


## Mac o Linux
```bash
> git clone https://github.com/EfrainGaray/mysql-docker-persistent.git
> cd .\mysql-docker-persistent\
> docker volume create mysql-db-data
> docker run --name mysql -e MYSQL_ROOT_PASSWORD=TUPASSWORD -d -p 3306:3306 -v mysql-db-data:/var/lib/mysql -v $PWD/:/etc/mysql/conf.d  mysql/mysql-server:latest

```
## Windows
```bash
> git clone https://github.com/EfrainGaray/mysql-docker-persistent.git
> cd .\mysql-docker-persistent\
> docker volume create mysql-db-data
>  docker run --name mysql -e MYSQL_ROOT_PASSWORD=TUPASSWORD -d -p 3306:3306 -v mysql-db-data:/var/lib/mysql -v %cd%/:/etc/mysql/conf.d  mysql/mysql-server:latest

```

Si todo salio bien ya tienes creada tu imagen MySql solo nos falta dar permiso al usuario root para que podamos ingresar desde nuestro IDEfavorito.

```bash
> docker exec -it mysql mysql -p (Te solicitara tu password)
mysql> USE mysql;
mysql> CREATE USER 'root'@'%' IDENTIFIED BY 'tupassword';
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';
mysql> FLUSH PRIVILEGES;
mysql> exit;
```
Listo Ahora con los permisos actualizados para que se pueda acceder desde cualquier ip estas listo para poder conectarte

NOTA: Esto es solo para uso en ambientes de desarrollo en ningún caso usar esta configuración 'root'@'%' en servidores de producción.

## License
[MIT](https://choosealicense.com/licenses/mit/)
