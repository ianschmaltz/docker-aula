# Aula Docker
# Introdução

Este projeto consiste na criação de contêineres Docker para um ambiente Node.js e um banco de dados MySQL. Os contêineres são configurados com mapeamento de portas, volumes e uma rede Docker. Um servidor Node.js é executado na porta 3000 e se comunica com o banco de dados MySQL. Os dados são exibidos em um front-end acessível pelo endereço localhost:3000.

# Códigos Bash

### Contêiner node: 
docker run -it --rm --name ian-node -v "$PWD:/usr/src/app" -w "/usr/src/app" -p "3000:3000" --network=ian-network node bash -c "npm install && node index"

### Contêiner mysql: 
docker run -d --rm --name ian-sql -v volume-mysql:/var/lib/mysql -p "3306:3306" --network=ian-network -e MYSQL_ROOT_PASSWORD=senhasecreta mysql

### Volumes: 
docker volume create ian-volume
#### *Note que ao rodar um docker inspect ian-volume, o "Mountpoint" é definido como "/var/lib/docker/volumes/volume-mysql/_data"

### Network: 
docker network create ian-network

### Conexão: 
docker network connect ian-network ian-node/ian-mysql &&
docker network disconnect bridge ian-node/ian-mysql

