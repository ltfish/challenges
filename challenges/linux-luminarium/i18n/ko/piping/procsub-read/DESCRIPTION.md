때로는 두 파일이 아니라 두 명령의 출력을 비교해야 할 때가 있습니다.
각 출력을 먼저 파일에 저장하는 방법을 떠올릴 수도 있습니다:

```console
hacker@dojo:~$ command1 > file1
hacker@dojo:~$ command2 > file2
hacker@dojo:~$ diff file1 file2
```

하지만 더 우아한 방법이 있습니다! 리눅스는 ["모든 것은 파일이다"](https://en.wikipedia.org/wiki/Everything_is_a_file)라는 철학을 따릅니다.
즉, 실행 중인 프로그램의 입력과 출력을 포함해 대부분의 자원에 파일처럼 접근할 수 있게 하려 합니다!
셸도 이 철학을 따라서, 앞의 몇 레벨에서 배운 것처럼 커맨드 라인에서 파일 인자를 받는 유틸리티를 프로그램의 출력에 연결할 수 있게 해 줍니다.

흥미롭게도 여기서 더 나아가, 프로그램의 입력과 출력을 명령의 _인자_ 에 연결할 수도 있습니다.
이것은 [프로세스 치환(Process Substitution)](https://www.gnu.org/software/bash/manual/html_node/Process-Substitution.html)으로 합니다.
명령에서 읽어올 때(입력 프로세스 치환)는 `<(command)`를 씁니다.
`<(command)`라고 쓰면 bash가 그 명령을 실행하고 출력을 자기가 만든 임시 파일에 연결합니다.
물론 _진짜_ 파일은 아니고, 파일 이름을 가진 _이름 있는 파이프_ 라고 부르는 것입니다:

```console
hacker@dojo:~$ echo <(echo hi)
/dev/fd/63
hacker@dojo:~$
```

`/dev/fd/63`은 어디서 나왔을까요?
`bash`가 `<(echo hi)`를 그 명령의 출력에 연결된 이름 있는 파이프 파일의 경로로 바꿔치기한 것입니다!
그 명령이 실행되는 동안, 이 파일을 읽으면 그 명령의 표준 출력에서 데이터를 읽게 됩니다.
보통은 입력 파일을 인자로 받는 명령에 이렇게 씁니다:

```console
hacker@dojo:~$ cat <(echo hi)
hi
hacker@dojo:~$
```

물론 여러 번 쓸 수도 있습니다:

```console
hacker@dojo:~$ echo <(echo pwn) <(echo college)
/dev/fd/63 /dev/fd/64
hacker@dojo:~$ cat <(echo pwn) <(echo college)
pwn
college
hacker@dojo:~$
```

이제 여러분의 챌린지입니다!
[명령어 이해하기](/linux-luminarium/commands)의 `diff` 챌린지에서 배운 것을 떠올려 보세요.
그 챌린지에서는 두 파일을 diff했습니다.
이번에는 두 명령의 출력을 diff합니다. `/challenge/print_decoys`는 가짜 플래그를 잔뜩 출력하고, `/challenge/print_decoys_and_flag`는 그 가짜들에 진짜 플래그를 더해 출력합니다.

프로세스 치환과 `diff`로 두 프로그램의 출력을 비교해서 플래그를 찾으세요!
