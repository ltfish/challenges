`fg` 명령으로 프로세스를 _포그라운드_ 에서 재개해 봤습니다.
`bg` 명령으로 프로세스를 _백그라운드_ 에서 재개할 수도 있습니다!
이렇게 하면 프로세스는 계속 실행되면서, 그동안 여러분은 셸을 되돌려받아 다른 명령을 실행할 수 있습니다.

이 레벨의 `run`은 자기 자신의 또 다른 사본이 _일시 중단되지 않은 채_ 같은 터미널을 쓰며 실행되고 있기를 바랍니다.
어떻게 할까요?
터미널에서 실행한 뒤 일시 중단하고, `bg`로 _백그라운드로_ 보낸 다음, 첫 번째 것이 백그라운드에서 돌아가는 동안 또 하나를 실행하세요!

---

**비밀 이야기:**
좀 더 깊은 내용이 궁금하다면, 일시 중단된 상태와 백그라운드 상태의 차이를 어떻게 확인하는지 살펴보세요!
직접 보여드리겠습니다.
먼저 `sleep`을 일시 중단해 봅시다:

```console
hacker@dojo:~$ sleep 1337
^Z
[1]+  Stopped                 sleep 1337
hacker@dojo:~$
```

이제 `sleep` 프로세스는 백그라운드에서 _일시 중단_ 되어 있습니다.
`-o` 옵션으로 `stat` 열을 출력하게 하면 `ps`로 이를 확인할 수 있습니다:

```console
hacker@dojo:~$ ps -o user,pid,stat,cmd
USER         PID STAT CMD
hacker       702 Ss   bash
hacker       762 T    sleep 1337
hacker       782 R+   ps -o user,pid,stat,cmd
hacker@dojo:~$ 
```

저 `T`가 보이나요?
우리가 누른 `Ctrl-Z` 때문에 프로세스가 일시 중단되었다는 뜻입니다.
`bash`의 `STAT` 열에 있는 `S`는 `bash`가 입력을 기다리며 자고 있다는 뜻입니다.
`ps`의 열에 있는 `R`은 활발히 실행 중이라는 뜻이고, `+`는 포그라운드에 있다는 뜻입니다!

`sleep`을 백그라운드에서 재개하면 어떻게 되는지 보세요:

```console
hacker@dojo:~$ bg
[1]+ sleep 1337 &
hacker@dojo:~$ ps -o user,pid,stat,cmd
USER         PID STAT CMD
hacker       702 Ss   bash
hacker       762 S    sleep 1337
hacker      1224 R+   ps -o user,pid,stat,cmd
hacker@dojo:~$
```

짠!
이제 `sleep`에 `S`가 붙었습니다.
자는 중이라 자고 있는 것이지, 일시 중단된 것은 아닙니다!
또한 _백그라운드_ 에 있으므로 `+`가 없습니다.
