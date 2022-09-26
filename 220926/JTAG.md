Joint Test Action Group

![Untitled](https://user-images.githubusercontent.com/91246353/192209647-7c82e850-b527-4227-9537-141acbcbd6f4.png)

![Untitled (1)](https://user-images.githubusercontent.com/91246353/192209658-ea3ef4ff-3df0-46c3-b063-66893ffdbb5f.png)

# 핀 설명
TMS (Test Mode State Pin)
TDO (Test Data Out Pin)
RTCK (JTAG Return Test Clock)
TDI (Test Data In Pin)
TRST (Test Reset Pin)
TCL (Test Clock Pin)
VCC
GND
RESET

전체적인 인터페이스는 5개의 핀 (TDI, TMS, TCK NRST, TDO)를 통해 제어합니다.

펌웨어에 Break문을 걸어가면서 변수에 값이 잘 쓰여있는지 해당 구문이 잘 실행되는지 확인하는 용도로 사용합니다.

또한 JTAG은 플래시 메모리에 소스 코드를 다운로드하는 용으로도 사용이 됩니다.

프로그램을 컴파일하고 나면 통합 바이너리 파일이 만들어지는데 이 파일을 플래시 메모리에 넣기 위해서 JTAG 포트를 사용합니다.

반대로 내용을 읽어올 수도 있습니다.

이 외에도 여러가지 인터페이스가 있는데 JTAG은 기본적으로 핀을 많이 사용하는 것이 단점입니다.
