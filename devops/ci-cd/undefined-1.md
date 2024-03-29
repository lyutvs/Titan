# 지속적 통합(CI)

## 지속적 통합이란

자동화된 빌드 및 테스트가 실행된후 개발자가 변경한 내용을 중앙 레포지토리에 병합 시키는 [데브옵스](https://github.com/lyutvs/DevOps\_Learn/blob/main/%EB%8D%B0%EB%B8%8C%EC%98%B5%EC%8A%A4/DevOps%EB%9E%80.md) 의 한 개발 방식입니다.

## 지속적 통합이 필요한 이유

이전에는 개발자가 작성한 코드가 장기적으로 격리되어있고, 작업이 완료한 이후에 메인 브런치에 병합 했습니다. 이 때문에 병합 할때 번거롭고 시간을 소모적으로 사용하게 되었습니다. 이러한 요소로 인해 유저에게 좀더 빠르게 서비스를 제공하기 어려워 집니다.

## 지속적 통합 작동 방식

CI 는 trigger를 자기 자신의 입맛에 맞게 yml 파일로 설정 할 수 있다. CI를 지원 하는 여러가지 툴마다 세팅 방식이 다를수도 있다.\


![작동빙식](https://d1.awsstatic.com/product-marketing/DevOps/continuous\_integration.4f4cddb8556e2b1a0ca0872ace4d5fe2f68bbc58.png)\
지속적 통합에서는 개발자가 Git와 같은 버전 관리 제어 시스템을 사용하여 공유된 레포지토리에 빈번하게 커밋하게 됩니다. 각 커밋에 앞서, 개발자는 통합 전에 코드에 로컬 유닛 테스트를 수행할 수 있습니다.\
지속적 통합 서비스는 새로운 코드 변화에 대한 유닛 테스트를 자동으로 구축하고 실행하여 즉시 모든 오류를 표면화합니다.

## 장점

### 개발자 생산성 향상

![생산성 향상](https://d1.awsstatic.com/product-marketing/DevOps/CICD\_improve-productivity.c73191c7af7e9f0a859c9ec8af8b1bd4e4eae5be.png)\


지속적 통합을 사용하면 개발자가 수동 작업에 대한 부담을 줄이고 고객에게 제공되는 서비스에 대한 버그가 줄어들어 팀의 생산성을 높일수 있습니다.

### 버그 해결및 발견 향상

![버그](https://d1.awsstatic.com/product-marketing/DevOps/CICD\_find-bugs.a60937d9bd1ba25ac3781db46758ebe92c5c889a.png)\
테스트를 빈번하게 실행 함으로써 이후에 더 큰 문제로 발전하는것을 막을 수 있습니다.

### 업데이트를 좀더 빠르게 제공

![제공](https://d1.awsstatic.com/product-marketing/DevOps/CICD\_deliver-updates.1d175ba80e02e998a0bcb5f4918bac95338820b2.png)\
지속적 통합을 이용하면 팀이 좀더 빠르고 좀 더 빈번하게 고객에게 서비스를 제공 할 수 있습니다.
