# 7.2 TCP server 예제

TCP server 예제 프로그램을 문자열과 바이너리 송수신 방식으로 나누어 설명합니다.

TCP client가 `connect()` 함수로 server에 접속하는 반면, TCP server는 `listen()` 함수를 수행한 후, `accept()` 함수로 client의 connect를 기다립니다.  

* 동시에 1개의 client 접속만 허용합니다.
* remote port는 지정할 필요 없습니다.

나머지 동작들은 client와 동일합니다.
