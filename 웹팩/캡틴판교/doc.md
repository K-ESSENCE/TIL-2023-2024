### 모듈 번들링이란

파일을 하나로 압축해주는 동작을 모듈 번들링 이라고함

빌드 번딜링 변환 모두 같은 의미

mode ? => 기본적으로 development / production / none 세가지가 존재

    "build": "webpack --mode=none --entry=src/index.js --output=public/output.js"

이런식으로하는거보다 웹팩설정파일을쓰는게좋음

module.export = {
mode: 'none',
entry: './src/index.js',
output: './public/output.js',
};

node / path / resolve => 경로 잡아주는
console.log(path.resolve('user', 'data', 'file.txt')); // /현재경로/user/data/file.txt
\_\_dirname은 Node.js에서 사용되는 전역 변수 //파일 시스템에서의 절대 경로

### 웹팩 전후

웹팩전과 후 리퀘스트 횟수가 다름

라이브러리가 20개다 그러면 서버에 왔다갔다 20번 해야되는데.

웹팩은 하나로 합쳐서 날리기때문에 요청자체는 한번이된다.
![alt text](image.png)

다음과같이 번호로관리
![alt text](image-1.png)

즉시실행함수의 형태로 들어있음
