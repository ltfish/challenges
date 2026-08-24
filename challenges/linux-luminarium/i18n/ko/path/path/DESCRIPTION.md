"셸은 `ls`를 어떻게 찾을까?"에 대한 답은 꽤 간단합니다.
`PATH`라는 특별한 셸 변수가 있는데, 셸이 명령에 해당하는 프로그램을 찾을 디렉터리 경로들을 담고 있습니다.
이 변수를 비워버리면 상황이 나빠집니다:

```console
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ PATH=""
hacker@dojo:~$ ls
bash: ls: No such file or directory
hacker@dojo:~$
```

PATH가 없으면 bash는 `ls` 명령을 찾지 못합니다.

이 레벨에서는 `/challenge/run` 프로그램의 동작을 방해하게 됩니다.
이 프로그램은 `rm` 명령으로 플래그 파일을 **삭제** 합니다.
하지만 `rm` 명령을 찾지 못하면 플래그는 삭제되지 않고, 챌린지가 그것을 여러분에게 줍니다!
따라서 `/challenge/run`도 `rm` 명령을 찾지 못하게 만들어야 합니다!

기억하세요. 성공하지 못해서 플래그가 삭제되면, 다시 시도하려면 챌린지를 재시작해야 합니다!
