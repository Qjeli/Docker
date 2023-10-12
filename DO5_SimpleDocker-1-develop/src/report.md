## Part 1. Ready-made docker

* Take the official docker image from nginx and download it using docker pull.

<img src="../src/pics/1/1.1.png" alt="1" width="500"/>

* Check for the docker image with `docker images`

<img src="../src/pics/1/1.2.png" alt="1" width="500"/>

* Run docker image with `docker run -d [image_id|repository]`

<img src="../src/pics/1/1.3.png" alt="1" width="500"/>

* Check that the image is running with `docker ps`

<img src="../src/pics/1/1.4.png" alt="1" width="500"/>

* View container information with `docker inspect [container_id|container_name]`

<img src="../src/pics/1/1.5.png" alt="1" width="500"/>

* From the command output define and write in the report the container size, list of mapped ports and container ip

List of mapped ports and IP adress can be found at the very botom of the inspect list

<img src="../src/pics/1/1.6.png" alt="1" width="500"/>

To ease my burdens i used `grep` command to find the container size

<img src="../src/pics/1/1.7.png" alt="1" width="500"/>

* Stop docker image with `docker stop [container_id|container_name]`

<img src="../src/pics/1/1.8.png" alt="1" width="500"/>

* Check that the image has stopped with `docker ps`

<img src="../src/pics/1/1.9.png" alt="1" width="500"/>

* Run docker with mapped ports 80 and 443 on the local machine with `run` command

to do this we need to run the `docker run -d -p 127.0.0.1:80:80 -p 127.0.0.1:443:443 nginx` command

<img src="../src/pics/1/1.10.png" alt="1" width="500"/>

* Check that the nginx start page is available in the browser at localhost:80

<img src="../src/pics/1/1.11.png" alt="1" width="500"/>

* Restart docker container with `docker restart [container_id|container_name]`

* Check in any way that the container is running

<img src="../src/pics/1/1.12.png" alt="1" width="500"/>

## Part 2. Operations with container

* Read the nginx.conf configuration file inside the docker container with the `exec` command

<img src="../src/pics/2/2.1.png" alt="1" width="500"/>

* Create a nginx.conf file on a local machine

* Configure it on the /status path to return the nginx server status page

<img src="../src/pics/2/2.2.png" alt="1" width="500"/>

* Copy the created nginx.conf file inside the docker image using the `docker cp nginx.conf ddacc6f9fa28:/etc/nginx/conf.d/default.conf` command

<img src="../src/pics/2/2.3.png" alt="1" width="500"/>

* Restart nginx inside the docker image with `docker exec ddacc6f9fa28 nginx -s reload`

<img src="../src/pics/2/2.4.png" alt="1" width="500"/>

* Check that localhost:80/status returns the nginx server status page

<img src="../src/pics/2/2.5.png" alt="1" width="500"/>

* Export the container to a container.tar file with the export command

<img src="../src/pics/2/2.6.png" alt="1" width="500"/>

* Export the container to a container.tar file with the `docker export -o container.tar ddacc6f9fa28` command

<img src="../src/pics/2/2.7.png" alt="1" width="500"/>

* Stop the container using `docker stop ddacc6f9fa28`

<img src="../src/pics/2/2.8.png" alt="1" width="500"/>

* Delete the image with `docker rmi nginx -f` without removing the container first

<img src="../src/pics/2/2.8.png" alt="1" width="500"/>

* Delete stopped container using `docker container rm ddacc6f9fa28`

<img src="../src/pics/2/2.9.png" alt="1" width="500"/>

* Import the container back using the `docker import container.tar nginx` command

<img src="../src/pics/2/2.10.png" alt="1" width="500"/>

* Run the imported container with `docker run -d -p 80:80 -p 443:443 -it nginx bash` command

<img src="../src/pics/2/2.11.png" alt="1" width="500"/>

* Check that localhost:80/status returns the nginx server status page

First we start a server using `exec`

<img src="../src/pics/2/2.12.png" alt="1" width="500"/>

<img src="../src/pics/2/2.13.png" alt="1" width="500"/>

## Part 3. Mini web server

* Wrote a mini server in C and FastCgi that will return a simple page saying Hello World!

<img src="../src/pics/3/3.1.png" alt="1" width="500"/>

* Updated the packages in the container and loaded the fcgi library

<img src="../src/pics/3/3.2.png" alt="1" width="500"/>

* Changed the nginx.conf file

<img src="../src/pics/3/3.3.png" alt="1" width="500"/>

* Launched the written mini server via spawn-fcgi on port 8080

<img src="../src/pics/3/3.3.png" alt="1" width="500"/>

<img src="../src/pics/3/3.4.png" alt="1" width="500"/>

* check with `curl` that everything was done right and also check in localhost

<img src="../src/pics/3/3.5.png" alt="1" width="500"/>

## Part 4. Your own docker

* Build the written docker image with docker build, specifying the name and tag

<img src="../src/pics/4/4.1.png" alt="1" width="500"/>

* Check with docker images that everything is built correctly

<img src="../src/pics/4/4.2.png" alt="1" width="500"/>

* Run the built docker image by mapping port 81 to 80 on the local machine and mapping the ./nginx folder inside the container to the address where the nginx configuration files are located (see Part 2)

<img src="../src/pics/4/4.3.png" alt="1" width="500"/>

* Check that the page of the written mini server is available on localhost:80

<img src="../src/pics/4/4.4.png" alt="1" width="500"/>

* Restart docker image

<img src="../src/pics/4/4.5.png" alt="1" width="500"/>

* Check that localhost:80/status now returns a page with nginx status

<img src="../src/pics/4/4.6.png" alt="1" width="500"/>

## Part 5. Dockle

* Install dockle via brew.

<img src="../src/pics/5/5.1.png" alt="1" width="500"/>

* Install dockle via brew.

<img src="../src/pics/5/5.1.png" alt="1" width="500"/>

* Check the image from the previous task with `dockle hello_world:1.0`

<img src="../src/pics/5/5.2.png" alt="1" width="500"/>

* Fix the image so that there are no errors or warnings when checking with dockle

<img src="../src/pics/5/5.3.png" alt="1" width="500"/>

## Part 6. Basic Docker Compose

* Map port 8080 of the second container to port 80 of the local machine

* Start the docker container from Part 5 (it must work on local network, i.e., you don't need to use EXPOSE instruction and map ports to local machine)

* Start the docker container with nginx which will proxy all requests from port 8080 to port 81 of the first container

<img src="../src/pics/6/6.1.png" alt="1" width="500"/>

* `docker-compose up` command

<img src="../src/pics/6/6.2.png" alt="1" width="500"/>

Checking a localhost and localhost/status

<img src="../src/pics/6/6.3.png" alt="1" width="500"/>
<img src="../src/pics/6/6.4.png" alt="1" width="500"/>


