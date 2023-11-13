### CloudFront

Content Delivery Network

컨텐츠가 전체적으로 분산되어 있으므로 DDos 공격에서 보호를 받을 수 있다.

DDos=> 서버 동시 공격

S3 버킷으로 클라우드 프론트를 통해 파일을 분산하고 캐싱할 수 있게 한다.

버킷에 CloudFront만 접근하게 하는게 => OAC origin access control

CF 를 통해 버킷에 데이터를 보내는 방법 도 가능하다. 이를 Ingress라고 함

Coustom Origin => 로드밸런서 ,EC2 ,S3 등 그밖에 http 백엔드 는 전부 가능

클라이언트가 엣지 로케이션에 연결되고

엣지는 캐싱되어있는지 확인 함 => 캐싱 안되면 요청결과 가져옴

그리고 로컬에 캐시 저장 해서 같은 거 요청하면 캐시한거 갖다씀

OAC로 접근이 막혀있기떄문에 보호된다.

CF와 CRR의 차이

CF는 전세계 네트워크 사용

CRR => s3 교차 리전 복제는 => 전세계 대상이 아님 거의 실시간으로 되고
캐싱은 안되고 읽기전용

일부 리전 대상으로 동적 컨텐츠를 낮은 지연시간으로 제공하고자 할때 좋음

### 퍼블릭으로 안만들고 S3 CF 로 접근하는법

origin domain 설정

origin access 음 여기에 oac 있네

oai 는 레거시 옛날방식

access control 가서 제어설정 생성하면 버킷 정책을 업데이트 해야된다는 말이 뜸
