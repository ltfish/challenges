다음으로 레지스터 값을 출력하는 법을 배웁니다.

`info registers`로 모든 레지스터의 값을 볼 수 있습니다. 아니면 `print` 명령(줄여서 `p`)으로 특정
레지스터의 값만 출력할 수도 있습니다. 예를 들어 `p $rdi`는 $rdi의 값을 10진수로 출력합니다. `p/x $rdi`로
16진수로도 출력할 수 있습니다.

이 레벨을 풀려면 레지스터 r12의 현재 무작위 값을 16진수로 알아내야 합니다.

앞서와 마찬가지로 챌린지를 시작하고 `run` gdb 명령을 실행한 뒤 안내를 따르세요.
필요한 것을 출력했으면 `continue`로 챌린지의 다음 단계로 넘어가는 것을 잊지 마세요!

----
**관련 문서:**
- gdb의 [run](https://sourceware.org/gdb/current/onlinedocs/gdb#Starting) 명령
- gdb의 [continue](https://sourceware.org/gdb/current/onlinedocs/gdb#Continuing-and-Stepping) 명령
- gdb의 [info](https://sourceware.org/gdb/current/onlinedocs/gdb#Registers) 명령
- gdb의 [print](https://sourceware.org/gdb/current/onlinedocs/gdb#Data) 명령
