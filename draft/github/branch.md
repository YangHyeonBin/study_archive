# 브랜치 전략
: 다양한 전략 중 상황에 맞는 걸 사용하기

## 1. Git flow 전략
: main, develop, feature, release(=임시) 브랜치 활용

- main에서 develop 브랜치를 파고,
- develop에서 feature 브랜치를 팜

- 새로 개발할 기능을 **'feature/신기능'**과 같은 이름으로 브랜치 만들어 작업 후,
- 기능이 잘 동작하면 develop로 pull request & merge 

- develop 브랜치 내에서도 기능이 잘 돌아가서 출시할 만해지면,
- release 라는 임시 브랜치 만들어, **테스트 및 qa** 진행

- 완성되면 main 브랜치로 merge 및 배포
- develop 브랜치는 제거하지 않고 계속 사용하므로, release에서 수정한 것을 **develop에도 merge**,
- release 브랜치는 제거

- main에서 올린 것에 급한 버그 발생 시, 바로 수정 및 hotfix, 배포


## 2. Trunk-based 전략
: main 브랜치만 가져가고, 새 기능 개발할 때마다 그에 맞는 feature 브랜치 만들어 작업, main에 merge 및 배포

- git flow 전략보다 더 많이, 자주 테스트 해야 안전 (main에 바로 붙이니까)
- CI/CD와 궁합 좋음