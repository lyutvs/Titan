# 지속적 배포(CD)

## 지속적 배포란?

**지속적 배포(Continuous Delivery)** 는 프로덕션에 릴리스하기 위한 코드 변경이 자동으로 준비되는 소프트웨어 개발 방식입니다.\
지속적 배포는 빌드 후 모든 코드 변경을 테스트환경/실 배포 환경에 배포 함으로써 [지속적 통합](https://github.com/lyutvs/DevOps\_Learn/blob/main/%EB%8D%B0%EB%B8%8C%EC%98%B5%EC%8A%A4/%EC%A7%80%EC%86%8D%EC%A0%81%ED%86%B5%ED%95%A9.md) 을 확장 합니다.\
효과적인 CD를 하기 위해서는 CI가 안정적으로 구축이 되어있어야 합니다.

## 장점

### 소프트웨어 릴리즈 프로세스 자동화

![프로세스 자동화](https://d1.awsstatic.com/product-marketing/DevOps/CICD\_automate-release.06a38e2a6d9e866ffb50ddb3168e6d9976c2ddf5.png)\
지속적 전달을 사용하면 팀에서 프로덕션에 릴리스하기 위한 코드 변경을 자동으로 빌드, 테스트 및 준비하여, 좀 더 빠르고 효율적으로 소프트웨어를 전달할 수 있습니다.

### 개발자 생산성 향상

![생산성 향상](https://d1.awsstatic.com/product-marketing/DevOps/CICD\_improve-productivity.c73191c7af7e9f0a859c9ec8af8b1bd4e4eae5be.png)\
수동 작업에 대한 부담을 덜고 고객에게 배포되는 오류 및 버그 수를 줄이는 데 도움이 되는 기능을 활용함으로써 팀의 생산성을 높일 수 있습니다.

### 버그를 더 빠르게 발견 및 해결

![버그](https://d1.awsstatic.com/product-marketing/DevOps/CICD\_find-bugs.a60937d9bd1ba25ac3781db46758ebe92c5c889a.png)\
좀 더 자주 테스트를 함으로써 큰 문제로 발전 하기 전에 버그를 발견하고 해결 할 수 있습니다.

### 업데이트를 좀 더 빠르게 제공

![제공](https://d1.awsstatic.com/product-marketing/DevOps/CICD\_deliver-updates.1d175ba80e02e998a0bcb5f4918bac95338820b2.png)\


팀이 좀 더 빠르고 좀 더 빈번하게 고객에게 업데이트를 제공할 수 있습니다. 앞 장점을 모두 가져 테스트를 통과한 아티팩트를 빌드 할 수 있습니다.
