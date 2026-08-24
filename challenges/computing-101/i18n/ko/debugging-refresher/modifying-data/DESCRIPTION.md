사실 gdb는 대상 프로세스를 완전히 통제합니다.
프로그램의 상태를 분석할 수 있을 뿐 아니라 바꿀 수도 있습니다.
gdb가 프로그램을 오래 유지보수하기에 가장 좋은 도구는 아니겠지만, 분석을 더 쉽게 하려고 대상 프로세스의 동작을 빠르게 바꾸는 데는 유용할 때가 있습니다.

`set` 명령으로 대상 프로그램의 상태를 바꿀 수 있습니다.
예를 들어 `set $rdi = 0`으로 $rdi를 0으로 만들 수 있습니다.
`set *((uint64_t *) $rsp) = 0x1234`로 스택의 첫 값을 0x1234로 설정할 수 있습니다.
`set *((uint16_t *) 0x31337000) = 0x1337`로 0x31337000의 2바이트를 0x1337로 설정할 수 있습니다.

대상이 fd 42의 어떤 소켓에서 읽는 네트워크 애플리케이션이라고 해봅시다.
분석하기에는 대상이 대신 stdin에서 읽는 편이 더 쉬울 수 있습니다.
다음 gdb 스크립트로 그런 것을 해낼 수 있습니다:

```gdb
start
catch syscall read
commands
  silent
  if ($rdi == 42)
    set $rdi = 0
  end
  continue
end
continue
```

이 예시 gdb 스크립트는 시스템 콜에서 자동으로 멈추는 법과, 명령 안에서 조건을 써서 gdb 명령을 조건부로 수행하는 법을 보여줍니다.

앞 레벨에서 여러분의 gdb 스크립팅 풀이는 아마 여전히 답을 복사해 붙여넣어야 했을 것입니다.
이번에는 프로그램과 전혀 대화하지 않고, 레지스터와 메모리를 알맞게 바꿔서 각 문제를 자동으로 푸는 스크립트를 작성해 보세요.

----
**관련 문서:**
- gdb의 [run](https://sourceware.org/gdb/current/onlinedocs/gdb#Starting) 명령
- gdb의 [continue](https://sourceware.org/gdb/current/onlinedocs/gdb#Continuing-and-Stepping) 명령
- gdb의 [info](https://sourceware.org/gdb/current/onlinedocs/gdb#Registers) 명령
- gdb의 [print](https://sourceware.org/gdb/current/onlinedocs/gdb#Data) 명령
- gdb의 [examine](https://sourceware.org/gdb/current/onlinedocs/gdb#Memory) 명령
- gdb의 [break](https://sourceware.org/gdb/current/onlinedocs/gdb#Set-Breaks) 명령
- gdb의 [display](https://sourceware.org/gdb/current/onlinedocs/gdb#Auto-Display) 명령
- gdb의 [여러 단계 실행 명령](https://sourceware.org/gdb/current/onlinedocs/gdb#Continuing-and-Stepping)(그 절 전체)
- gdb의 [중단점 스크립팅](https://sourceware.org/gdb/current/onlinedocs/gdb#Break-Commands)
- gdb의 [set](https://sourceware.org/gdb/current/onlinedocs/gdb#Assignment) 명령. 이 챌린지에서는 특히 이 명령으로 레지스터(위의 `$rdi` 등)와 메모리(링크된 절의 아래쪽에 설명되어 있습니다)를 설정하게 된다는 점을 기억하세요.
