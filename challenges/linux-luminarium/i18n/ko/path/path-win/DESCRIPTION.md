`PATH`를 비워버리면 문제가 생긴다는 것을 알았습니다.
그렇다면 `PATH`로 _쓸모 있는_ 일을 하는 것은 어떨까요?

예를 들어 프로그램이 담긴 새 디렉터리를 우리 명령 목록에 더하려면 어떻게 하는지 살펴봅시다.
`PATH`가 명령을 찾을 디렉터리 목록을 담고 있다는 것과, 표준적이지 않은 곳에 있는 명령은 보통 경로로 실행해야 한다는 것을 떠올려 보세요:

```console
hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ goodscript
bash: goodscript: command not found
hacker@dojo:~$ /home/hacker/scripts/goodscript
YEAH! This is the best script!
hacker@dojo:~$
```

이름만으로 실행하고 싶은 유용한 스크립트를 여럿 관리한다면 이것은 성가신 일입니다.
하지만 이 목록에 디렉터리를 추가하거나 목록의 디렉터리를 바꾸면, 그 프로그램들을 이름만으로 실행할 수 있게 만들 수 있습니다!
예를 들면:

```console
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
```

연습해 봅시다.
이 레벨의 `/challenge/run`은 `win` 명령을 이름만으로 실행하는데, 이 명령은 처음에는 PATH에 없는 `/challenge/more_commands/` 디렉터리에 있습니다.
`/challenge/run`에 필요한 것은 `win` _뿐_ 이므로, `PATH`를 그 디렉터리 하나로 덮어써도 됩니다.
행운을 빕니다!
