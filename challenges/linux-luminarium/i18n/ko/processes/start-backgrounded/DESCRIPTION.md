물론 백그라운드로 보내려고 꼭 일시 중단해야 하는 것은 아닙니다. 처음부터 백그라운드로 시작할 수도 있습니다!
간단합니다. 명령 뒤에 `&`를 붙이기만 하면 됩니다:

```console
hacker@dojo:~$ sleep 1337 &
[1] 1771
hacker@dojo:~$ ps -o user,pid,stat,cmd
USER         PID STAT CMD
hacker      1709 Ss   bash
hacker      1771 S    sleep 1337
hacker      1782 R+   ps -o user,pid,stat,cmd
hacker@dojo:~$ 
```

여기서 `sleep`은 일시 중단된 것이 _아니라_ 백그라운드에서 활발히 실행 중입니다.
이제 여러분이 연습할 차례입니다!
`/challenge/run`을 백그라운드로 실행해서 플래그를 얻으세요!
