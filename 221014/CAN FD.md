CAN with Flexible Data rate

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2a6db4e6-c8c5-448f-846f-87be9eabac69/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/da42a077-1a89-478b-ad0c-0a712c21adc0/Untitled.png)

Bosch사가 개발한 CAN 통신 네트워크는 약 30년 동안 ECU를 연결하는 직렬 버스 네트워크 통신으로 자동차 산업에서 지배적인 통신 방법이었습니다. 하지만 차량 내 데이터 트래픽의 증가로 CAN 버스 네트워크에 높은 부하가 가해지면서 보다 나은 통신 방법이 필요했습니다. 한 네 트워크를 여러 개의 버스로 분할하는 방법이나 고성능의 FlexRay로 전환하는 방법은 많은 투자비용을 요구했습니다.

이 때 2012년 Bosch사가 새롭게 공개한 CAN 프로토콜인 CAN FD(CAN with Flexible Data rate)가 차량 통신 네트워크의 새로운 기반이 되었습니다. 과연 CAN FD 통신의 어떤 특징이 통신량 증가에 따른 병목현상을 해결하기 위한 솔루션이 되었는지 알아볼까요?

1. 데이터 길이
    
    기존 CAN 프로토콜의 8Bytes에서 64Bytes로 확장
    
2. 데이터 전송 속도
    
    100Kbit/s ~ 5Mbit/s
    
    CAN FD 표준에서 최고 15Mbit/s까지 허용
    
    High Speed CAN(1Mbit/s) 속도와 FlexRay(10Mbit/s) 전송속도의 사이
    
3. 데이터 보안

CRC(Cyclic Redundancy Check) Filed 증가

확장된 데이터 길이에도 기존 CAN 프로토콜과 동일한 요건 충족

이 외에 기존 CAN 하드웨어 사용이 가능하다는 점, FlexRay와 유사한 성능을 보이지만 비용이 저렴하다는 점 등을 통해 CAN FD     통신이 떠오르는 통신 네트워크가 되었습니다.

그렇다면 이번에는 간단히 그림과 표로 표현한 CAN과 CAN FD 통신의 프레임의 차이점을 통해 CAN FD 통신의 프레임 구성을 살펴보겠습니다.

![https://mblogthumb-phinf.pstatic.net/MjAxODExMjlfMTc0/MDAxNTQzNDc4OTY1NTM2.KAMvxWJjm4pUzI-RbR0UJ4Qph9_ByorkZBXAFoHgPO0g.PRNnX_DKqXHD6HN_zpiSi1ZFIhfK0rZtfz4OgjOFIwIg.PNG.suresofttech/image.png?type=w800](https://mblogthumb-phinf.pstatic.net/MjAxODExMjlfMTc0/MDAxNTQzNDc4OTY1NTM2.KAMvxWJjm4pUzI-RbR0UJ4Qph9_ByorkZBXAFoHgPO0g.PRNnX_DKqXHD6HN_zpiSi1ZFIhfK0rZtfz4OgjOFIwIg.PNG.suresofttech/image.png?type=w800)

<그림 2> CAN과 CAN-FD 프레임 구조 차이점 (출처: Vector E-learning)

1) BRS 비트로 Control field와 Data field 부분의 비트 속도를 올려 동일 시간에 더 많은 데이터 전송

3) Control Field는 6Bits → 9Bits로, Data Field는 최대 8Bits → 64Bits로 확장

Control Field에 추가된 비트는 EDL, BRS, ESI이며 DLC 값에 따라 Data Field의 길이 선택

CAN 프레임에 대한 설명은 이전 포스팅에서 설명하였으니 이번 포스팅은 CAN-FD 프레임에서 변경되거나 추가된 비트에 대해 살펴보겠습니다.

<표 1> CAN-FD 프레임 추가 설명

<표 2> DLC 값에 따른 데이터 길이 테이블

지금까지 기존 CAN에서 진화한 CAN-FD에 대해 알아보았습니다. 지속적으로 늘어나는 차량 내 정보를 주고받기 위해서 앞으로는 어떠한 통신 네트워크가 발전할지 기대하면서 이번 포스팅을 마치겠습니다.

| 이름 | 설명 |
| --- | --- |
| EDL (Extended Data Length)
기존 CAN 프레임과 구분 | Dominant(0) : CAN 프레임
Recessive(1) : CAN FD 프레임 |
| BRS (Bit Rate Switch)
비트 속도 전환 | Dominant(0) : No change of bit rate for data phase
Recessive(1) : Change to higher bit rate for data phase |
| ESI (Error State Indicator)
CAN FD 노드 에러 식별 | Dominant(0) : CAN FD node is error active
Recessive(1) : CAN FD node is error passive |
| DLC (Data Length Code)
데이터 확장 비트 (참고: 표2) | CAN : 최대 8Bytes
CAN-FD : 최대 64Bytes |
| CRC (Cyclic Redundancy Check)
오류 검출 비트 | CAN : 15Bits
CAN-FD : 18, 22Bits |

| DLC | Data Field Bytes CAN | Data Field Bytes CAN-FD |
| --- | --- | --- |
| 0 | 0 | 0 |
| 1 | 1 | 1 |
| 2 | 2 | 2 |
| 3 | 3 | 3 |
| 4 | 4 | 4 |
| 5 | 5 | 5 |
| 6 | 6 | 6 |
| 7 | 7 | 7 |
| 8 | 8 | 8 |
| 9 | 8 | 12 |
| 10 | 8 | 16 |
| 11 | 8 | 20 |
| 12 | 8 | 24 |
| 13 | 8 | 32 |
| 14 | 8 | 48 |
| 15 | 8 | 64 |