
# What Is a regular Expression Concept

정규식을 사용하면 문자열의 패턴을 매칭시킴.

# Readability 

매우 복잡하고 이해하기어려울수있음 => 정규식이 평판이 안좋은 이유 중 하나. 
이에대한 solution? => comment
6개월 뒤에는 자신이 작성한 정규식의 의도를 잊어버릴수있음. 그러니 주석은 좋은 선택 

# Regg-ex or Redge-ex 
정규식은 regex라고 줄여서 말하기도함. 
그리고 이건 Regg-ex or Redge-ex로 불리기도함
레겍스 렛지엑스 선택은 니몫
regex101.com 
간단한 건 변경이없지만 심화는 플랫폼에 따라 달라질수도있음 

정규식의 시작과 끝을 알려주는게 => '/' 
그래서 // 로 사실상 완성 


# Quantifiers

문자 하나가 몇번이나 반복될수있는지에 대한 정량자 

? => zero or one times 
+ => one or more times 1번이상 무조건 1개는 있어야됨.
* => 0 or more times 0 혹은 무한(제한없음)

## 특문
?+* . {} [] () ^? 
특문을 매치시키고 싶다면. \이스케이프와 함께 사용
백슬래시 
\*


## {} Quantifiers
세밀한 컨트롤 
{1,3} => 2개  1과 3사이 

{3} => 3개반복 허용 
{3,} 3개 이상 





