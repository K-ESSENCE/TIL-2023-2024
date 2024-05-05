## 유틸리티 컨테이너

특정 환경만 포함하는 컨테이너를 의미함 => nodejs환경이나 php환경같은.

앱을 실행하는 기존방식이 아닌. 환경을쓰는개념

### 왜쓰는가

호스트 머신에 툴을 전역적으로 설치안하고
앱에 필요한 환경이 포함된 컨테이너 사용하는게 도커의 개념
그러나 노듸의 경우 npm init 을 할려면 node를 깔아야됨
노드뿐만아니라 대부분 프로젝트를 생성하기위에 호스트머신에 부가적인 툴이 필요하다.

### 컨테이너에서 명령실행방법

docker exec => 실행중인 컨테이너 내에서 명령 실행가능

dockerfile에 지정된 명령외에 추가적인 명령 실행 가능

docker exec 역시 -it 모드로 실행 해야 입력 가능

docker exec -it container npm init 이런 느낌

docker run -it node npm init 으로 override도 가능.

유틸리티를 만들려면 자체 이미지가필요 => dockerfile

alpine => 슬림 버전

호스트머신에 깔지않고도 호스트머신에 영향을 미치도록 하는개념

### entry point

CMD와 유사하지만 run 하고 뒤에있는 명령어가있으면 CMD는 override되지만
ENTRYPOINT는 뒤에 추가됨

### docker-compose 로 구성하기

그동안 했던 구성 재사용하면되는데

docker compose up 이 아닌 다른 명령어

docker-compose run (싱글서비스) npm(서비스이름) init

docker-compose run 에는 up/down 개념이없기때문에 --rm 달아주면 알아서 소멸
