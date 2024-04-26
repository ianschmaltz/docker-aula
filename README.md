# Aula Docker
## Resumo
Este projeto consiste na criação de contêineres Docker para um ambiente Node.js e um banco de dados MySQL. Os contêineres são configurados com mapeamento de portas, volumes e uma rede Docker. Um servidor Node.js é executado na porta 3000 e se comunica com o banco de dados MySQL. Os dados são exibidos em um front-end acessível pelo endereço localhost:3000.

## Códigos Bash
### Contêiner node: 
docker run -it --rm --name ian-node -v "$PWD:/usr/src/app" -w "/usr/src/app" -p "3000:3000" --network=ian-network node bash -c "npm install && node index"

### Contêiner mysql: 
docker run -d --rm --name ian-sql -v volume-mysql:/var/lib/mysql -p "3306:3306" --network=ian-network -e MYSQL_ROOT_PASSWORD=senhasecreta mysql <br>
docker exec -it ian-mysql bash

### Volumes: 
docker volume create ian-volume
#### *Note que ao rodar um docker inspect ian-volume, o "Mountpoint" é definido como "/var/lib/docker/volumes/volume-mysql/_data"

### Network: 
docker network create ian-network

### Conexão: 
docker network connect ian-network ian-node/ian-mysql <br>
docker network disconnect bridge ian-node/ian-mysql

## Comandos SQL

No bash do contêiner mysql: mysql -uroot -psenhasecreta <br><br>
CREATE DATABASE ian_db; <br>
SHOW DATABASES; <br>
USE ian_db; <br>
CREATE TABLE produto(id int NOT NULL AUTO_INCREMENT primary key, nome varchar(255) NOT NULL); <br>
SHOW TABLES; <br>
INSERT INTO produto (nome) VALUES ('Iphone 15'), ('Playstation 5'); <br>
SELECT * FROM produto; 

