### git rebase

그동안 스쿼시 때문에 그냥 리베이스는 커밋을 하나로 합친다고 만 생각했는데

스쿼시랑 리베이스랑은 조금 다른개념인듯하다.

rebase는 커밋내역을 기준이되는 브랜치 기준으로 두줄로 만들어버려서 선형으로 만드는 것이고

스쿼시는 여러개의 커밋을 하나로 묶는것.

### git-flow

설마 깃 플로우를 다시보게 될 줄이야.

master/main => 제품 출시

develop : 다음 버젼
feature: 기능 개발

release : 이번 출시 버젼 준비 브랜치

hotfix: 출시버젼 수정

그러니 릴리즈 타고 들어간건 다시 디벨롭으로 가면 최신화를해야.

main -> develop -> feature 타고 개발 해서 되면 develop 에 merge

develop -> release 에서 테스트 -> main에 합침

핫픽스 사항이 생기면 -> main 에서 타고 나와서 만들고 디벨롭과 main에 다시 최신화

### cherry-pick

예전에 테코톡 봤는데. 커밋하나 선택해서 브랜치에 붙이는거

//내용추가
