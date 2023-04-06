# Docker 란?

![도커ㅓ](https://d1.awsstatic.com/acs/characters/Logos/Docker-Logo\_Horizontel\_279x131.b8a5c41e56b77706656d61080f6a0217a3ba356d.png)\


도커는 컨테이너 기반의 오픈소스 가상화 플랫폼 이다.

컨테이너라 하면 배에 실는 네모난 화물 소송용 박스를 생각할 수 있는데 각각의 컨테이너 안에는 물건 등을 넣을수 있고 규격화 되어 배, 트레일러등 으로 쉽게 운반 할수 있다.

![컨테이너](https://miro.medium.com/max/1400/0\*ujI404Gnomn1Wz5h.png)\
컨테이너라 하면 배에 실는 네모난 화물 소송용 박스를 생각할 수 있는데 각각의 컨테이너 안에는 옷, 신발, 전자제품, 술, 과일등 다양한 화물을 넣을 수 있고 규격화되어 컨테이너선이나 트레일러등 다양한 운송수단으로 쉽게 옮길 수 있습니다.

컨테이너는 격리되어 있고 그 안에서 가상 프로세스가 동작하는 방식 인데 기존에 있던 가상화 방식과는 다른 개념이 있다.

![os 가상화](https://www.redhat.com/cms/managed-files/what-is-a-container.png)\


전가상화든 반가상화든 추가적인 OS를 설치하여 가상화하는 방법은 어쨋든 성능문제가 있었고 이를 개선하기 위해 **프로세스를 격리** 하는 방식이 등장합니다.

하나의 서버에 여러개의 컨테이너를 실행하면 서로 영향을 미치지 않고 독립적으로 실행되어 마치 가벼운 VMvitual Machine을 사용하는 느낌을 준다. 실행중인 컨테이너에 접속하여 명령어를 입력할수 있고 호스트의 특정 포트와 연결하거나 호스트의 특정 디렉토리를 내부 디렉토리인 것처럼 사용할 수도 있습니다.

새로운 컨테이너를 만든는데 걸리는 시간은 겨우 1-2초로 가상머신과 비교도 할 수 없이 빠릅니다.

![도커 설명](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2\&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbLO1jV%2FbtqF4yJWiMb%2Fg0fPTY5UMZiiC07IZxrCx0%2Fimg.png)

도커에서 가장 중요한 개념은 컨테이넌와 함께 이미지라는 개념입니다.

이미지는 **컨테이너 실행에 필요한 파일과 설정값등을 포하하고 있는 것** 으로 상태값을 가지지 않고 변하지 않습니다. 컨테이너는 이미지를 실행한 상태라고 볼수 있고 추가되거나 변하는 값은 컨테이너에 저장됩니다. 같은 이미지에서 여러개의 컨테이너를 생성할 수 있고 컨테이너의 상태가 바뀌거나 컨테이너가 삭제되더라고 이미지는 변하지 않고 그대로 남아있다.

ubuntu이미지는 ubuntu를 실행하기 위한 모든 파일을 가지고 있고 MySQL이미지는 debian을 기반으로 MySQL을 실행하는데 필요한 파일과 실행 명령어, 포트 정보등을 가지고 있습니다. 좀 더 복잡한 예로 Gitlab 이미지는 centos를 기반으로 ruby, go, database, redis, gitlab source, nginx등을 가지고 있습니다.

말그대로 이미지는 컨테이너를 실행하기 위한 모오오오오든 정보를 가지고 있기 때문에 더 이상 의존성 파일을 컴파일하고 이것저것 설치할 필요가 없습니다. 이제 새로운 서버가 추가되면 미리 만들어 놓은 이미지를 다운받고 컨테이너를 생성만 하면 됩니다. 한 서버에 여러개의 컨테이너를 실행할 수 있고, 수십, 수백, 수천대의 서버도 문제없습니다.

![도커 허브](https://subicura.com/assets/article\_images/2017-01-19-docker-guide-for-beginners-1/docker-store.png)

도커 이미지는 [Docker hub](https://hub.docker.com/)에 등록하거나 [Docker Registry](https://docs.docker.com/registry/) 저장소를 직접 만들어 관리할 수 있습니다. 현재 공개된 도커 이미지는 50만개가 넘고 Docker hub의 이미지 다운로드 수는 80억회에 이릅니다. 누구나 쉽게 이미지를 만들고 배포할 수 있습니다.

## 왜 이리 핫한가?

![장점](https://subicura.com/assets/article\_images/2017-01-19-docker-guide-for-beginners-1/image-layer.png)

도커 이미지는 컨테이너를 실행하기 위한 모든 정보를 가지고 있기 때문에 보통 용량이 수백메가에 이릅니다. 처음 이미지를 다운받을 땐 크게 부담이 안되지만 기조 이미지 파일 하나 추가 했다고 수백메가를 다시 다운받는다면 매우 비효율적일 수 밖에 없다.

도커는 이런 문제를 해결하기 위해 **레이어** 라는 개념을 사용하고 유니온 파일 시스템을 이용하여 여러개의 레이어를 하나의 파일시스템으로 사용할 수 있게 해줍니다. 이미지는 여러개의 읽기 전용read only 레이어로 구성되고 파일이 추가되거나 수정되면 새로운 레이어가 생성됩니다. ubuntu 이미지가 A + B + C의 집합이라면, ubuntu 이미지를 베이스로 만든 nginx 이미지는 A + B + C + nginx가 됩니다. webapp 이미지를 nginx 이미지 기반으로 만들었다면 예상대로 A + B + C + nginx + source 레이어로 구성됩니다. webapp 소스를 수정하면 A, B, C, nginx 레이어를 제외한 새로운 source(v2) 레이어만 다운받으면 되기 때문에 굉장히 효율적으로 이미지를 관리할 수 있습니다.

컨테이너를 생성할 때도 레이어 방식을 사용하는데 기존의 이미지 레이어 위에 읽기/쓰기read-write 레이어를 추가합니다. 이미지 레이어를 그대로 사용하면서 컨테이너가 실행중에 생성하는 파일이나 변경된 내용은 읽기/쓰기 레이어에 저장되므로 여러개의 컨테이너를 생성해도 최소한의 용량만 사용합니다.

![장점](https://subicura.com/assets/article\_images/2017-01-19-docker-guide-for-beginners-1/image-url.png)

이미지는 url 방식으로 관리하며 태그를 붙일 수 있습니다. ubuntu 14.04 이미지는 [docker.io/library/ubuntu:14.04](http://docker.io/library/ubuntu:14.04) 또는 [docker.io/library/ubuntu:trusty](http://docker.io/library/ubuntu:trusty) 이고 [docker.io/library는](http://docker.io/library%EB%8A%94) 생략가능하여 ubuntu:14.04 로 사용할 수 있습니다. 이러한 방식은 이해하기 쉽고 편리하게 사용할 수 있으며 태그 기능을 잘 이용하면 테스트나 롤백도 쉽게 할 수 있습니다.

## DockerFile

```docker
# vertx/vertx3 debian version
FROM subicura/vertx3:3.3.1
MAINTAINER chungsub.kim@purpleworks.co.kr

ADD build/distributions/app-3.3.1.tar /
ADD config.template.json /app-3.3.1/bin/config.json
ADD docker/script/start.sh /usr/local/bin/
RUN ln -s /usr/local/bin/start.sh /start.sh

EXPOSE 8080
EXPOSE 7000

CMD ["start.sh"]
```

도커는 이미지를 만들기 위해 Dockerfile이라는 파일에 자체 DSLDomain-specific language언어를 이용하여 이미지 생성 과정을 적습니다. 추후에 문법에 대해 자세히 다루겠지만 위 샘플을 보면 그렇게 복잡하지 않다는 걸 알 수 있습니다.

서버에 어떤 프로그램을 설치하려고 이것저것 의존성 패키지를 설치하고 설정파일을 만들었던 경험이 있다면 더 이상 그 과정을 블로깅 하거나 메모장에 적지 말고 Dockerfile로 관리하면 됩니다. 이 파일은 소스와 함께 버전 관리 되고 원한다면 누구나 이미지 생성과정을 보고 수정할 수 있습니다.

### Command와 API

도커 클라이언트의 커맨드 명령어는 정말 자아아알 만들어져 있습니다. 대부분의 명령어는 직관적이고 사용하기 쉬우며 컨테이너의 복잡한 시스템 구성을 이해하지 못하더라도 편하게 사용할 수 있습니다. 또한 http기반의 Rest API도 지원하여 확장성이 굉장히 좋고 훌륭한 3rd party 툴이 나오기 좋은 환경입니다.

### 유용한 새로운 기능들

도커는 발전속도가 아주 빠른 오픈소스입니다. 사용하면서 부족하다고 느꼈던 부분은 빠르게 개선되고 새로운 버전이 나오면 유용한 기능이 대폭 추가됩니다.
