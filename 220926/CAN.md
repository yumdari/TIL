자동차에 주로 쓰이는 CAN 통신도 OSI 7 layer 프로토콜을 적용받는다.

주로 physical, datalink layer를 집중한다.

Physical layer

CAN 통신은 High, Low 두개의 전선으로 이루어져 있고 두 선의 전압차를 통해 데이터를 송수신한다.

이 때 두 전선은 노이즈를 감소시키기 위해 꼬여있고 이걸 Two pair twist system이라고 부른다.

꼬으면 왜 노이즈 감소?

평행한 두 도선에 전류가 같은 방향으로 흐르고 있다면 그 전류를 통해 일정한 방향을 가진 전자기력 벡터가 발생하게 되고

이 전자기력은 캐리어의 움직임에 노이즈(외력)을 발생시킨다.

전선을 꼬으면 전자기력의 방향이 계속 바뀌게 되고 그럼 상쇄하는 효과를 야기하여 노이즈(외력)이 감소한다.

Physical layer를 담당하고 있는 CAN Tranceiver 모듈은 아날로그 신호 <-> 디지털 신호 변환 역할을 담당한다.

비트 생성 원리는?

위에서 언급했다 싶이 두 전선을 통해 데이터를 송수신한다고 하였다.

두 도선 CAN_H(2.5~3.5V), CAN_L(2.5~1.5V)의 전압차를 통해  CAN 트랜시버는 디지털 신호1,0을 생성한다.

0bit(3.5V-1.5V)를 dominant / 1bit (2.5V-2.5V)를 recessive 라고 부르고

향후 bus access 부분에서 이 명칭의 이유가 나온다.

데이터를 수신하는 영역은 Datalink layer를 책임지는 CAN Controller 모듈에서 담당한다.

전압차 2V를 0으로 전압차 0V를 1로 비트를 변환하여 수신한다. 이 때 layer의 특징을 활용하여

오차 범위를 고려하여 범위를 수정한다.

0.9V <= Vdiff <= 5V -> 0                /               -1.0V <=Vdiff<=0.5V  -> 1

Sample point : 비트 판단 기준점

**Addressing**

TX의 주소는 모든 CAN Node에서 겹치면 안된다. RX 주소는 당연히 여러 Node 주소에서 겹쳐도 됨

(주는 놈의 주소를 공유하면 누가 줬는지 모르기 떄문)

(Can 통신은 브로드캐스팅 방식이기 때문에 누가 받는지 상관하지 않는다. 그렇기 때문에 RX 주소는

여러 노드에서 가지고 있어도 상관없다.)

Bus Access

여러 노드에서 data 전송 시 당연히 버스 충돌이 발생한다.

충돌 방지 방법?

Arbitration field 영역을 만들어 우선순위가 높은 ID를 가진 CAN Node의 데이터를 버스에 뿌려준다

이를 CSMA/CA 라고 부른다.

CAN DATA의 룰은 처음 11bit 동안 recessive bit 즉 1비트를 계속 보내야 한다.

이를 버스 IDLE상태라고 약속한다(ISO 국제표준)

CAN 통신 속도를 500kbps라고 할 때 1bit 송신하는데 2마이크로초가 걸린다.11bit 즉 22마이크로초를

1bit로 지속해야한다. 그 이후 falling edge를 발생시키기 위해 0bit를 발생하고

이를 Start of frame filed 라고 하여 프레임의 시작이라고 부른다.

그 이후의 영역을 이제 Arbitration field라고 하여 우선순위를 부여한다.

이 field를 통해 bus access가 결정된다.

**[출처]** [자동차 Classic 통신 스터디 : CAN, CANFD 1탄](https://blog.naver.com/rlagrkwns30/221796551320)|**작성자** [업글이](https://blog.naver.com/rlagrkwns30)