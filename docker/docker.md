# Docker

## 도커 기본

### 기본 명령어

| 명령어  |  설명  |
|---|---|
| run | 컨테이너 실행하기 |
| ps | 컨테이너 목록 확인하기 |
| stop | 컨테이너 중지하기 |
| rm | 컨테이너 제거하기 |
| logs | 컨테이너 로그보기 |
| images | 이미지 목록 확인하기 |
| pull | 이미지 다운로드하기 |
| rmi | 이미지 삭제하기 |

### 컨테이너 생성

**ubuntu 컨테이너 생성**

```
docker run --rm -it ubuntu:18.04 /bin/sh
```

**간단한 웹 애플리케이션 생성**

```
docker run -d -p 4567:4567 subicura/docker-workshop-app:1
```

http://xxxx:4567 접속

**MySQL 생성**

```
docker run -d -p 3306:3306 \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
  --name mysql \
  mysql:5.7
```

Database 생성

```
docker exec -it mysql mysql
create database wp CHARACTER SET utf8;
grant all privileges on wp.* to wp@'%' identified by 'wp';
flush privileges;
quit
```

**Wordpress 생성**

```
docker run -d -p 8000:80 \
  -e WORDPRESS_DB_HOST=172.17.0.1 \
  -e WORDPRESS_DB_NAME=wp \
  -e WORDPRESS_DB_USER=wp \
  -e WORDPRESS_DB_PASSWORD=wp \
  wordpress
```

http://xxxx:8000 접속

**컨테이너 목록 확인**

```
docker ps -a
```

**컨테이너 로그**

```
docker logs xxx
```

**컨테이너 종료**

```
docker stop xxx
```

**컨테이너 삭제**

```
docker rm xxx
```

**이미지 목록 확인**

```
docker images
```

**네트워크 생성**

```
docker network create app-network
```

**네트워크에 연결된 컨테이너 생성**

```
docker run -d \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
  --name mysql \
  --network=app-network \
  mysql:5.7
```

```
docker exec -it mysql mysql
create database wp CHARACTER SET utf8;
grant all privileges on wp.* to wp@'%' identified by 'wp';
flush privileges;
quit
```

```
docker run -d -p 8000:80 \
  --network=app-network \
  -e WORDPRESS_DB_HOST=mysql \
  -e WORDPRESS_DB_NAME=wp \
  -e WORDPRESS_DB_USER=wp \
  -e WORDPRESS_DB_PASSWORD=wp \
  wordpress
```

## Exam 1. 방명록 만들기




**frontend**

이미지
- subicura/guestbook-frontend:latest

환경변수
- PORT # ex) 8000
- GUESTBOOK_API_ADDR # ex) APISERVER:8000

**backend**

이미지
- subicura/guestbook-backend:latest

환경변수
- PORT # ex) 8000
- GUESTBOOK_DB_ADDR # ex) DB:27017

**mongodb**

이미지
- mongo:4

기본포트
- 27017

## 정리

```
docker stop xxx
docker rm xxx
docker system prune -a
```


```
ubuntu@ip-172-26-12-66:~$ docker ps
CONTAINER ID        IMAGE                                COMMAND                  CREATED             STATUS              PORTS                    NAMES
313663514e81        subicura/guestbook-frontend:latest   "node --inspect=9229…"   About an hour ago   Up About an hour    0.0.0.0:3000->8000/tcp   strange_bouman
f20e677ff9e0        subicura/guestbook-backend:latest    "node --inspect=9229…"   About an hour ago   Up About an hour                             backend
016b1491914f        mongo:4                              "docker-entrypoint.s…"   About an hour ago   Up About an hour    27017/tcp                mongodb
ubuntu@ip-172-26-12-66:~$ 
ubuntu@ip-172-26-12-66:~$ 
ubuntu@ip-172-26-12-66:~$ docker stop 31 f2 01
31
f2
01
ubuntu@ip-172-26-12-66:~$ 
ubuntu@ip-172-26-12-66:~$ 
ubuntu@ip-172-26-12-66:~$ docker rm 31 f2 01
31
f2
01
ubuntu@ip-172-26-12-66:~$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

```
