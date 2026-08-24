소켓을 만들었으면 다음 단계는 그 소켓에 네트워크 정체성을 부여하는 것입니다.
이 챌린지에서는 [bind](https://man7.org/linux/man-pages/man2/bind.2.html) 시스템 콜로 소켓을 특정 IP 주소와 포트 번호에 연결합니다.
이 호출은 소켓 파일 디스크립터, `struct sockaddr`의 포인터, 그리고 그 구조체의 크기를 요구합니다.
[엔디언 대모험](/computing-101/endian-escapades)에서 x86이 여러 바이트 값을 메모리에 리틀 엔디언으로 저장하며, 네트워크 프로토콜처럼 CPU 바깥의 맥락에서는 다른 바이트 순서를 쓸 수 있다는 것을 보았습니다.
IP 소켓 구조체에서 여러 바이트 숫자는 빅 엔디언 순서를 씁니다. 가장 높은 자리 바이트가 먼저 오죠.
이 관례를 **네트워크 바이트 순서(network byte order)** 라고 부릅니다.
16비트 포트 번호라면 포트 `80`(`0x0050`)은 바이트 `00 50`으로 표현됩니다.
IPv4에서는 구조체가 `struct sockaddr_in`이며, `bind`는 그 포인터의 16바이트를 다음 필드로 읽습니다:

```text
bytes 0..1    address family, `AF_INET` (`2`)
bytes 2..3    port, in network byte order (`00 50` for port 80)
bytes 4..7    address (`0.0.0.0` is four zero bytes)
bytes 8..15   padding
```

[RIP로 플래그 열기](/computing-101/hello-hackers/open-read-write-rip-relative)에서는 저장된 바이트를 쓰고 그 주소를 시스템 콜에 넘겼습니다.
여기서는 `sockaddr_in` 바이트를 스택에 만들고, 스택 주소를 포인터로 넘기고, 크기로 `16`을 넘기세요.
64비트 x86에서 워드 값 `0x5000`을 쓰면 바이트 `00 50`이 저장되며, 이는 네트워크 바이트 순서의 포트 `80`입니다.
바인딩은 서버가 알려진 주소에서 대기하도록 보장해 클라이언트가 찾아올 수 있게 하므로 필수적입니다.
