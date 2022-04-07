# MPEG TS 란

---

MPEG transport stream : `TS`, `TP`, `MPEG-TS` 로 줄일 수 있다

오디오, 비디오 데이터 전송을 위한 통신 프로토콜이다.

`PES`( Packetized Elementary Streams ) 와 기타 데이터를 포함하는 디지털 컨테이너 포맷의 일종

## 포맷 구조

---

![](../../images/비트.png)

1Byte + 2Byte + 1Byte = 4Byte

PES : 184Byte

*8bits : SyncByte* : 0x47

### *1bit : Transport Error Indicator* ( 전송오류 표시기 )


ㄴ 에러 : 1, 정상 : 0

### *1bit :  Payload Unit Start Indicator* ( 페이로드 유닛 시작 표시기 )

ㄴ Original Data 의 위치 정보

* 0: packet 에 Original Data 중간 부분에 포함
* 1 : packet 에 Original Data 처음 부분에 포함

<br>

### *1bit : Transport Priority indicator* ( 전송 우선 순위 )

ㄴ ts packet 의 우선 순위를 표시함

같은 PID 가 존재할 경우

* 1 : 우선 순위

* 0 : 후 순위

### *13bits : PID* ( 패킷 아이디 )

ㄴ 0x0000 ( PAT ) Program Association Table

ㄴ 0x0001 ( CAT ) Conditional Access Table

ㄴ 0x0002 ( TSDT ) Transport Stream Description Table

ㄴ 0x0003 ~ 0x000F Reserved

ㄴ 0x1FFF Null Packet


### *2bits : Transport scrambling control* ( 스크램블 제어 )

ㄴ 00 : not scrambled

ㄴ 01 : 사용 예약

ㄴ 10 : 짝수로 스크램블

ㄴ 11 : 홀수로 스크램블

### *2bits : Adaptation Field Control* ( 유효필드 제어 )

ㄴ 01 : 유효 필드 없음, 페이로드 만 있음

ㄴ 10 : 유효 필드 만 있음, 페이로드 없음

ㄴ 11 : 유효 필드 다음에 페이로드 있음

ㄴ  00: 사용안함 ( 추후에 사용 가능 )

### *4bits : Continuity counter* ( 연속 카운터 )

ㄴ 15가 넘어가면 0으로 초기화 ( 같은 PID packet +1 증가 ) 전송

*PES Header*

*ES Data*

용어 정리

[https://ko.wikipedia.org/wiki/MPEG_트랜스포트_스트림](https://ko.wikipedia.org/wiki/MPEG_%ED%8A%B8%EB%9E%9C%EC%8A%A4%ED%8F%AC%ED%8A%B8_%EC%8A%A4%ED%8A%B8%EB%A6%BC)

<br> 


### PID

TS의 각 테이블이나 기초 스트림(ES)은 13비트 패킷 ID (PID)로 식별한다.

역다중화기(demultiplexer)는 같은 PID로 식별된 패킷을 검색하여 부분적으로 TS로부터 기초 스트림을 추출한다.

시분할 다중화는 얼마나 자주 특정한 PID가 TS에 나타나는지를 결정하는 데 쓰인다.

<br>


### 프로그램

각 프로그램은 고유 PID를 갖는 프로그램 맵 테이블 (PMT)로 기술되며 그 프로그램과 연결된 기초 스트림은 PMT에 나열된 PID를 가진다.

<br> 


### PSI

ㄴ 프로그램 연결 (Program Association, PAT)

ㄴ 프로그램 맵 (Program Map ,PMT)

ㄴ 조건식 제한 접근(Conditional Access, CAT)

ㄴ 네트워크 정보(Network Information, NIT)

<br> 


### PAT ( Program Association Table )

ㄴ 해당 프로그램이 PAT에 존재하지 않으면 기본 PID 값 (0x0010)이 NIT에 쓰인다.

<br> 

### PMT ( Program Map Table )

ㄴ 위키 참고

### PCR

ㄴ 위키 참고

### Null 패킷

ㄴ 위키 참고

* *-- 실제 TS 를 분석 해 보자 ---*

```tsx
47 : SyncByte

bits 로 변환 하면 다음과 같다

40 : 0100 0000

11 : 0001 0001

10 : 0001 0000

0100 0000 0001 0001 0001 0000

Transport Error Indicator : 0            ( 정상 )

Payload Unit Start Indicator : 1        ( Original Data 처음 부분에 포함 ) 

Transport Priority indicator : 0       ( 후순위 )

PID : 0000000010001                  ( 0x0011 )

Transport scrambling control : 00 ( not scrambled )

Adaptation Field Control : 01         ( 유효 필드 없음, 페이로드 만 있음 )

Continuity counter : 0000             ( 0 )

PES Header & ES Data ( 184 byte )
```