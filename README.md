# docker-node-react-mongo

Using docker to deploy three containers of Node(backend), React(frontend), Mongo(database)

Follow all the steps to make sure frontend, backend, database are connected and tested successfully

Main Commands used:

1.  First try connecting Frontend, Backend, mongodb locally
    Check if all individual are connecting together properly

2.  ---- Dockerizing mongodb (Database) ----
    Docker run --name mongodb --rm -d-p 27017:27017 mongo

    Run node app.js locally which should connect to mongodb automatically

    Check from UI if entire connectivity is working fine

3.  ---- Dockerizing Nodejs (Backend) ----
    Create docker file for Nodejs

    Make changes to code below in app.js
    'mongodb://host.docker.internal:27017/course-goals'

    Create Nodejs image:
    docker build -t goals-node .

    Run Nodejs container:
    Docker run --name goals-backend --rm -p 80:80 goals-node

    Now nodejs should able to connect with Mongodb

4.  ----- Dockerizing Reactjs (Frontend) ----
    Build image
    Docker build -t goals-react .

    Run the docker reactjs container in interactive mode:
    Docker run --name goals-frontend --rm -p 3000:3000 -it goals-react

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
