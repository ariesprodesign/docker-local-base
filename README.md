####################################
#          Setting.yaml            #
####################################
```
Neos:
  Flow:
    core:
      phpBinaryPathAndFilename: '/usr/bin/php'
    persistence:
      backendOptions:
        dbname: brylliant_dev
        user: root
        password: root
        host: db
        driver: pdo_mysql
        charset: utf8mb4
      doctrine:
        sqlLogger: Neos\Flow\Persistence\Doctrine\Logging\SqlLogger
    http:
      baseUri: https://local.brylliant.de/
```      
####################################
#          Routes.yaml            #
####################################
```
-
  name: 'Brylliant Main'
  uriPattern: '<BrylliantMainSubroutes>'
  subRoutes:
    'BrylliantMainSubroutes':
      package: 'Brylliant.Main'
-
  name: 't3n graphql'
  uriPattern: 'api/<t3nGraphQLSubroutes>'
  subRoutes:
    't3nGraphQLSubroutes':
      package: 't3n.GraphQL'
      variables:
        'endpoint': 'public'
```       
**********************************************************************************

####################################
#             Commands             #
####################################

# build image and create containers
```
docker-compose up -d
```
# List built docker images
docker images

# Delete one containers
```
docker stop <id> or <name>
docker rm <id> or <name>
```
# Stop all Containers
```
docker stop $(docker ps -a -q)
```
# Delete all containers
```
docker rm $(docker ps -a -q)
```
# Delete one images
```
docker rmi <id> or <name>
```
# Delete all images
```
docker rmi $(docker images -a -q)
```
#Start SSH on Container:
```
docker exec -i -t <id> bash #by ID
```
or
```
docker exec -i -t <name> bash #by Name
```

#update a image and container of image
```
docker-compose build --no-cache <short name>
```

#to identify the name of the machine <machine IP>
```
docker ls
```

#Getting a docker container's ip address from the host
```
docker inspect  <container id>
```

# Set permissons:
```
chown -R www-data:www-data /var/www/html/*
```

# Build new web Container
```
go into docker-compose folder
docker-compose build --no-cache web
docker-compose up -d
```


# install nano
# start new container
```
docker exec -it vowo-dev /bin/bash -c "export TERM=xterm; exec bash"
```

# clear pagespeed cache:
```
touch /var/ngx_pagespeed_cache/cache.flush
```
