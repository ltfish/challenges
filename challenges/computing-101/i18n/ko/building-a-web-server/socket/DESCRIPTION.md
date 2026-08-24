이 챌린지에서는 [socket](https://man7.org/linux/man-pages/man2/socket.2.html) 시스템 콜로 소켓을 만들며 네트워킹 여정을 시작합니다.
소켓은 네트워크 통신의 기본 구성 요소이며, 데이터를 주고받는 종단점 역할을 합니다.
[socket](https://man7.org/linux/man-pages/man2/socket.2.html)을 호출할 때는 세 가지 핵심 인자를 줍니다. 도메인(예: IPv4를 뜻하는 `AF_INET`), 종류(예: TCP를 뜻하는 `SOCK_STREAM`), 그리고 프로토콜(보통 기본값을 고르려고 `0`)입니다.
이 시스템 콜을 익히는 것은 이후의 모든 네트워크 상호작용의 토대가 되므로 중요합니다.

----
**참고:**
문서를 보면 시스템 콜의 인자가 전부 대문자 이름으로 적혀 있습니다.
예를 들어 `socket(AF_INET, SOCK_STREAM, 0)`을 호출하고 싶더라도 그냥 `mov rdi, AF_INET`이라고 쓸 수는 없습니다. 어셈블리 수준에는 `AF_INET`이라는 개념이 아예 없으니까요.
`AF_INET`에 해당하는 정수를 찾아야 합니다.
이 숫자들은 man 페이지에도 없지만, 여러분의 머신에는 존재합니다.
`/usr/include` 디렉터리를 살펴보세요.
C 프로그래밍을 위한 시스템의 범용 include 파일이 전부 여기 있습니다. (C를 써봤다면 코드에 넣었던 `#include <stdio.h>` 같은 헤더 파일을 떠올려 보세요. 그 함수와 상수가 전부 여기 어딘가에 정의되어 있습니다.)
C는 어셈블리로 컴파일되므로 그 숫자들은 이 디렉터리 어딘가에 있습니다.
일일이 뒤지는 대신 [grep](https://pwn.college/linux-luminarium/commands/)으로 찾을 수 있습니다.
