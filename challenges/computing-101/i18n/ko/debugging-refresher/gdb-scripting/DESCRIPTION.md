우리는 재현하고 다듬을 수 있는 아이디어를 표현하려고 코드를 작성합니다.
우리의 분석을, 분석 대상을 데이터로 삼아 먹어치우는 프로그램이라고 생각할 수 있습니다.
흔히 말하듯 코드는 데이터이고 데이터는 코드입니다.

앞 레벨들처럼 gdb를 대화형으로 쓰는 것도 대단히 강력하지만, 또 하나의 강력한 도구가 gdb 스크립팅입니다.
gdb를 스크립트로 제어하면 목적에 딱 맞는 프로그램 분석 도구를 아주 빠르게 만들 수 있습니다.
gdb와 상호작용하는 법을 안다면 gdb 스크립트를 쓰는 법도 이미 아는 셈입니다. 문법이 완전히 같으니까요.
명령을 예를 들어 `x.gdb` 같은 파일에 쓰고, `-x <PATH_TO_SCRIPT>` 플래그로 gdb를 띄우면 됩니다.
그러면 gdb가 시작된 뒤 그 파일의 모든 gdb 명령이 실행됩니다.
아니면 `-ex '<COMMAND>'`로 명령을 하나씩 실행할 수도 있습니다.
`-ex` 인자를 여러 개 주어 명령을 여러 개 넘길 수도 있습니다.
마지막으로, `~/.gdbinit`에 넣어두면 어떤 gdb 세션에서든 항상 실행되게 할 수 있습니다.
거기에 `set disassembly-flavor intel`을 넣어두면 좋습니다.

gdb 스크립팅에서 아주 강력한 구성 요소는 중단점 명령입니다. 다음 gdb 스크립트를 봅시다:

```gdb
start
break *main+42
commands
  x/gx $rbp-0x32
  continue
end
continue
```

이 경우 `main+42`의 명령어에 걸릴 때마다 특정 지역 변수를 출력하고 실행을 이어갑니다.

이제 비슷하지만 아직 보지 않은 명령을 쓰는 조금 더 발전된 스크립트를 봅시다:

```gdb
start
break *main+42
commands
  silent
  set $local_variable = *(unsigned long long*)($rbp-0x32)
  printf "Current value: %llx\n", $local_variable
  continue
end
continue
```

여기서 `silent`는 출력을 좀 더 깔끔하게 하려고 중단점에 걸렸다는 사실을 gdb가 알리지 않게 합니다.
그다음 `set` 명령으로 gdb 세션 안에 변수를 정의하는데, 그 값은 우리의 지역 변수입니다.
마지막으로 서식 문자열로 현재 값을 출력합니다.

이 레벨에서 무작위 값을 모으는 데 gdb 스크립팅을 활용하세요.
어렵게 느껴질 수 있지만, 앞으로의 여정에서 큰 도움이 될 것입니다.

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
