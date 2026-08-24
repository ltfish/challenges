동적 분석에서 결정적으로 중요한 부분은, 분석하고 싶은 상태까지 프로그램을 진행시키는 것입니다.
지금까지 이 챌린지들은 여러분이 분석하고 싶어 할 만한 상태에서 실행이 멈추도록 중단점을 알아서 설정해 주었습니다.
그것을 직접 할 줄 아는 것이 중요합니다.

프로그램의 실행을 앞으로 나아가게 하는 방법은 여러 가지입니다.
`stepi <n>` 명령(줄여서 `si <n>`)으로 명령어 하나만큼 나아갈 수 있습니다.
`nexti <n>` 명령(줄여서 `ni <n>`)으로 함수 호출은 건너뛰면서 명령어 하나만큼 나아갈 수 있습니다.
`<n>` 인자는 선택 사항이지만, 여러 단계를 한 번에 진행할 수 있게 해 줍니다.
`finish` 명령으로 지금 실행 중인 함수를 끝까지 진행할 수 있습니다.
`break *<address>` 명령으로 지정한 주소에 중단점을 설정할 수 있습니다.
이미 써본 `continue` 명령은 프로그램이 중단점에 걸릴 때까지 실행을 이어갑니다.

프로그램을 단계별로 진행할 때 어떤 값들이 항상 보이면 유용할 수 있습니다.
방법은 여러 가지입니다.
가장 간단한 방법은 `display/<n><u><f>` 명령인데, `x/<n><u><f>` 명령과 형식이 완전히 같습니다.
예를 들어 `display/8i $rip`는 다음 8개 명령어를 항상 보여줍니다.
`display/4gx $rsp`는 스택의 처음 4개 값을 항상 보여줍니다.
또 다른 방법은 `layout regs` 명령입니다.
이것은 gdb를 TUI 모드로 바꿔 모든 레지스터의 내용과 근처 명령어를 보여줍니다.

이 레벨을 풀려면 스택에 놓일 일련의 무작위 값을 알아내야 합니다.
앞서처럼 `run`으로 시작하지만, 프로그램이 중간에 멈추므로 조심스럽게 실행을 이어가야 합니다.

`stepi`, `nexti`, `break`, `continue`, `finish`를 이리저리 조합해 보면서 이 명령들을 확실히 익히기를 강력히 권합니다.
이 명령들은 프로그램의 실행을 헤쳐 나가는 데 모두 절대적으로 중요합니다.

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

**참고:**
이 챌린지는 어셈블리를 _읽고_ _이해_ 해야 합니다!
걱정 마세요, 이 기술은 pwn.college 뒷부분에서 아주 유용하게 쓰입니다.
