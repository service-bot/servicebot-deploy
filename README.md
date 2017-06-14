# ServiceBot Docker Deployment

## ServiceBot runs the following containers:
- PostgreSQL
- ServiceBot

## Volumes 
  - upload-data -- contains user uploaded files 
  - environment-file -- contians the environment file of servicebot
  - </cert/path>:/usr/src/app/ssl -- host volume containing the SSL certs,
    links to the /usr/src/app/ssl folder in the servicebot container. 
    Needs to be configured.

## Steps:

#### Install [Docker](http://docs.docker.com/installation/) and [Docker Compose](https://docs.docker.com/compose/install/).

#### Create a folder on server and place SSL Certificate files in it
Certificates should be named as follows:
- Keyfile : servicebot.key
- Certificate : servicebot.crt
- CA : servicebot_bundle.crt



#### Configure docker-compose.yaml File

For SMTP Edit and uncomment the following lines to match
 your SMTP server information, 
 
    SMTP_HOST : "localhost"
    SMTP_USER : "postmaster@localhost"
    SMTP_PASSWORD : "password"
    SMTP_PORT : "587"

if SMTP password has a $ you need to escape it with an additional $, see the [docker-compose documentation](https://docs.docker.com/compose/compose-file/#variable-substitution) for more information

For SSL, uncomment the two SSL lines and change /path/to/ssl/certs/on/server
to the path on your server`that you created for the certificates
     
      CERTIFICATES: "./ssl/"
      - /path/to/ssl/certs/on/server:/usr/src/app/ssl


#### Build Images
    
    docker-compose build
#### Start containers in background:
    
    docker-compose up -d
## Helpful commands
#### Restarting all containers:
    
    docker-compose restart
#### View logs from all services:
    
    docker-compose logs
