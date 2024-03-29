
- modbus 는 프로토콜 중에 하나다.
- RS485 또는 TCP 위에 적용되는 프로토콜이다.

## RS485 의 이해 - part 1
--- 
- RS485 위에 동작하도록 먼저 만들어졌다.
- RS485 란?
	- 시리얼 통신 중의 하나.
- 네트워크 통신이 이뤄지기 위해서는 유무선 모두 a-b 가 연결되어야한다.
	- 유선이면 단자에 대한 약속,
	- 무선이면 어떤 식으로 연결할 건지 약속이 정해져야한다.
	- 데이터를 어떻게 보낼 것인지에 대한 약속 또한 정해야한다.
		- 전압이 1이 두번 들어오면 1로 인식할 건지, 0이 한번 들어오면 0으로 인식할 건지 등
		- 어마어마한 것들을 정해야한다.
- 시리얼 통신
	- 시리얼 케이블 상에는 0101110001 처럼 한번에 쭈욱 들어오게 된다.
	- 병렬 처리는 01 / 01 / 11 / 00 / 01 이렇게 병렬적으로 들어올 수 있다.
- RS485는 아래 4가지에 대해서 설정을 해줘야한다.
	1. bps : bit per sec &rightarrow; 전송 속도
		- bps 가 통신에 필요한 이유? 
		    : 01011110 이 들어왔을때, 1111에 대해서 (11 , 11) 인지, (111, 1) 인지 구분이 필요.
		- 9600 이 보통 많이 씀. 너무 크면 불안정해짐
	2. 데이터 길이 
		- 8,7,6,5,3 등 설정할 수 있는데, 해당 길이만큼 보내고, 정지비트를 보내게 된다. 
	3. 패리티 : N. E. O
		- 데이터를 보낼 때, 받는 측에서 데이터를 올바르게 받았는지를 확인하는 용도
		- 해당 패리티 비트에 대해서 다른 연산?을 하는 듯 하다.
		- 대부분 N (none: 안쓴다) 으로 쓴다. E (even: 짝수), O (odd: 홀수) 도 있다.
		- 이 부분도 맞춰줘야지 통신이 제대로 된다. 송수신 파트에서 다르면 통신 안됨
	4. 정지비트
		- 대부분 1로 쓰며, 데이터의 정지를 뜻함
  
## RS485의 이해 - part 2
----
- RS232 : 꾸지다. 외부의 영향(전파 etc)을 많이 받는다.
- RS422 : 아주 좋다, 전이중방식(데이터를 보냄과 동시에 받는다.)
	+ 현장에서는 잘 안쓰는데, 그 이유가 명확하지가 않다. 다만 선이 4가닥 필요한데 이게 비용적으로나 사용성으로나 떨어져서 그런게 아닐까(추측)
- RS485 : 좋다. 가장 많이 쓴다.
	+ 반이중(보낸다음에 잠깐 쉬었다가 받는 것) &rightarrow; 2가닥
- 멀티드롭 
	-  ( A ) : |  S-id  |   |    |    |    |    
	     |______________________________________
	                    (S-id)

## 마스터 슬레이브 존재의 이유, 드라이버란
----
1. 왜? 마스터와 슬레이브가 존재 해야 하는지?
	- 동시에 말하는 것을 방지하기 위함이다.
	- 모든 말은 마스터로부터 시작이다.
	- 슬레이브 너는 대답만해라. 
2. 가상 시리얼 포트 구성
	- 