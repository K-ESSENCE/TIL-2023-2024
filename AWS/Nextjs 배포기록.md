23/11/8

SSH(Secure SHell)란 원격으로 컴퓨터(서버)에 안전하게 접속하기 위해, 사용자와 서버가 사용하는 비밀 언어(프로토콜)

### 연결 과정

1. EC2 로 인스턴스 설정

우분투 or 아마존 리눅스

로그인을 위한 키페어 설정

인스턴스 연결에 ssh 명령어 친절히 적혀있음

2. 윈도우 Power shell 로 해당 인스턴스 연결 및 접속 시도
   2-1. 권한 deined
   1에서 설정했던 키페어 파일이 있는곳에서 시도했어야되는데 걍 키고 복붙한 결과로 뜸

   => C\ 로 파일 옮기고 실행 해결

   2-2 WARNING: UNPROTECTED PRIVATE KEY FILE!  
   SSH 의 키 파일이 너무 개방적이라 뜨는 에러
   안전하게 보호되지않았으면 연결을 거부함

   =>리눅스 운영체제 는 chmod 명령어이나 윈도우에서는 icals 사용

   icacls .\23-11-8Nextjs.pem /reset
   설정된 모든 액세스 권한을 리셋

   icacls .\23-11-8Nextjs.pem /inheritance:r
   상속된 권한을 제거하고, 오직 명시적으로 정의된 권한만 남깁니다.

   icacls .\23-11-8Nextjs.pem /grant:r "$($env:USERNAME):(R)
   $env:USERNAME은 현재 로그인된 사용자의 이름을 나타내고, :(R)은 해당 사용자에게 읽기(Read) 권한을 부여

   리눅스운영체제
   chmod 400 ~/.ssh/your-key.pem
   같은 방식으로 쉽게 변경 가능

3. Node js 및 Npm 설치

   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
   source ~/.bashrc
   nvm install 16

   node -v
   npm -v
   로 확인

### 연결 후 ?

그냥 mkdir 만들고 git clone으로 생성하고 npm i 하고 빌드 하면됨

은 아니고 빌드하고 나서 3000포트나 인바운드 아웃바운드 규칙에서 열어줘야됨 3000 포트도

### ACL?

네트워크 리소스에 대한 접근 권한을 관리하는 방법을 정의한 리스트
각 ACL에는 특정 사용자나 시스템 사용자 그룹에게 특정 파일이나 디렉터리, 객체 등에 대한 접근을 허용하거나 거부할 수 있는 권한을 정의하는 여러 규칙(항목)이 포함됨

### git authenticate fatal

개발자 세팅으로 가서 token 생성

참고로 난 클래식

생성하고 권한 줘야됨

그리고 비밀번호 git clone 시 물어보면 해당 토큰 번호 써야됨

잊어버렸으면 재발행. 안그러면 한번 보고 못봄
