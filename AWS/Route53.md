이전 까지 알고있던 내용

도메인 등록하는 시스템이다.

근데 왜 호스팅 영역은 있는데 등록된 도메인은없지 강의 상으로는 도메인을 등록해야지 호스팅 영역이 생기는데

### 레코드 생성

A레코드 도메인 네임을 ipv4로 연결하는거

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
