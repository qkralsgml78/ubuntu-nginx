## docker 로 ubuntu IMG 를 받아서 NGINX 설치하기

### 1. REPO 에 ubuntu-nginx 를 생성
```
$ mkdir ubuntu-nginx
$ cd ubuntu-nginx
```

이미지1

```
$ git init

$ git vi README.md

$ git add .

$ git commit -m [깃 commit 메세지]

$ git push

```
### 2. hub 에서 ubuntu pull & run
```
$ sudo docker pull ubuntu:22.04

$ sudo docker run -itd --name ubuntu -p 9051:80 ubuntu:22.04

$ sudo docker ps
CONTAINER ID   IMAGE          COMMAND       CREATED         STATUS         PORTS                                   NAMES
122399bffcc9   ubuntu:22.04   "/bin/bash"   5 seconds ago   Up 3 seconds   0.0.0.0:9051->80/tcp, :::9051->80/tcp   ubuntu
```

### 3. (2) 에 들어가서 nginx.org 참조하여 nginx 설치
```
$ sudo docker exec -it ubuntu bash
root@122399bffcc9:/# apt update
root@122399bffcc9:/# apt install nginx
root@122399bffcc9:/# exit
```

