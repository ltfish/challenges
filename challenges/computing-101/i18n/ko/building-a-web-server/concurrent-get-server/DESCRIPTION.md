서버가 여러 클라이언트를 동시에 처리할 수 있도록 [fork](https://man7.org/linux/man-pages/man2/fork.2.html) 시스템 콜로 동시성을 도입합니다.
클라이언트가 접속하면 [fork](https://man7.org/linux/man-pages/man2/fork.2.html)가 그 연결을 전담할 자식 프로세스를 만듭니다.
그동안 부모 프로세스는 곧바로 돌아가 추가 연결을 받아들입니다.
이 설계에서 자식은 [read](https://man7.org/linux/man-pages/man2/read.2.html)와 [write](https://man7.org/linux/man-pages/man2/write.2.html)로 클라이언트와 주고받고, 부모는 계속 대기합니다.
이 동시 처리 모델은 확장 가능한 실전 서버를 만드는 데 핵심 개념입니다.
