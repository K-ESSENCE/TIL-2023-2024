이전 까지 알고있던 내용 + 복습

도메인 등록하는 시스템이다.

근데 왜 호스팅 영역은 있는데 등록된 도메인은없지 강의 상으로는 도메인을 등록해야지 호스팅 영역이 생기는데

### DNS

dns 에는 계층이있다

도메인 레지스트라 : 아마존 라우트 53 , 고대디 등등

DNS Records: A,AAAA,CNAME ,NS 등이 있다

Zone file : 모든 dns 레코드를 포함

Name Server : Dns 쿼리를 실제로 해결하는 서버

TLD: top level domain : .com / .us /.in /.gob 등등

SLD: second level domain : amazon.com / google.com

FQDN : 풀 도메인 네임 걍전체 ㅇ

.com이 최상위

example.com 이 SLD

www.example.com 이 서브 도메인

api.www.example.com 이 도메인 네임

http는 프로토콜

전체는 FQDN

DNS의 동작

웹 서버가있음, 도메인 이름을 이용해서 접근하고자 한다면, 접근하고자 하는 이름을 dns용 서버에 등록해야됨

어떻게 접근하고 받는가? => 로컬 dns 서버에 물어봄 (로컬 dns 서버는 보통 회사에 의해 할당되고 관리됨 아니면 isp 에 의해 동적으로 할당)

모른다고하면 루트 dns 로

하지만 .com 은 안다 라고 하면 TLD DNS Server에 또 요청

마지막으로 서브도메인의 dns 서버에 요청함 아마존 route 53등등이 여기에 해당됨

레코드가 뭐고 ip 가 뭔지 알려줌

그럼 이제 dns 서버는 답을 알게됨 캐시해서 알려줌

### Route 53 -records

레코드를 통해 특정 도메인으로 라우팅 하는 방법을 정함

TTL 은 DNS 리졸버에서 레코드가 캐싱되는 시간 타임투리브라고도함

반드시 알아야 될건 A AAAA CNAME NS

NS 는 호스팅 존의 네임서버

호스팅존에 대한 DNS 쿼리에 응답할 수있음, 트래픽이 도메인으로 라우팅 되는 방식을 제어함

### 호스팅 존

레코드의 컨테이너임 도메인과 서브도메인으로 가는 트래픽의 라우팅 방식을 정의함

퍼블릭, 프라이빗 호스팅 존이 있음

퍼블릭 도메인 이름을 살 때마다 퍼블릭 호스팅 존을 만들 수 있음

퍼블릭 존은 쿼리에 도메인 이름의 IP가 뭔지 물어볼 수 있음

프라이빗 호스팅 존 이 있는데 공개되지 않는 도메인이름을 지원함

VPC만이 URL을 리졸브 할 수 있음 (사내 에서만 접근할 수 있는 URL)

퍼블릭 호스팅 존은 공개된 클라이언트로부터 온 쿼리에 응답가능

프라이빗의 경우 해당 vpc에서만 동작함 비공개 도메인 이름의 프라이빗 리소스를 식별할 수 있게 함

### 레코드 타입/ 생성

A레코드 도메인 네임을 ipv4로 연결하는거

AAAA는 ipv6랑 연결

CNAME 은 호스트이름을 다른 호스트 이름과 맵핑함

value 실제 기관의 인스턴스로 설정

값으로 cloudFront 넣으면 걸로

윈도우 nslookup 맥 dig

dig 없으면 sudo yum install -y bind-utils 깔아야됨

=> nslookup 과 dig 까는거

nslookup test.~.com

name 이랑 address 나오네 address 가 value

dig url

동일

나오는 정보 결과가 좀더 상세함 응답 , 레코드 A 도 나오네 레코드값이랑 TTL도 보여줌
