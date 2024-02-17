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

### 4. 기록을 바탕으로 Dockerfile 생성
```
$ vi Dockerfile
```
![image](https://github.com/qkralsgml78/ubuntu-nginx/assets/149050285/41336938-4f0e-4bd3-805f-c1e5d0ec0e9d)
![스크린샷 2024-02-18 020002](https://github.com/qkralsgml78/ubuntu-nginx/assets/149050285/9c58f37a-a37e-4899-881b-23ed719c6eb4)

### error 발생
```
1. y를 중간에 넣어주지 않은 문제
- y란 install할 때 자동으로 yes해주겠다는 것

2. cmd창을 자동으로 생성해주는 코드를 넣어주지 않은 문제
```
![스크린샷 2024-02-18 021103](https://github.com/qkralsgml78/ubuntu-nginx/assets/149050285/8b3ea568-eb6d-4846-b63e-12d11b9e8f81)

### 수정 & 해결
```
FROM ubuntu:22.04
RUN apt update;apt install -y nginx
CMD ["nginx", "-g", "daemon off;"]
```

![스크린샷 2024-02-18 021011](https://github.com/qkralsgml78/ubuntu-nginx/assets/149050285/441d8355-a3bd-4c45-8a3b-a4fb4d860838)

![스크린샷 2024-02-18 021029](https://github.com/qkralsgml78/ubuntu-nginx/assets/149050285/050794f5-ca40-4b05-83b9-6eee9638fc0d)

### Build & Run
```
$ sudo docker run -itd --name D-ubuntu -p 9053:80 ubuntu
$ sudo docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                                   NAMES
448db98f2477   ubuntu         "nginx -g 'daemon of…"   5 seconds ago   Up 4 seconds   0.0.0.0:9053->80/tcp, :::9053->80/tcp   D-ubuntu
122399bffcc9   3db8720ecbf5   "/bin/bash"              2 hours ago     Up 2 hours     0.0.0.0:9051->80/tcp, :::9051->80/tcp   ubuntu
```
![image](https://github.com/qkralsgml78/ubuntu-nginx/assets/149050285/6142004b-d591-48f0-9158-230d294b10bd)
- itd를 넣어줌으로써 run하고 start를 따로 해줘야 하지만 하지 않아도 바로 컨테이너를 확인하면 실행이 되어 있는 것을 확인할 수 있다.
  

### 컨테이너 확인

![image](https://github.com/qkralsgml78/ubuntu-nginx/assets/149050285/4b3ae619-2e2d-4106-8ebd-0e2f257fe703)
