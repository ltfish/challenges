리눅스를 쓰다 보면 출력이 아주 많은 프로그램에서 앞부분만 가져와야 하는 상황을 만나게 됩니다.
그럴 때 손이 가는 것이 `head`입니다!
`head` 명령어는 입력의 처음 몇 줄을 보여줍니다:

```console
hacker@dojo:~$ cat /something/very/long | head
this
is
just
the
first
ten
lines
of
the
file
hacker@dojo:~$
```

기본적으로 처음 10줄을 보여주지만, `-n` 옵션으로 조절할 수 있습니다:

```console
hacker@dojo:~$ cat /something/very/long | head -n 2
this
is
hacker@dojo:~$
```

이 챌린지의 `/challenge/pwn`은 데이터를 잔뜩 출력하는데, 그것을 `head`로 파이프해서 처음 7줄만 가져온 다음 `/challenge/college`로 이어서 파이프해야 합니다. 제대로 하면 플래그를 줍니다!
풀이는 파이프 _두 개_ 로 명령 셋을 이은 긴 복합 명령이 될 것입니다.
행운을 빕니다!
