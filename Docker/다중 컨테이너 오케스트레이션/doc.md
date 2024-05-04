### compose 파일

버전을 먼저 명명하는데 우리 앱의 버전이 아니라 compose의 버전을 명명한다.

그다음 services: 하고 네스팅 인덴팅으로 쓰게되는데

yaml에선 이 인덴팅이 굉장히 중요.

sevices에 들어가는 값은 무엇일까? => 바로 컨테이너

same level로 인덴팅 되어야됨

도커 컴포즈는 기본적으로 detach모드임 지정할필요없음

```

version: '3.8'
services:
  mongodb:
    image: 'mongo'
    volumes:
      - data:/data/db
    environment:
      - MONGO_INIT_ROOT_USERNAME=me
      - MONGO_INIT_ROOT_PASSWORD=secret
  backend:

  frontedn:

```

```
version: '3.8'
services:
  mongodb:
    image: 'mongo'
    volumes:
      - data:/data/db
    env_file:
      - ./env/mongo.env
  backend:

  frontedn:


```

이런식으로 가리키는것도 가능 후자가 더 세련된듯.

도커 컴포즈를 사용할떄는 네트워크 옵션을 이용할필요가없음. 자동으로 추가함

```

version: '3.8'
services:
  mongodb:
    image: 'mongo'
    volumes:
      - data:/data/db
    env_file:
      - ./env/mongo.env
    networks:
      - goals-net
  backend:

  frontedn:

```

다음과 같이 추가할려면 추가할 수도있긴함.

명명된 볼륨을 인식하기위해선 최상위에서 volumes를 다시한번 정의하는게 필요
그래야 사용가능 익명 볼륨은 지정할필요없다.

### up & down

docker-compose up -d detach mode
모든 서비스 중지 / 제거 => down

docker-compose down -v 하면 볼륨도 같이제거

up은 빌드를 위한거고 down은 중지를 위한것

### 백/프

도커 컴포즈에 이미지를 지정하는것말고도 이미지 빌드에 필요한 정보 제공도가능하다

```

version: '3.8'
services:
  mongodb:
    image: 'mongo'
    volumes:
      - data:/data/db
    env_file:
      - ./env/mongo.env
  backend:
    build: ./backend/
    # image: 'backend'
```

경로 지정하면 알아서 거기에서 Dockerfile을 찾음

도커파일을 dev환경등 분리해서 쓰는경우에는 context를 네스팅해서 적어서 더많은것들을 적을수도있음

도커 run 에서는 바인드 마운트를 쓸려면 절대경로가 필요했음.

근데 compose에선 상대경로 사용가능

```
version: '3.8'
services:
  mongodb:
    image: 'mongo'
    volumes:
      - data:/data/db
    env_file:
      - ./env/mongo.env
  backend:
    build: ./backend/
    ports:
      - '80:80'
    volumes:
      - logs:app/logs
      - ./backend:app

```

depends_on:

이건 docker run에는 없는거 왜냐면 단일 설정이라 그때는 필요가없음

어디에 의존하는가 에 대한 것을 설정할수있음 지금 현재로 mongodb에 의존

이걸 적어줌으로써 mongdb를 먼저 불러와야됨을 명시

```
version: '3.8'
services:
  mongodb:
    image: 'mongo'
    volumes:
      - data:/data/db
    env_file:
      - ./env/mongo.env
  backend:
    build: ./backend/
    ports:
      - '80:80'
    volumes:
      - logs:/app/logs
      - ./backend:/app
      - /app/node_modules
      # 마지막껀 익명 볼륨
    env_file:
      - ./env/backend.env
    depends_on:
      - mongodb

  # frontedn:
  #   build: ./frontedn
volumes:
  data:
  logs:


```

재미있네

```
version: '3.8'
services:
  mongodb:
    image: 'mongo'
    volumes:
      - data:/data/db
    env_file:
      - ./env/mongo.env
  backend:
    build: ./backend/
    ports:
      - '80:80'
    volumes:
      - logs:/app/logs
      - ./backend:/app
      - /app/node_modules
      # 마지막껀 익명 볼륨
    env_file:
      - ./env/backend.env
    depends_on:
      - mongodb

  frontedn:
    build: ./frontend
    ports:
      - '3000:3000'
    volumes:
      - ./frontend/src:app/src
    stdin_open: true
    tty: true
    # -it 옵션 stdin_open 과 tty 두개
volumes:
  data:
  logs:


```

### 추가 옵션

docker-compose up --build 하면 이미지 리빌드를 강제할수있다.
이걸안하면 빌드는 한번만함. => 기존 이미지를 재사용함
근데 난 이번에 강의에서 주는건 node 22버전이 호환이 안되가지고 강제로 버젼 할당하고 build 강제했음

이전처럼 자체 name을 주려면 container_name 옵션을 사용하면됨
