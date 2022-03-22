# DOCKER UTILITÁRIO 

## DOCKER IMAGES
docker images

docker images | grep dang (filtra por dangling images)

docker images -f dangling=true.  (filtra imagens dangling)

docker images -f dangling=true -q (lista ids)

docker rmi $(docker images -f dangling=true -q)   - remove todas dangling images

### criar imagem por Dockerfile

docker build --tag centos_apache:v1  .

docker build -t nginx_custom:v1 -f Dockerfile2 .

docker build --tag centos_apache:v1  . (create images from dockefile)


### passando argumento

docker build -t apache_with_code:v8 -f Dockerfile3 --build-arg user=andre .

docker build -t apache_with_code:v9 -f Dockerfile3 --build-arg user=andre --build-arg httpd_package=httpd .



## DOCKER CONTAINER

docker stop container

docker start container

docker inspect container

docker rm -f $(docker ps -a -q) (remover todos containers)

docker ps (listar containers ativos)

docker container ls (listar containers ativos)

docker ps -a 

docker ps -l

docker exec -ti apache2 bash (entrar no container)

docker run -d -ti -p 9091:80 --name apache2 apache_with_code:v10 (Iniciar container com terminal)

docker run -d --name centos2 centos python -m SimpleHTTPServer 8080  (substituir CMD)

docker run —rm -ti centos bash (temporary container)

docker info | grep -i root 

alterar path save containers /lib/sytemd/system/docker.service

### criar container a partir de imagens
docker container create

docker run --name centos-test -d centos_apache:v1

docker run -d -p 9090:80  --name centos-yescmd centos_apache:v2


### criar imagem a partir de um container
docker commit cab2a2c047de final_test_centos (cria image from container)

### determinar limites de memória
docker run -d --name nginx2 --memory="200mb" nginx:alpine

docker run -d --name nginx3 --memory="200mb" --cpuset-cpus 0 nginx:alpine  (cpu)

### logs
docker stats f69de559efb9 (mostra hardware/memoria container)

docker logs 443811548a81d911f07221c681897ff02da5e725b26368d43ccf41b324c26f05


## DOCKER VOLUMES
docker volume create mysql_volume

docker volume ls

docker volume rm 

docker rm -fv

Library/Containers/com.docker.docker/Data/vms/0


### BIND VOLUMES
docker run -d -v /Users/andrenascimentodefreitas/Desktop/docker-course/mysql:/var/lib/mysql  --name mysql -e "MYSQL_ROOT_PASSWORD=12345" mysql:5.7

### NORMAL VOLUMES
docker run -d -v mysql_volume:/var/lib/mysql  --name mysql -e "MYSQL_ROOT_PASSWORD=12345" mysql:5.7

### DANGLING VOLUMES

docker volume ls -f=dangling=true

docker volume ls -f=dangling=true -q

docker volume rm $(docker volume ls -f=dangling=true -q)

## NETWORK SETTINGS
docker network ls

docker network ls | grep bridge

docker network inspect bridge


docker exec container1 bash -c "ping 172.17.0.3"

### CRIAR / DELETAR


Docker network create -d bridge --subnet 172.18.0.0/16 --gateway 172.18.0.1 new_network

docker network rm new_network

docker rm -fv $(docker ps -aq)

### CONECTAR CONTAINER DE DIFERENTES NETWORKS

docker network connect net1 net2

docker exec net1 bash -c "ping net2"

docker network disconnect net1 net2

docker run -dti --network test_network --ip 172.40.0.50 --name test1 centos


## DOCKER COMPOSE
docker-compose up -d

docker-compose down

docker-compose logs

### ESPECIFICAR DOCKER COMPOSE FILE

docker-compose -f docker-compose-mysql.yml up -d

docker-compose -f docker-compose-mysql.yml down


## TAGS

    -d run in background (deached mode)
    -f force command
    -p port
    —tag name from image
    –y option automatically answers yes to the confirmation prompt.
    —name name container
    -a all container running and processing
    --file docker build
    -e (envirement) -v create new volume
    Bash -c “command”
    Options: docker images  | grep centos ( filtrar por centos)
