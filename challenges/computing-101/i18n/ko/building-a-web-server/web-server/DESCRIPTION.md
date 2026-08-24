마지막 챌린지에서 여러분의 서버는 하나의 프로그램 안에서 GET과 POST 요청을 모두 매끄럽게 지원해야 합니다.
[read](https://man7.org/linux/man-pages/man2/read.2.html)로 들어온 요청을 읽은 뒤, 서버는 처음 몇 글자를 살펴 GET인지 POST인지 판단합니다.
요청 종류에 따라 데이터를 알맞게 처리하고, [write](https://man7.org/linux/man-pages/man2/write.2.html)로 적절한 응답을 돌려보냅니다.
이 과정 내내 [fork](https://man7.org/linux/man-pages/man2/fork.2.html)로 각 연결을 동시에 처리해서, 서버가 여러 요청을 한꺼번에 감당할 수 있게 합니다.
이것을 마치면 여러 종류의 HTTP 요청을 처리할 수 있는, 단순하지만 온전히 동작하는 웹 서버를 만든 것입니다.
