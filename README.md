# docker 로 ubuntu IMG 를 받아서 NGINX 설치하기

### 1. REPO 에 ubuntu-nginx 를 생성
```
$ mkdir ubuntu-nginx
$ cd ubuntu-nginx
```
![스크린샷 2024-02-18 012107](https://github.com/qkralsgml78/ubuntu-nginx/assets/149050285/c5c0a5c3-7bfc-4e44-90ea-5006697ce0f9)


#### - git
```
$ git init

$ git vi README.md
```
![스크린샷 2024-02-18 012700](https://github.com/qkralsgml78/ubuntu-nginx/assets/149050285/af8419db-7d05-4af4-93a3-5a159cab1959)
```
$ git add .

$ git commit -m [깃 commit 메세지]
```
![스크린샷 2024-02-18 012715](https://github.com/qkralsgml78/ubuntu-nginx/assets/149050285/b27278cd-f336-4388-a784-bc000dc11a6a)

```
$ git push
```
![스크린샷 2024-02-18 012744](https://github.com/qkralsgml78/ubuntu-nginx/assets/149050285/7d2a9d0c-8562-4369-a034-9b17473bcf7e)
![스크린샷 2024-02-18 012836](https://github.com/qkralsgml78/ubuntu-nginx/assets/149050285/41dbd67e-fccf-4d36-a02c-df7bd9c64130)




### 2. hub 에서 ubuntu pull & run
```
$ sudo docker pull ubuntu:22.04
```
![image](https://github.com/qkralsgml78/ubuntu-nginx/assets/149050285/138745f7-924a-408e-be55-1ff134e6a14c)

```
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

