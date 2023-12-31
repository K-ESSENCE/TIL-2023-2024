

## 상태관리 
컴포넌트 상태
전역
서버상태 (탠스택 만든 사람이언급)
상태변경
상태최적화
렌더링 최적화
불변성
상태관리자 

### 왜 상태를 관리하는가 

상태? : 사물  현상이 놓여있는 모양 / 형편


### useEffect 

useEffect와 기명함수 함께 사용하기  

팀이 많아지면 익명함수를 기명함수로 바꾸는것도 방법이다.

```

useEffect(fucntion isInView()=>{),[]) // 이걸로 어떤것인지 추측이 가능

대략적인 추상화.


어 클린업에서도 사용가능
reutn function Remove어쩌고()=>{}

이것의 가장 큰 장점은? => 에러가 터졌을 때
console.log 나 report 도구를 쓰거나 react Dev 툴 등을 씀

이런것들을 볼 때 다 로그로 보게 되어있음. 같은 useEffect 인데 다 익명함수로 3,4 개씩 있다고 하면 찾기가 굉장히 어려움.

기명함수를 남기게 된다면. 로그에 콜스택에 쌓여서 찾기 쉬움


useEffect도 solid 처럼 한가지 역할 만 하도록.하자

이것을 점검하는 방법? =>
1. 콜백에 기명함수 적용.
2. 디펜던시 어레이에 너무 많은 대상이 있는게 아닌지.


useEffect(()=>{

redirect(newPath);

const userInfo = setLogin(token)

},[token,newPath])

이게 위험한 이유는 토큰이 바뀔떄랑 주소가 바뀔때랑 로직이 뒤섞여있다.

일단 이런경우 무조건 분리를 해야된다.

경로 바뀌었는데 로그인 로직 타버릴수도있고

토큰 바꼈더니 리다이렉트 될수도있음 이게 정말 위험하다.



```

useEffect를 하나에 다 때려넣으려고 하지마라.

명확하게 의존성을 분리해라 .


useEffect(()=>{

redirect(newPath);

const userInfo = setLogin(token)

if(option){

//이런식으로 부가적으로 사용해도 괜찮은것만. 따로 

}

},[token,option])




