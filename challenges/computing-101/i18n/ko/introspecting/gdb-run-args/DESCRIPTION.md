앞 레벨에서 gdb의 `run` 명령을 처음 써봤습니다. `run`은 프로그램을 시작해 자유롭게 실행되게 합니다.
그런데 프로그램이 동작하려면 _커맨드 라인 인자가 필요하다면_ 어떨까요?

gdb 밖에서는 프로그램 이름 뒤에 인자를 그냥 적어서 넘겨왔습니다:

```console
hacker@dojo:~$ /challenge/debug-me hello
```

gdb 안에서 이에 대응하는 것은 `run`에 인자를 넘기는 것입니다:

```text
(gdb) run hello
```

`run` 뒤에 적은 것이 무엇이든 대상 프로그램의 `argv[1]`, `argv[2]` 등이 됩니다. 셸 커맨드 라인에 그 인자를 입력한 것과 똑같죠.
GDB는 짧은 형태인 `r`도 받습니다:

```text
(gdb) r hello
```

(gdb 문서에서 `run`이 보이는 곳에서는 `r`도 동작합니다.)

이 챌린지에서 `/challenge/debug-me`는 `argv[1]`로 문자열 `pwn`을 줄 때에만 플래그를 출력합니다.
해보세요!
