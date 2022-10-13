보통 Digital System의 pin에 인가되는 값은 Logic 0일 때 동작 상태, 또는 Logic 1일 때 동작 상태로 많이 사용됩니다만, 어느 상태이건 만드는 사람 마음대로 동작 상태를 정하기 나름입니다. 뭐, 일단 동작 상태를 Active라고 부르며, 이때 Logic 0 Active인 pin을 Low Active라고 부르고, Logic 1 Active인 pin을 High Active라고 부릅니다.

Low Active의 경우에는 Low가 되었을 때만 동작이 되도록 확실하게 하기 위하여 평소 Default 값을 High로 만들어 놓고, Active되었을 때만 Low로 만들어주는 것이 가장 확실한 방법일 것이겠네요. 

![http://pds15.egloos.com/pds/200905/25/90/c0098890_4a1a983dbb7cc.jpg](http://pds15.egloos.com/pds/200905/25/90/c0098890_4a1a983dbb7cc.jpg)

일단 예를 들어보면 조금 더 쉬우니까, 위와 같은 회로 구성에서 봅시다. Digital Chip은 R에 비해 많이 큰 저항이라고 본다면, Low Active case에서의  Pull up이라는 건 Digital Chip의 입장에서 ①번 Switch On 상태에서는 Digital chip input에 GND 즉 0V의 전압이 가해지며, ②번 Switch Off상태에서는 Digital chip input에 3V에 가까운 전압이 가해지게 됩니다. 이는 즉, Swtich가 On될 때는 Low 값이 Digital Chip에 인가됨을 의미합니다. 만일 이 Digital chip은 input이 0일 때, 동작 가능하다고 한다면, 평소에는 3V의 input을 유지할 수 있는 이런 식의 회로 구성이 가장 타당합니다.

그럼, 반대로 High Active Pull down이라는 건 Pull up과 완전 반대로 평상시에는 Low를 유지하다가, Switch ON을 시켰을 때, High를 Digital chip에 인가 시켜주는 것을 의미합니다. ①은 switch on이며, ON을 시켰을 경우에는 확실하게 High 3V가 인가되며, Off시켰을 경우에는 Digital Chip에 0V가 인가됩니다.

![http://pds15.egloos.com/pds/200905/25/90/c0098890_4a1a9858e8b0f.jpg](http://pds15.egloos.com/pds/200905/25/90/c0098890_4a1a9858e8b0f.jpg)

이렇듯, Pull up & down은 Digital 신호의 기본적인 Default Level을 무엇으로 둘 것이냐의 문제인 것인데, 원래 Ideal한 것으로 따지면 필요 없는 회로이어야 합니다만, real world라는 건 또 그리 만만한 것이 아니라서 필요한 거죠. 예를 들어 High Active로 동작하는 Digital chip의 경우에 system이 정전기를 맞았거나, 사람이 칩을 만졌을 때, 외부 요인에 의하여 순간적으로 그때의 input이 High가 되어버린다면 Digital chip은 의도와 상관없이 동작하게 되는 경우가 있습니다. 이런 시스템이만일 핵미사일 발사 시스템의 단추와 연관되어 있다면 그것 참 무시무시한 일이 아닐 수 없습니다. 덜덜덜. 화장실 불을 켜는 정도라면 덜 위험할 수도 있긴 하지만, 조금 더 reliable하게 확실한 default 값을 보장하기 위해서 pull up이나 pull down이 회로 level에서 필요하게 되었습니다.

한 가지 더, Switch로 on, off하는 것을 보니 떠오르는 것이 하나 있지 않나 모르겠습니다. 역시나 눈치 채셨겠지만, 우리는 Transistor가 Switch로 사용가능하다는 것을 바로 전에 알아 차려 버렸습니다. 그러면, 간단하게 하나 더 Transistor를 사용해서 pull up system을 구현해 보도록 하지요.

![http://pds10.egloos.com/pds/200905/25/90/c0098890_4a1a9865585ab.jpg](http://pds10.egloos.com/pds/200905/25/90/c0098890_4a1a9865585ab.jpg)

지금껏 Digital Chip이라고 불리우던 chip은 다른 chip에 의해서 control이 된다고 가정하고 slave - 하인 이라는 의미가 참으로 적당하군요 - 라고 부르고, 좌측에 이 chip을 control하는 chip을 Master - 역시나 하인은 주인이 control 해야지 제격입니다 - 라고 부르겠습니다.

일단 Master의 output pin이 High를 주느냐, Low를 주느냐에 따라 Slave가 동작을 하게 되는데 일단 Master는 Slave를 동작시키고 싶을 때, High를 주고, Slave를 동작시키지 않을 때는 Low를 준다고 가정합시다. (Slave는 Low Active라고 할 때 - )

회로를 분석해 보면 Vcc는 Pull up을 위한 전원이고, Rc는 Pull up을 위한 저항이고요.Transistor는 Switch역할을 합니다. R1은 보통 Master chip의 output이 Logic 0일때, 0V를 제대로 내어 줘야 되는데 약간은 찔끔찔끔 전압을 내보낼 때도 있습니다. 이를 대비하여, 만일 TR이 ON 될 만큼의 전압 이하에서는 확실하게 0V로 만들어 주기 위하여 R1을 달아 Base로 전류가 흐르지 못하게 만들어 줍니다. 보통 이런식으로 switch로 사용하는 Transistor는 B와 E를 저항으로 직접 연결된 Transistor를 한 개의 소자로 해서

팔기도 합니다. Master가 0을 주면 Transistor는 off상태이며, Slave로 들어가는 input은 Pull up되어 High가 됩니다. Slave 선수 동작 안하지요. 반대로 Master가 1을 주면 Transistor는 On이 되어, Slave로 들어가는 input은 0V를 넣어주어 Slave chip이 동작하도록 해줍니다. 간단간단 입니다.

그러면, 마지막으로 이런 Switch가 Master chip에 아예 들어가 있는 경우까지 scope를 extend 해서 볼 수 있습니다. 이런 Switch가 Master chip 내부에 아예 들어가 있는 경우를 Open collector라고 부르는데, 이런 구조는 Collector가 output으로 나와 있으며 아무것도 연결되어 있지 않으니까 Open Collector라고 부르며, Open Collector는 그림과 같이 여러 개의 Master가 한 개의 Slave에 연결될 때 아주 유리한 구조인거죠.

각 Master의 명령 input앞에 달려 있는 는 inverter로서 input의 상태를 반전시킵니다. - 위의 예에서와 같이 실제 master가 주는 신호와 반대의 신호가 slave로 흘러가니까, 같은 식으로 생각한다면, Master가 Low를 주었을 때, Slave가 Low를 받게 하려면 inverter를 달면 편리하겠다는 간단간단 발상입니다. -

![http://pds12.egloos.com/pds/200905/25/90/c0098890_4a1a98a96418d.jpg](http://pds12.egloos.com/pds/200905/25/90/c0098890_4a1a98a96418d.jpg)

- 잘보면 ~ 명령1 OR 명령2

하나 이상의 여러개의 Master는 Low Active인 Slave의 Out (Slave입장에서는 input이 되겠습니다.요) 에 Low를 주기 위하여, High를 주게 되는데, 표와 마찬가지로 평소에는 High Pull up상태를 유지하다가 둘 중에 하나만 Low가 되면 Slave에는 Low가 전달되어 Slave가 동작하도록 합니다. 결국에는 Low와 High가 같이 공통 버스에 인가 되어도 서로 부딪치지 않고, Low가 이깁니다. 재미 있는 사실은 보통 chip과 chip사이에 이런 공통 버스로 연결되어 있는 경우 한 chip에서는 High, 다른 한 chip에서는 Low를 한꺼번에 공통 버스에 올려놓았을 때 그 두 chip들 사이에 저항이 없다면 순간 무한 전류가 흘러버려 system이 타 버리게 됩니다만, 이런 open collector의 경우에는 서로 달라도 상관 없는 구조입니다. 일종의 Low Active 버스라고도 볼 수 있고, 다르게 표현 하면 예를 들어 Low OR로서 어느 하나만 Low가 되면 Slave 동작 OK이므로, 여러 개의 Interrupt를 하나의 Interrupt로 인식할 때 따위의 - Slave가 Main Processor 따위의 경우겠네요  - 유리합니다.