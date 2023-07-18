### Docker images and container setup.

- To create mongo container : `docker run -d --name mongodb --rm -p 27010:27010  mongo`

- To create backend node image : `docker build -t goals-api  .`

- To create backend container : `docker run -p 80:80 --rm --name goals-backend goals-api`

- To create ui image: `docker build -t goals-ui .`

- To create ui container: `docker run --rm -d -p 3000:3000 -it --name goals-frontend  goals-ui`

### To get all 2 apps to interact with each other we should create a docker network

- To create network `docker network  create goals-network`

now restart all the containers by attaching to this network

- mongo `docker run -d --name mongodb --rm -d --network goals-network  mongo`

- backend `docker run --network goals-network -p 80:80  --rm --name goals-backend goals-api`

- frontend : `no need to add network bcs the ui code runs in browser and not in docker`

### To start compose ( launch configs for docker containers ).

- start `docker-compose up` to start in detached mode add `-d`

- to stop all containers and network `docker-compose down` to delete volumes too use `-v` bcs bydefault the volumes are not deleted.

to force images to rebuild on we need to run add `docker-compose -build` command.
