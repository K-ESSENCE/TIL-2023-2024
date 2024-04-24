### mongodb

27017:27017 포트 노출
네트워크때 했던 host.docker.internal
둘 다 잊지말것

환경변수

-e MONGO_INITDB_ROOT_USERNAME=
-e MONGO_INITDB_ROOT_PASSWORD=

이걸넣으면 데이터베이스가 보호되고있어서 node에서 파일수정해야됨

mongodb://user:pw@mongodb:27017

### node

는 별로 다를거없음

### fe

run 시 -it옵션을 넣어줘야됨

알다시피 내부 포트 3000 맵핑

리액트코드는 컨테이너 내부에서가 아니라 브라우저에서 실행됨 그의미는 브라우저에서 실행되기떄문에

브라우저는 우리가 바꾼 컨테이너이름을 모름

브라우저가 인식하는 식별자를 넣어줘야됨

localhost

프론트엔드에서는 --network 옵션 할필요없음 의미없음 이경우에는

### 네트워크

효율적인 컨테이너간 통신을 위해 생성

프론트엔드의 localhost도 전부 컨테이너 이름으로 변경
