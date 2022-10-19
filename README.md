<h1 align="center"> Tarefa 02 do Estágio Compass.uol</h1>
<center>
<img src="docker.png" alt="Não Encontrado!" title="Docker" height="300" width="600"/>
</center>
<h3>Subindo uma aplicação Wordpress + DB Mysql utilizando Docker: instalação</h3>
<!–# Tarefa 02 do Estágio Compass.uol Docker 

Para dar início ao nosso Container Docker com wordpress e Mysql iremos atualizar os pacotes da máquina Oracle Linux 8.6:

```apt-get update```

Em seguida, iremos instalar o Docker através do seguinte comando:

```apt-get -y install docker.io```

Após a instalação do docker será necessário instalar o docker-compose, pois é um conteúdo aparte do docker e que iremos utilizar para configurar o nosso container.
 Para instalação usamos o comando:
 
 ```sudo apt install docker-compose```
 
 e podemos verificar sua instalação com o comando:
 
 ```docker-compose --version```

Para iniciar o nosso container primeiro criamos uma pasta no diretório /:

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

Por último, rodaremos o nosso container com o seguinte comando:

```docker-compose up -d```

E para verificar seu funcionamento acessamos através do https://localhost:80
