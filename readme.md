   

#### Before running add your superuser email/password and project name in docker/prod/env/.data.env file

    SUPERUSER_EMAIL=django@pool.com
    SUPERUSER_PASSWORD=secretp@ssword
    MICROSERVICE_TITLE=MyProject

#### Run the local develop server:

    docker-compose up -d --build
    docker-compose logs -f
    
##### Server will bind 8000 port. You can get access to server by browser [http://localhost:8000](http://localhost:8000)


#### Configuration for develop stage at 9000 port:
    docker-compose -f prod.yml -f prod.dev.yml up -d --build

##### The same configuration could be for stage and prod:
    docker-compose -f prod.yml -f prod.stage.yml up -d --build
    docker-compose -f prod.yml -f prod.prod.yml up -d --build


##### For testing mail backend you can use MailHog service
    docker-compose -f docker-compose -f docker/modules/mailhog.yml up -d --build
    docker-compose -f prod.yml -f prod.dev.yml -f docker/modules/mailhog.yml up -d --build

<b>Don't forget to set SMTP mail backend in settings</b>

#### For set https connection you should have a domain name
<b> In prod.certbot.yml: </b>

Change the envs:
    CERTBOT_EMAIL: your real email
    ENVSUBST_VARS: list of variables which set in nginx.conf files
    APP: value of the variable from list ENVSUBST_VARS
    
To set https for 2 and more nginx servers:
    
    ENVSUBST_VARS: API UI
    API: api.domain.com
    UI: domain.com
    
Run command:

    docker-compose -f prod.yml -f prod.certbot.yml up -d --build
    
### Will be added 

* PgBouncer
