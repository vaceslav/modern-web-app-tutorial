# Docker

## DEMO 1

    docker run -d -p 8080:80 nextcloud

## DEMO 2

create docker compose file **docker-compose.yml**

    version: '3.3'

    services:
        db:
            image: mysql:5.7
            volumes:
                - db_data:/var/lib/mysql
            restart: always
            environment:
                MYSQL_ROOT_PASSWORD: somewordpress
                MYSQL_DATABASE: wordpress
                MYSQL_USER: wordpress
                MYSQL_PASSWORD: wordpress

        wordpress:
            depends_on:
                - db
            image: wordpress:latest
            ports:
                - "8080:80"
            restart: always
            environment:
                WORDPRESS_DB_HOST: db:3306
                WORDPRESS_DB_USER: wordpress
                WORDPRESS_DB_PASSWORD: wordpress
    volumes:
        db_data:

remove container and start again

delete db_data volume (remove container before)

    docker volume ls
    docker volume rm VOLUME_NAME

## DEMO 3

* create angular app
* create docker file **Dockerfile**

Content

    ### STAGE 1: Build ###

    # We label our stage as 'builder'
    FROM node:9-alpine as angular-builder

    COPY package.json yarn.lock angular.json ./

    #RUN npm set progress=false && npm config set depth 0 && npm cache clean --force

    ## Storing node modules on a separate layer will prevent unnecessary npm installs at each build
    #RUN npm i && mkdir /ng-app && cp -R ./node_modules ./ng-app
    RUN yarn && mkdir /ng-app && cp -R ./node_modules ./ng-app

    WORKDIR /ng-app

    COPY . .

    ## Build the angular app in production mode and store the artifacts in dist folder
    #RUN $(npm bin)/ng build --prod --build-optimizer
    RUN  yarn build --prod --build-optimizer --progress=no


    # Stage 2
    # Stage 1, based on Nginx, to have only the compiled app, ready for production with Nginx
    FROM nginx:1.13.3-alpine

    COPY ./nginx-custom.conf /etc/nginx/conf.d/default.conf
    ## Remove default nginx website
    RUN rm -rf /usr/share/nginx/html/*

    ## From 'builder' stage copy over the artifacts in dist folder to default nginx public folder
    COPY --from=angular-builder /ng-app/dist/APP_NAME /usr/share/nginx/html

    CMD ["nginx", "-g", "daemon off;"]

create file **./nginx-custom.conf**

    server {
        listen 80;
        sendfile on;
        default_type application/octet-stream;

        gzip on;
        gzip_http_version 1.1;
        gzip_disable      "MSIE [1-6]\.";
        gzip_min_length   1100;
        gzip_vary         on;
        gzip_proxied      expired no-cache no-store private auth;
        gzip_types        text/plain text/css application/json application/javascript application/x-javascript text/xml application/xml application/xml+rss text/javascript;
        gzip_comp_level   9;

        root /usr/share/nginx/html;

        location / {
            try_files $uri $uri/ /index.html =404;
        }
    }

run followed commandos

    docker build -t myapp .
    docker run -p 8080:80 myapp