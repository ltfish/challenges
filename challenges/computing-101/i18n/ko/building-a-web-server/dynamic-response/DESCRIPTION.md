이 챌린지에서 여러분의 서버는 HTTP GET 요청에 따라 동적인 내용을 다루도록 발전합니다.
먼저 [read](https://man7.org/linux/man-pages/man2/read.2.html) 시스템 콜로 클라이언트 소켓에서 들어오는 HTTP 요청을 받습니다.
요청 줄, 특히 여기서는 URL 경로를 살펴보면 클라이언트가 무엇을 원하는지 알 수 있습니다.
그다음 [open](https://man7.org/linux/man-pages/man2/open.2.html) 시스템 콜로 요청된 파일을 열고 [read](https://man7.org/linux/man-pages/man2/read.2.html)로 그 내용을 읽습니다.
[write](https://man7.org/linux/man-pages/man2/write.2.html) 시스템 콜로 그 파일 내용을 클라이언트에 돌려보냅니다.
서버가 단순히 고정된 메시지를 되풀이하는 대신 출력을 맞춰 내놓기 시작하므로, 이는 상호작용을 향한 중요한 진전입니다.
