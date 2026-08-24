먼저 `ps` 명령어로 실행 중인 프로세스를 나열하는 법을 배웁니다.
누구에게 묻느냐에 따라 `ps`는 "process snapshot"이기도 하고 "process status"이기도 하며, 프로세스를 나열합니다.
기본적으로 `ps`는 여러분의 터미널에서 실행 중인 프로세스만 나열하는데, 솔직히 그리 유용하지는 않습니다:

```console
hacker@dojo:~$ ps
    PID TTY          TIME CMD
    329 pts/0    00:00:00 bash
    349 pts/0    00:00:00 ps
hacker@dojo:~$
```

위 예시에는 셸(`bash`)과 `ps` 프로세스 자신이 있고, 그 터미널에서 실행 중인 것은 그게 전부입니다.
또한 각 프로세스에 숫자 식별자(_프로세스 ID_, 즉 PID)가 있는 것도 보입니다. 리눅스 환경에서 실행 중인 모든 프로세스를 고유하게 식별하는 번호입니다.
명령이 실행 중인 터미널(여기서는 `pts/0`)과, 그 프로세스가 지금까지 쓴 총 _CPU 시간_ 도 보입니다(이 프로세스들은 부담이 적어서 아직 1초도 쓰지 못했습니다!).

대부분의 경우 기본 `ps`로 볼 수 있는 것은 이게 전부입니다.
쓸모 있게 만들려면 인자를 몇 개 넘겨야 합니다.

`ps`는 아주 오래된 유틸리티라서 사용법이 좀 뒤죽박죽입니다.
인자를 지정하는 방식이 두 가지 있습니다.

**"표준" 문법:** 이 문법에서는 "모든(every)" 프로세스를 나열하는 `-e`와 인자까지 포함한 "전체 형식(full format)" 출력을 위한 `-f`를 쓸 수 있습니다.
이 둘은 `-ef`라는 하나의 인자로 합칠 수 있습니다.

**"BSD" 문법:** 이 문법에서는 모든 사용자의 프로세스를 나열하는 `a`, 터미널에서 실행 중이 아닌 프로세스까지 나열하는 `x`, "사용자가 읽기 좋은" 출력을 위한 `u`를 쓸 수 있습니다.
이 셋은 `aux`라는 하나의 인자로 합칠 수 있습니다.

이 두 방식 `ps -ef`와 `ps aux`는 조금 다르지만 서로 알아볼 수 있는 출력을 냅니다.

도장에서 해봅시다:

```console
hacker@dojo:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
hacker         1       0  0 05:34 ?        00:00:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7       1  0 05:34 ?        00:00:00 /bin/sleep 6h
hacker       102       1  1 05:34 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server --auth=none -
hacker       138     102 11 05:34 ?        00:00:07 /usr/lib/code-server/lib/node /usr/lib/code-server/out/node/entr
hacker       287     138  0 05:34 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server/lib/vscode/ou
hacker       318     138  6 05:34 ?        00:00:03 /usr/lib/code-server/lib/node --dns-result-order=ipv4first /usr/
hacker       554     138  3 05:35 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server/lib/vscode/ou
hacker       571     554  0 05:35 pts/0    00:00:00 /usr/bin/bash --init-file /usr/lib/code-server/lib/vscode/out/vs
hacker       695     571  0 05:35 pts/0    00:00:00 ps -ef
hacker@dojo:~$
```

여기 보이는 것은 챌린지 환경 초기화 프로세스(`docker-init`), 컴퓨팅 자원을 아끼려고 챌린지를 자동 종료하기까지의 타임아웃(6시간 뒤 종료하는 `sleep 6h`), VSCode 환경(여러 `code-server` 보조 프로세스), 셸(`bash`), 그리고 제가 실행한 `ps -ef` 명령입니다.
`ps aux`도 기본적으로 같습니다:

```
hacker@dojo:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
hacker         1  0.0  0.0   1128     4 ?        Ss   05:34   0:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7  0.0  0.0   2736   580 ?        S    05:34   0:00 /bin/sleep 6h
hacker       102  0.4  0.0 723944 64660 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       138  3.3  0.0 968792 106272 ?       Sl   05:34   0:07 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       287  0.0  0.0 717648 53136 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       318  3.3  0.0 977472 98256 ?        Sl   05:34   0:06 /usr/lib/code-server/lib/node --dns-result-order=
hacker       554  0.4  0.0 650560 55360 ?        Rl   05:35   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       571  0.0  0.0   4600  4032 pts/0    Ss   05:35   0:00 /usr/bin/bash --init-file /usr/lib/code-server/li
hacker      1172  0.0  0.0   5892  2924 pts/0    R+   05:38   0:00 ps aux
hacker@dojo:~$
```

`ps -ef`와 `ps aux`에는 공통점이 많습니다. 둘 다 사용자(`USER` 열), PID, TTY, 프로세스 시작 시각(`STIME`/`START`), 사용한 총 CPU 시간(`TIME`), 명령(`CMD`/`COMMAND`)을 보여줍니다.
`ps -ef`는 추가로 _부모 프로세스 ID_ (`PPID`), 즉 해당 프로세스를 띄운 프로세스의 PID를 출력하고, `ps aux`는 그 프로세스가 쓰고 있는 시스템 전체 CPU와 메모리의 비율을 출력합니다.
그 밖에도 지금은 다루지 않을 것들이 여럿 있습니다.

아무튼 연습해 봅시다!
이 레벨에서도 `/challenge/run`의 이름을 무작위로 바꿔 놓았고, 이번에는 `/challenge` 디렉터리를 `ls`할 수도 없게 만들었습니다!
하지만 그것을 실행해 두었으니, 실행 중인 프로세스 목록에서 찾아 파일 이름을 알아낸 뒤 직접 다시 실행해서 플래그를 얻으세요!
행운을 빕니다!

**참고:** `ps -ef`와 `ps aux`는 둘 다 명령 표시를 터미널 너비에 맞게 잘라냅니다(그래서 위 예시들이 오른쪽에서 딱 떨어져 보이는 것입니다).
프로세스의 전체 경로를 읽을 수 없다면 터미널을 넓히거나, 잘림을 피하려고 출력을 어딘가로 리다이렉트해야 할 수도 있습니다!
아니면 `w` 옵션을 _두 번_ 주면(예: `ps -efww`나 `ps auxww`) 잘라내기를 끌 수 있습니다.
