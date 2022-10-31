MQTT는 M2M, IOT를 위한 프로토콜로서, 최소한의 전력과 패킷량으로 통신하는 프로토콜입니다. 따라서 IOT와 모바일 어플리케이션 등의 통신에 매우 적합한 프로토콜입니다.

MQTT는 HTTP, TCP등의 통신과 같이 클라이언트-서버 구조로 이루어지는 것이 아닌, Broker, Publisher, Subscriber 구조로 이루어집니다.

![https://miro.medium.com/max/731/1*lKWgSNIYc1Pil5FFoAHMkA.png](https://miro.medium.com/max/731/1*lKWgSNIYc1Pil5FFoAHMkA.png)

Publisher는 Topic을 발행(publish) 하고, Subscriber는 Topic에 구독(subscribe)합니다. Broker는 이들을 중계하는 역할을 하며, 단일 Topic에 여러 Subscriber가 구독할 수 있기 때문에, 1:N 통신 구축에도 매우 유용합니다.

MQTT에서 Topic은 /를 사용해서 구성되기 때문에,

![https://miro.medium.com/max/848/1*nJAaE5oGbYpYpxILVzwY9g.png](https://miro.medium.com/max/848/1*nJAaE5oGbYpYpxILVzwY9g.png)

위와 같이 계층을 구성한다면, IOT 센서와 같은 데이터를 관리하기에 매우 용이합니다.

MQTT는 QoS(Quality of Service)를 제공하는데, 총 3단계로 나뉘어져 있습니다.

- 0 : 메세지는 한번만 전달되며, 전달 이후의 수신 과정을 체크하지 않는다.1 : 메세지는 한번 이상 전달되고, 핸드셰이킹 과정을 추적하나, 엄격하게 추적하지 않기 때문에 중복 수신의 가능성이 있다.2 : 메세지는 한번만 전달되고, 핸드셰이킹의 모든 과정을 체크한다.

QoS의 단계가 높아질 수록 통신의 품질은 향상되지만, 그에 따라 성능 저하의 가능성이 있으므로. MQTT의 QoS는 프로젝트의 특성에 따라 결정되어야 합니다.