UART(범용 비동기화 송수신기: Universal asynchronous receiver/transmitter)는 병렬 데이터의 형태를 직렬 방식으로 전환하여 데이터를 전송하는 컴퓨터 하드웨어의 일종이다. 

통신 데이터는 메모리 또는 레지스터에 들어 있어 이것을 차례대로 읽어 직렬화 하여 통신한다. 최대 8비트가 기본 단위이다.

UART는 일반적으로 컴퓨터나 주변 기기의 일종으로 병렬 데이터를 직렬화 하여 통신하는 개별 [집적 회로](https://ko.wikipedia.org/wiki/%EC%A7%91%EC%A0%81_%ED%9A%8C%EB%A1%9C)이다.

비동기 통신이므로 동기 신호가 전달되지 않는다. 따라서 수신 쪽에서 동기신호를 찾아내어 데이터의 시작과 끝을

시간적으로 알아 처리할 수 있도록 약속되어 있다. 디지털 회로는 자체의 [클럭 신호](https://ko.wikipedia.org/wiki/%ED%81%B4%EB%9F%AD_%EC%8B%A0%ED%98%B8)를 사용하여 정해진

속도로 수신 데이터로부터 비트 구간을 구분하고 그 비트의 논리 상태를 결정하여 데이터 통신을 한다.

시리얼 통신을 사용하기 위해서는 보내는 쪽(TX)와 받는 쪽(RX)에서 약속을 정해야 하는데, 이를 프로토콜(Protocol)이라고 한다.

MCU에서는 0과 1의 값만을 처리할 수 있으므로 0은 GND, 1은 VCC로 데이터를 전송하고,

받는 쪽에서는 GND와 VCC를 다시 0과 1의 이진값으로 변환하여 사용한다.

보내는 쪽(TX)와 받는 쪽(RX)이 원할하게 데이터를 교류하려면, 데이터를 보내는 속도에 대하여

약속(프로토콜, Protocol)이 정해져 있어야 한다.

[https://t1.daumcdn.net/cfile/tistory/99BC37345A45F5262C](https://t1.daumcdn.net/cfile/tistory/99BC37345A45F5262C)

UART에서는 보내는 쪽(TX)와 받는 쪽(RX)에서 데이터를 보내는 속도를 **보율(baud rate)**로 정하고 있다.

[https://t1.daumcdn.net/cfile/tistory/99789E4A5A45F5D737](https://t1.daumcdn.net/cfile/tistory/99789E4A5A45F5D737)

보내는 쪽(TX)과 받는 쪽(RX)이 동일한 속도롤 데이터를 주고받는다고 하여 정확하게 통신이

이루어지는 것은 아니다.

보내는 쪽(TX)은 항상 데이터를 보내는 것이 아니며, 필요한 경우에만 데이터를 보낸다.

따라서, 받는 쪽(RX)은 언제 보내는 쪽(TX)이 데이터를 보내는지,

그리고 어디서부터가 보내는 쪽(TX)에서 보낸 데이터의 시작인지 알아낼 수 있는 방법이 필요한데,

이를 위해서, UART에서는 **'0'의 시작 비트(start bit)**와 **'1'의 정지 비트(stop bit)**를 사용한다.

UART는 바이트 단위 통신을 주로 사용하며, 시작 비트(start bit)와 정지 비트(stop bit)가 추가되어,

**10비트 데이터를 전송**하는것이 일반적이다. (**패리티 비트를 사용하지 않을 경우에**)

[https://t1.daumcdn.net/cfile/tistory/999CEC4B5A45F75434](https://t1.daumcdn.net/cfile/tistory/999CEC4B5A45F75434)

UART 통신은 **전이중 방식(full duplex)** 통신으로 송신과 수신을 동시에 진행할 수 있으며, 이를 위해서

2개의 범용 입출력 핀이 필요하다.(시리얼포트 -> TX, RX)

[https://t1.daumcdn.net/cfile/tistory/999C05435A461FA81F](https://t1.daumcdn.net/cfile/tistory/999C05435A461FA81F)

예를 들어, 컴퓨터와 ATMEGA16를 연결하는 경우, 컴퓨터와의 연결에 있어서 RS232 연결을 사용하며,

RS232에서 사용하는 신호 레벨은 UART의 신호 레벨(TTL)과 달라 별도의 변환 장치를 사용하여

레벨을 변환시켜 주어야만 사용이 가능하다.

RS232 통신에 있어서 가장 대표적으로 쓰이는 IC는 **MAX232** 이다.

[https://t1.daumcdn.net/cfile/tistory/997CF5445A4620C60E](https://t1.daumcdn.net/cfile/tistory/997CF5445A4620C60E)

이외에 USB-시리얼 변환 장치를 통해서 컴퓨터와 MCU 보드 간의 통신이 가능하다.

[https://t1.daumcdn.net/cfile/tistory/99242F465A46228C05](https://t1.daumcdn.net/cfile/tistory/99242F465A46228C05)