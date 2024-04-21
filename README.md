# docker-day2

# ITI - Docker Lab Two🐋
## Task 1: Run a container using nginx image, and mount a directory from your host into the Docker container.
example: /home/samy/nginx:/home/nginx (bind mount)

### Steps
#### 1. Create Bind Mount Directory
```bash
mkdir nginx_bindMount
cd nginx_bindMount
pwd
```
![image](https://github.com/mennazm/docker-day2/assets/91394925/aff6f6c6-7fde-4277-8428-dbe0ea92213a)

#### 2. Run a container using nginx image
```bash
docker run -d --name nginx_bindMount -v /root/nginx_bindMount:/user/share/nginx/html nginx
docker exec -it nginx_bindMount bash
```
![image](https://github.com/mennazm/docker-day2/assets/91394925/b19c326c-c338-4af4-a07d-a240e77b7151)


#### 3. Echo any content to show when curl ip-address
```bash
cd /user/share/nginx/html
echo "Hello world " > index.html
exit
docker inspect -f '{{.NetworkSettings.IPAddress}}' nginx_bindMount    ->172.17.0.3
curl 172.17.0.3
```

---
## Task 2: Create 2 docker network (net-1 & net-2)

### Steps
#### 1. Create 2 docker network (net-1 & net-2)
```bash
docker network create network1
docker network create network2
```
![image](https://github.com/mennazm/docker-day2/assets/91394925/51e7aed5-629a-44dd-bc15-c5041152a62c)


#### 2. Run 2 new containers using nginx:alpine image, and attach the net-1 to them.
```bash
docker run -d --name nginx_net1 --net network1 nginx:alpine
docker run -d --name nginx_net2 --net network1 nginx:alpine
```
![image](https://github.com/mennazm/docker-day2/assets/91394925/22c74b31-0642-41db-9859-7db4ba2a839b)

#### 3. Run another 1 new containers using nginx:alpine image, and attach the net-2 to them.
```bash
docker run -d --name nginx_net3 --net network_2 nginx:alpine
```

#### 4. Inspect the 3 containers to know their IPs and write them aside.
```bash
 docker inspect -f '{{.NetworkSettings.Networks.network1.IPAddress}}' nginx_net2
172.18.0.3

 docker inspect -f '{{.NetworkSettings.Networks.network1.IPAddress}}' nginx_net1
172.18.0.2 ```
![image](https://github.com/mennazm/docker-day2/assets/91394925/23b2b878-0a0b-4fb9-b6bf-a591bd5b4e8e)
