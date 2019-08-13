# k8s

## 기본설치 및 환경설정

1. Lightsail 생성

2. 방화벽설정

3. shell 주소
http://54.180.141.143:4200/
ubuntu / 1q2w3e4r

4. shell 접속 후 jq  설치
 ```
 sudo apt install -y jq
 ```
 - doc
 
 5. docker 설치

docker & docker-compose 설치

```sh
curl -fsSL https://get.docker.com/ | sudo sh
sudo usermod -aG docker $USER

sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# check (re-login)
docker version
docker-compose version

# reboot
sudo reboot
```


 
 
