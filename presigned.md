
https://medium.com/geekculture/how-to-upload-file-to-aws-s3-using-pre-signed-url-in-nextjs-1f70a955389e            

## Presigned URL


https://www.youtube.com/watch?v=f9LZWCSgojE

참조하여 
원래는 게이트웨이 통해서 람다로 업로드할려고했는데 용량 제한이 구현 10 mb 에 부합하지도않고 하여 
presigned url 방식을 사용하기로했다.
설정도 복잡하고 디버깅도 어렵다고 함 

게이트웨이 로 직접하는건 멀티파트도 안되고 권한 조절도어렵다. 

sdk 활용해서 임시 크레덴셜 활용하는 부분도 있었으나 권한관리가까다로울수있다함 
클라에서 업로드 다운로드 말고도 다양하게 하고싶으면 이렇게하라고함.


클라우드 프론트 활용하는건 추천하는 방법이지만 멀티파트가안됨.



### 흐름 
`
클라에서 파일 메타 데이터 생성해서 람다 ㄱ 
람다로 url 생성 하고 멀티파트쓸거면 멀티파트 url 

메타데이터를 쓰는이유? => 원래는 rds에 정보를 저장하고 해야되는데 메타 데이터를 넣으면 한방에해결

머신러닝같은거 할때도 목적 명시로 한방 컷


