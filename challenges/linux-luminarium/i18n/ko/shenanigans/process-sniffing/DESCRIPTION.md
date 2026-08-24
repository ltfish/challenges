가엾은 Zardus. 여러분이 그를 꽤 심하게 해킹했군요.
그런데 그가 정신을 차리고 홈 디렉터리를 잠갔습니다!
이걸로 끝일까요?

그렇지 않습니다!
한 컴퓨터에 여러 계정이 있을 때 사람들이 흔히 생각하지 못하는 것 중 하나가, 자기 _명령 실행_ 이 어떤 데이터를 흘리는가입니다.
`ps aux`를 하면 이런 것이 나온다는 것을 떠올려 보세요:

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

그런데 저 명령들 중 하나의 인자가 플래그나 비밀번호처럼 민감한 것이었다면 어떨까요?
실제로 이런 일이 생기며, 같은 머신을 쓰는(또는 다른 방법으로 그 머신의 프로세스를 볼 수 있는) 악의적인 사용자가 그 데이터를 훔쳐 쓸 수 있습니다!

이 챌린지가 살펴보는 것이 바로 그것입니다.
Zardus는 자동화 스크립트에 자기 계정 비밀번호를 인자로 넘겨 쓰고 있습니다.
Zardus는 `sudo`도 쓸 수 있습니다(따라서 `sudo cat /flag`도 가능하죠!).
비밀번호를 훔쳐 Zardus의 계정으로 로그인하고([사용자 풀어헤치기](/linux-luminarium/users) 모듈의 `su` 명령을 떠올려 보세요) 플래그를 얻으세요!
