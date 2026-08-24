서버의 능력을 한층 넓혀, 이 챌린지에서는 HTTP POST 요청을 동시에 처리하는 데 집중합니다.
POST 요청은 헤더와 메시지 본문을 모두 포함하므로 더 복잡합니다.
다시 [fork](https://man7.org/linux/man-pages/man2/fork.2.html)로 여러 연결을 관리하면서, [read](https://man7.org/linux/man-pages/man2/read.2.html)로 요청 전체를 받습니다.
역시 URL 경로를 파싱해 지정된 파일을 알아내지만, 이번에는 그 파일에서 읽는 대신 들어온 POST 데이터를 그 파일에 씁니다.
그러려면 들어온 POST 데이터의 길이를 알아내야 합니다.
*뻔한* 방법은 바로 그 길이를 지정하는 `Content-Length` 헤더를 파싱하는 것입니다.
아니면 [read](https://man7.org/linux/man-pages/man2/read.2.html)의 반환값으로 요청 전체 길이를 구하고, 요청을 파싱해 (`\r\n\r\n`으로 끝나는) 헤더 전체 길이를 구한 뒤, 그 차이로 본문 길이를 정하는 방법도 있습니다. 겉보기에 더 복잡한 이 알고리즘이 오히려 구현하기 쉬울 수 있습니다.
마지막으로 POST 요청이 성공했음을 알리는 `200 OK` 응답만 클라이언트에 돌려주세요.
