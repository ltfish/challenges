screen으로 탐정 놀이를 할 시간입니다!

screen을 즐겨 쓰다 보면 언젠가는 세션이 여러 개 돌아가게 됩니다.
어느 것에 다시 붙어야 할지 어떻게 찾을까요?

목록을 볼 수 있습니다:

```console
hacker@dojo:~$ screen -ls
There are screens on:
        23847.mysession   (Detached)
        23851.goodwork    (Detached)
        23855.morework    (Detached)
3 Sockets in /run/screen/S-hacker.
```

세션의 식별자는 각 screen 프로세스의 PID, 점, 그리고 세션 이름으로 이루어집니다.
특정 세션에 붙으려면 그 이름이나 PID를 `screen -r`의 인자로 주면 됩니다.

```console
hacker@dojo:~$ screen -r goodwork
```

이 챌린지에서는 screen 세션을 세 개 만들어 두었습니다.
그중 하나에 플래그가 있습니다.
나머지 둘은 가짜입니다!

찾을 때까지 하나씩 확인해야 합니다.
다음 세션을 보기 전에 분리(Ctrl-A d)하는 것을 잊지 마세요!
