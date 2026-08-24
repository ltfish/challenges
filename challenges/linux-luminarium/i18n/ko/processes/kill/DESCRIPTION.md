프로세스를 실행해 봤고, 살펴봤으니, 이제 프로세스를 _종료_ 하는 법을 배울 차례입니다!
리눅스에서는 무시무시한 이름의 `kill` 명령어로 합니다.
기본 옵션(이 레벨에서 다룰 전부입니다)으로 `kill`은 프로세스가 사라지기 전에 마무리를 지을 기회를 주는 방식으로 종료시킵니다.

다른 터미널에서 성가신 `sleep` 프로세스를 띄웠다고 해봅시다(`sleep`은 커맨드 라인에 지정한 초만큼 그냥 기다리는 프로그램이며, 여기서는 1337초입니다):

```console
hacker@dojo:~$ sleep 1337
```

어떻게 없앨까요?
프로세스 식별자(`ps`에 나오는 `PID`)를 인자로 주어 `kill`로 종료합니다:

```console
hacker@dojo:~$ ps -e | grep sleep
 342 pts/0    00:00:00 sleep
hacker@dojo:~$ kill 342
hacker@dojo:~$ ps -e | grep sleep
hacker@dojo:~$
```

이제 여러분의 첫 프로세스를 종료할 시간입니다!
이 챌린지에서 `/challenge/run`은 `/challenge/dont_run`이 실행 중인 동안에는 실행을 거부합니다!
`dont_run` 프로세스를 찾아 `kill`해야 합니다.
실패하면 `pwn.college`는 여러분의 임무에 대해 아는 바 없다고 잡아뗄 것입니다.
행운을 빕니다.
