앞 레벨들에서 비밀은 프로그램의 코드 안(하드코딩된 `mov` 명령어)에 숨어 있었습니다.
이번에 비밀은 프로그램의 *실행 중 상태* 에서 나옵니다. 바로 스택에 있는 인자 개수(`argc`)입니다.

프로그램은 `pop rdi`로 이 값을 스택에서 꺼내지만, 종료하기 전에 곧바로 `rdi`를 0으로 덮어씁니다:

```text
pop    rdi          <- reads argc from the stack into rdi
mov    rdi,0x0      <- overwrites rdi with 0!
mov    rax,0x3c
syscall             <- exit(0) --- the secret is gone!
```

코드는 전부 보이고 검열된 것도 없지만, `argc`는 프로그램이 몇 개의 인자로 실행되었는지에 달려 있으므로 디스어셈블리를 읽는 것만으로는 비밀을 알 수 없습니다.
이 레벨에서는 GDB가 그것을 처리해 주지만, 나중에는 gdb에서 프로그램의 인자를 설정하는 법도 알려드리겠습니다!

지금은 다음을 해야 합니다:
1. 프로그램을 시작합니다.
2. 명령어 하나를 진행해 `pop rdi`만 실행합니다
3. 덮어써지기 전에 `rdi`에 들어온 값을 `print`합니다
4. gdb를 종료하고 그 값을 `/challenge/submit-number`로 제출합니다.
