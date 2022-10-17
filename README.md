# Tarefa02
Tarefa do Estágio Compass Docker

Documentação do container Wordpress com Mysql(Em máquina Linux):

Para dar inicio ao nosso Container Docker com wordpress e Mysql iremos atualizar os pacotes da maquina Linux:

```apt-get update```

Em seguida iremos instalar o Docker através do segunte comando:

```apt-get -y install docker.io```

Após instalar o docker desta forma no linux, ele não vem com a ferramenta docker-compose, que iremos utilizar para configurar nosso container.
 Para instalação usamos o comando:
 ```sudo apt install docker-compose```
 e podemos verificar sua instalação com o comando:
 ```docker-compose --version```

Agora para inicar nosso container primeiro criamos uma pasta:
```mkdir wordpress```

nesta pasta iremos criar nosso arquivo "docker-compose.yml", com as seguintes linhas de código:

```
version: '2'

services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: wordpass
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "80:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpass
volumes:
    db_data:
```


docker-compose up -d
