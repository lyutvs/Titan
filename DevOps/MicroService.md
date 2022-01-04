# 마이크로서비스(MSA)

## 마이크로서비스란?

마이크로서비스란 소프트웨어를 구축하기 위한 아키텍처이자 하나의 접근 방식으로, 애플리케이션을 상호 독립적인 최소 구성 요소로 분할합니다. <br> 
모든 요소를 하나의 애플리케이션에 구축하는 전통적인 모놀리식 접근 방식 대신 마이크로서비스에서는 모든 요소가 독립적입니다.

## 모모놀리식 아키텍처와 마이크로서비스 아키텍처 비교
![msa 이미지](https://d1.awsstatic.com/Developer%20Marketing/containers/monolith_1-monolith-microservices.70b547e30e30b013051d58a93a6e35e77408a2a8.png) <br>

모놀리식 아키텍처의 경우 모든 프로세스가 긴밀하게 결합되고 단일 서비스로 실행됩니다. 
따라서 애플리케이션의 한 프로세스에 대한 수요가 급증하면 해당 아키텍처 전체를 확장해야 합니다. 
코드 베이스가 증가하게 되면 모놀리식 애플리케이션의 기능을 추가하거나 개선하기가 더 복잡해집니다. 
그리고 이러한 복잡성으로 인해 실험에 제한을 받고 새로운 아이디어를 구현하기가 어려워집니다.

마이크로서비스 아키텍처의 경우, 애플리케이션이 독립적인 구성 요소로 구축되어 각 애플리케이션 프로세스가 서비스로 실행됩니다. 
이러한 서비스는 API를 사용하여통해 통신합니다. 
서비스는 비즈니스 기능을 위해 구축되며 서비스마다 한 가지 기능을 수행합니다. 
서비스가 독립적으로 실행되기 때문에 애플리케이션의 특정 기능에 대한 수요를 충족하도록 각각의 서비스를 업데이트, 
배포 및 확장할 수 있습니다.

## 마이크로서비스의 특징

### 자율성
![자율성](https://d1.awsstatic.com/icons/benefit-icons/100x100_benefit_deployment2.c68823bf6f80f3f85c4fff89410069de9a1bd60c.png) <br>
한 비즈니스 로직이 독립성이 강하기 때문에 다른 비즈니스 로직에 영향을 주지 않으면서 개발, 배포, 운영, 확장 할 수 있습니다.
비즈니스 로직 하나당 다른 비즈니스 로직과 공유할 필요가 없습니다.

### 전문성
![전문성](https://d1.awsstatic.com/product-marketing/Serverless/benefit_85x85_gear-2.f27f2d94fe6897e2785603c4a7715d18173ff71a.png) <br>
각 서비스의 특정 문제를 해결 하는데 중점을 둡니다. 하나의 서비스가 다운되어도 다른 서비스에는 영향을 주지 못 하기 때문에 특정 문제를 해결 하는데 도움이 됩니다. <br>
시간이 지남에 따라 하나의 서비스에서 많은 기능을 제공 하면 좀더 세분화 시킬 수 있습니다.


## 장점

### 민첩성
![민첩성](https://d1.awsstatic.com/icons/benefit-icons/100x100_benefit_Low-Latency.2e96f1de3dacb3bda2a679b372d04c104718be02.png) <br>

MSA는 해당 서비스를 소유한 소규모 팀을 만들기에 적합 합니다. 팀은 기능에 대한 높은 이해도를 가지고 활동 하고 더 독립적이고 신속하게 개발 할 수 있습니다.

### 유연한 확장성
![확장성](https://d1.awsstatic.com/icons/benefit-icons/100x100_benefit_scalable.f24d5f6848364dc06c177951f15f29c63fd22f41.png) <br>
각 서비스가 지원하는 애플리케이션 기능의 수요를 충족하도록 해당 서비스를 독립적으로 확장할 수 있습니다.

### 손쉬운 배포
![배포](https://d1.awsstatic.com/icons/benefit-icons/100x100_benefit_delivery-pipeline.1e300fd9b26f94b1865ffe571f81eef55c833d38.png) <br>
[지속적 통합](https://github.com/lyutvs/DevOps_Learn/blob/main/데브옵스/지속적통합.md) 및 [지속적 배포](https://github.com/lyutvs/DevOps_Learn/blob/main/데브옵스/지속적%20배포.md) 을 통해 새로운 아이디어를 손쉽게 시험하고 문제가 발생할 경우 간단히 롤백할 수 있게 해 줍니다.

### 기술적 자유
![자유](https://d1.awsstatic.com/icons/benefit-icons/100x100_benefit_code-configuration.29104e7e882b2a715b6284a4352abfc97f9a60fc.png) <br>
팀은 자기가 쓸 언어, 프레임워크 등을 팀단위로 선택 할 수 있습니다, <br>예를들어 Login 서비스는 Spring boot 로 로직을 짜고 실시간 채팅 부분을 Nest.js 로 개발을 해도 괜찮다는 말 입니다.

### 복원성
![복원](https://d1.awsstatic.com/icons/benefit-icons/100x100_benefit_durable.54299a12d07fd6a95f634ea029ec94a6609f8eb6.png) <br>
한 서비스가 실패 해도 다른 서비스에 영향을 주지 않아 실패 하더라도 실패에 대한 저항성이 증가 합니다, 모놀리식 아키텍처에서는 단일 구성 요소가 실패하는 경우 전체 애플리케이션이 실패하게 될 수 있습니다.
