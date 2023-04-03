docker pull hello-world
docker run hello-world
docker ps -a
docker container rm <container_id>
docker build . -t myimage:v1
docker images
docker run -dp 8080:8080 myimage:v1
curl localhost:8080
docker stop $(docker ps -q)
docker ps