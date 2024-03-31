# 리액트 네이티브 복습

RN은 React-dom의 대안이다
네이티브 기기 API를 키긴 해야되지만 그래도 자바스크립트에서 쓰도록 할 수있음.

## 리액트 네이티브 내부 살펴보기 

- View
웹브라우저 / 네이티브 컴포넌트 ios , android , react native jsx 다음과 같이 컴파일

![image](https://github.com/MAGHC/TIL-2024-/assets/89845540/6777b0ef-0454-4896-b285-953ccbc03257)

- Logic

Ui와 요소와 다르게 논리는 컴파일 되지 않는다. 
자바스크립트 코드는 리액트 네이티브가 호스트한 대로 실행하게 됨.
네이티브앱 안에 리액트 네이티브를 이용해서 돌아가게 만듦

## Expo Cli vs React Native Cli 

두 가지 툴 모두 리액트 네이티브 프로젝트를 만들고 테스팅 기기 및 시뮬레이터에 React Native앱을 실행할 뿐만 아니라 
앱을 구축하고 앱스토어 배포하게 해줌.

실질적으로 앱을 구축하고 배포 가능한 패키ㄱ지로 만들어. 업로드하기 위해 꼭 필요한 툴. 

Expo에서 언제든 네이티브로 바꿀수있음. 

Expo Cli 보다 Rn이 더 불편하다.  단지 있는건 Expo이전에 존재해서. 

순수 Rn 워크플로우인 Rn cli의 장점은 자바나 Ojective-C , Swift , kotlin 과 같은 네티이브 소스 코드와 통합하기가 비교적 쉽다. 

__JS코드와 네이티브 기기 소스 코드를 합쳐야 한다면 Rn cli 를 쓰는게 좋다.__ 


## 프로젝트 생성 / 실행

npx create-expo-app

npm start 

expo 앱 => scan 


## 로컬 개발 환경 설정 

Android studio => create device => more action => virtual device => play store가 에뮬레이터에 포함되어있어야 expo 앱 다운로드해서 미리보기 가능 

ios => appstore = > xcode => preferences 메뉴 => location => cli tools에 버전선택 

윈도우는 아이폰 테스트불가. 

a를누르면 안드 i를누르면 ios 시뮬레이터 실행 



