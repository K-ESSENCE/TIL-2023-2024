# 구성

- app container
  Nginx Web Server
  PHP interpreter
  MySQL db

- utility container
  composer (npm으로 치면 node 같은거 써드파티 패키지 설치해서 관리함)
  lalavel Artison(db초기화 및 mig용)
  npm(프론트 로직 일부에서 js코드가 필요)

## nginx

version: '3.8'

services:
server:
image: 'nginx:stable-alpine' // quote로 묶어두는게 다른 방식으로 해석되지않도록해서 안전함
ports: - '8000:80' // 8000포트를 80에 바인드
volumes: - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro // bind로 자체 구성 전달

=>

server:
image: 'nginx:stable-alpine'
ports: - '8000:80' # 외부:내부
volumes: - ./src:/var/www/html - ./nginx/nginx.conf:/etc/nginx/conf.d/default.conf:ro

## php

php:
build:
context: ./dockerfiles
dockerfile: php.dockerfile
volumes: - ./src:/var/www/html:delegated # delegated 성능향상 => 호스트머신에 바로 반영하는게 아니라 배치로 처리 안정성은 떨어지나 속도는빨라진다. # 공식문서가보면 9000노출 하지만 할필요없음 nginx 가서 9000으로 변경

## mysql

mysql:
image: 'mysql:5.7'
env_file: - ./env/mysql.env

## composer

composer:
build:
context: ./dockerfiles
dockerfile: composer.dockerfile
volumes: - ./src:/var/www/html

유틸리티 컨테이너는 compose 에서 만들어도 단일로 실행하는게 일반적이라고함

docker-compose run --rm composer

laravel env 파일에 가서 db_host를 mysql 로 변경 이건 참고로 같은 네트워크에서 실행될때 컨테이너이름을 사용하면 알아서 인식하는 원리활용

### 일부만 실행하기

docker-compose up [service...]

docker-compose up server php mysql 이런식으로 선택적 실행가능

일일이 컨테이너 이름 설정 귀찮다 => depends_on 활용해서 php mysql 추가하면 얘만 실행시켜도 나머지 on

마지막으로 --build 로 변경사항 있으면 리빌드시키기

배운거 총망라네

## 남은 애들 유틸리티 컨테이너

### artisan

초기데이터로 데이터베이스 체우는데 쓴다고함

dockerfile에 entrypoint없으면 추가 하거나 override가능

다른애들도 마찬가지 working_dir 등
artisan:
build:
context: ./dockerfiles
dockerfile: php.dockerfile
volumes: - ./src:/var/www/html
entrypoint: ['php', '/var/www/html/artisan']
npm:
image: node:14
working_dir: /var/www/html
entrypoint: ['npm']
volumes: - ./src:/var/www/html

강사는 이런 방식보다 dockerfile 따로 만들어서 가리키게하는것을 더 좋아한다고함.

그리고 어짜피 복잡한 명령어가 필요하면 그떄는 dockerfile이 필요할거라고
docker-compose 에서는 copy나 run 명령어를 못쓰기떄문 ㅇ

바인드 마운트에대한 염두사항 => 개발에 큰 도움이 되지만 컨테이너를 배포할거라면 이건 선택사항이아님
개발 편하게 하는거지 이거 배포할떄쓰는거 ㄴ

### 바인드 마운트와 copy

nginx 구성을 dockerfile에 변경해봄

FROM nginx:stable-alpine

WORKDIR /etc/nginx/conf.d

COPY nginx/nginx.conf .

RUN mv nginx.conf default.conf

// 이름이 안맞음으로 실행 후 변경 동일한 파일을 동일한 폴더로 이동시키면 이름만 변경

WORKDIR /var/www/html

COPY src .

이 상태에서 compose 파일에서 build를 평상시 하던대로 context와 dockerfile로 연결하게되면

이미지는 빌드가 실패함 => 설정해둔 COPY의 폴더에 접근이 불가능함. 경로가달라서

그래서 context의 위치를 그냥 dot (.) 으로 해둠으로써 yaml파일과 같은 위치를 가리킴

      context: .
      dockerfile: dockerfiles/nginx.dockerfile

이런식

COPY가 있는애들은 이부분을 유의할것

바인드 마운트가없으면 소스코드의 변경 사항이 반영되지않음. 위처럼 COPY로 바꾸면 그렇다.

권한문제가 생길수있으면 RUN chown ㅇ
