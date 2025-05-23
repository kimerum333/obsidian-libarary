# 기본 설치 명령어즈

```
sudo apt install mysql-server

sudo apt install mysql-client-core-8.0

systemctl status mysql
```

# 초기화 프로세스


1. DB를 만들고
2. 사용자를 만들고
3. 사용자에게 해당 DB접속 권한을 준다.

```
CREATE DATABASE spc1234;
CREATE USER 'user1'@'%' IDENTIFIED BY 'password1234';
GRANT ALL PRIVILEGES ON spc1234.* TO 'user1'@'%';
FLUSH PRIVILEGES
```

sudo apt install python3 python3-pip

# 미니콘다
- 아나콘다의 가상환경만 들고오는 버전. 유용함.

```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```