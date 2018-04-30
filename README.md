# compose-postgrest
Forked from [compose-postgrest](https://github.com/mattddowney/compose-postgrest), adding docker-machine and NGINX.

## Stack
* [NGINX](https://github.com/nginxinc/docker-nginx): Webserver.
* [Postgres](https://www.postgresql.org/): Database Engine.
* [PostgREST](https://github.com/begriffs/postgrest): API Server.
* [Swagger UI](https://github.com/swagger-api/swagger-ui): API Spec Exploration & Test Interface.
* [docker-compose](https://github.com/docker/compose)/[Docker](https://github.com/docker): Containerization.
* [docker-machine](https://docs.docker.com/machine/): Virtual Machine for local development.
* [docker-machine-ipconfig](https://github.com/fivestars/docker-machine-ipconfig): Enables static IP addresses for docker-machine VMs.

## Local Development Installation Instructions
**NOTE:** Before you start, you'll need the following installed on your local machine: 
1. Docker
2. docker-compose
3. docker-machine
4. docker-machine-ipconfig

The quickest/easiest way to get the first three is by installing [Docker Toolbox](https://docs.docker.com/docker-for-mac/docker-toolbox/). For `docker-machine-ipconfig` see [its associated repo](https://github.com/fivestars/docker-machine-ipconfig).

Start by cloning this repo to your local machine:

```bash
$ git clone git@github.com:respondcreate/compose-postgrest.git
```

Next, create a docker-machine instance to run this project within:

```bash
$ docker-machine create -d virtualbox compose-postgrest
```

Now, assign a static IP address (`192.168.99.116`) to the instance you just created:

```bash
$ docker-machine-ipconfig static compose-postgrest 192.168.99.116
```

Next, add this VM's environment variables to your current shell session:

```bash
$ eval "$(docker-machine env compose-postgrest)"
```

Finally, build the docker-compose pod:

```bash
$ docker-compose up -d --build
```

Once that completes visit [http://192.168.99.116/swagger](http://192.168.99.116/swagger) in your browser!

### Other helpful commands
Spinning down your docker-compose pod:

```bash
$ docker-compose down
```

## Adding Additional SQL
Out of the box, this project provides the [world sample database](http://pgfoundry.org/projects/dbsamples/). To add additional SQL just include it in the `initdb` folder.
