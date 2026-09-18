Reference commands:
https://docs.google.com/document/d/16DMON_Xe5pSr3qlZfvXryJCNnSKJCHD_6A9KQaGBkmA/edit?tab=t.irubio7wzg2r

# docker-node-react-mongo

Using docker to deploy three containers of Node(backend), React(frontend), Mongo(database)

Follow all the steps to make sure frontend, backend, database are connected and tested successfully

Main Commands used:

1.  First try connecting Frontend, Backend, mongodb locally in system
    Check if all individual are connecting together properly using network

    Reference:
    https://github.com/lokeshp-797/steps-react-node-mongodb

Create docker networking to make sure UI, Backend, DB communicate effectively:

Docker network ls
Docker network create goals-net

2.  ---- Dockerizing mongodb (Database) ----
    Run Mongodb in network:
    docker run --name mongodb --rm -d --network goals-net mongo

        <!-- docker run --name mongodb --rm -d -p 27017:27017 mongo -->

        Run node app.js locally which should connect to mongodb automatically

        Check from UI if entire connectivity is working fine

3.  ---- Dockerizing Nodejs (Backend) ----
    Create docker file for Nodejs

    Build image of nodejs again
    Docker build -t goals-node .

    Run the container in network
    docker run --name goals-backend --rm -d -p 80:80 --network goals-net goals-node

    <!-- docker run --name goals-backend --rm -d --network goals-net goals-node -->

    Local testing:
    Make changes to code below in app.js
    'mongodb://host.docker.internal:27017/course-goals'

    Create Nodejs image:
    docker build -t goals-node .

    Run Nodejs container:
    docker run --name goals-backend --rm -p 80:80 goals-node

    Now nodejs should able to connect with Mongodb

4.  ----- Dockerizing Reactjs (Frontend) ----
    Build image:
    docker build -t goals-react .

    Run reactjs container in network:
    docker run --name goals-frontend --network goals-net --rm -p 3000:3000 -it goals-react

    Run the docker reactjs container in interactive mode:
    docker run --name goals-frontend --rm -p 3000:3000 -it goals-react

We see now all the containers are communicating with each other using localhost using [localhost:](http://localhost:3000/)

For using volumes and data persistence use below code:
Location:
GoogleDocs
Udemy_Devops Progress
Docs Link:
https://docs.google.com/document/d/16DMON_Xe5pSr3qlZfvXryJCNnSKJCHD_6A9KQaGBkmA/edit?tab=t.irubio7wzg2r

Local File Link:
Downloads/Solugenix_Udemy

Additional commands:
docker ps -a
docker images
docker stop <containerid>
docker rm <containerid>
docker rmi <imageid>

=======================
Another option
Can also run the docker compose file

Docker Compose

Create a docker-compose.yaml file in the root folder

No need to creating network in compose file. Docker itself creates all the resources together once everything is there in compose file

Delete all the images locally
Docker image prune
Docker image prune -a

Docker compose up

Docker compose down

Docker compose down -v => to delete the volumes

Docker compose up -d => to start in detach mode

Docker logs <backend containername> => we can see that its connected to mongodb

Now we can see it working from UI

To build only the images:
Docker-compose build => this will not start container
