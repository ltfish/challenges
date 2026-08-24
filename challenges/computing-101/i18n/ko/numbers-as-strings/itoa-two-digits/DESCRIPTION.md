한 자리는 쉬웠습니다.
`42` 같은 두 자리 수는 십의 자리(`4`)와 일의 자리(`2`)로 *쪼개야* 하는데, 쪼개기란 곧 나눗셈입니다. `42 / 10 = 4`(몫), `42 % 10 = 2`(나머지)죠.

x86은 `div` 하나로 *둘 다* 주지만, `div`는 까다로운 명령어라 잘 익혀둘 가치가 있습니다.
`div rcx`는 `rdx:rax`를 이어 붙여 만든 **128비트** 값을 `rcx`로 나누고, 몫은 `rax`에, 나머지는 `rdx`에 남깁니다.
여기서 세 가지가 따라옵니다:

- `rax`만이 아니라 `rdx:rax`를 나누므로, 먼저 `rdx`를 비워야 합니다(`xor rdx, rdx`). 그러지 않으면 `div`가 남아 있는 쓰레기 값을 여러분 수의 상위 절반으로 취급합니다(그리고 죽을 수도 있습니다).
- 제수는 즉시값이 아니라 레지스터에서 오므로, `10`을 레지스터에 넣으세요(예: `mov rcx, 10; div rcx`).
- 피제수는 여러분이 정할 수 없습니다. _언제나_ `rdx:rax`입니다.

`div` 뒤에는 `rax`에 십의 자리, `rdx`에 일의 자리가 들어 있습니다.
`itoa_digit`이 했던 대로 각각을 문자로 바꾸고(`0x30`을 더하고) 둘을 저장하세요.

챌린지에서 호출할 `itoa(value, buf)`를 작성하세요.
이 함수는 `rdi`로 값(`10`-`99`)을, `rsi`로 "출력" 버퍼의 포인터를 받습니다.
`div`로 `rdi`의 수를 쪼개고, 위와 같이 두 숫자를 변환해서 그 문자들을 버퍼에 쓰세요.
그런 다음 쓴 문자의 개수(여기서는 2)를 반환하세요.
`.global itoa`를 잊지 마세요.

**문자 쓰기.**
앞 레벨의 `itoa_digit` 함수는 결과를 (`rax`로) 반환했을 뿐, 그것을 버퍼에 쓸 필요가 없었습니다.
이제는 써야 합니다.
실제 문자는 _한 바이트_ (8비트)인데, 그것을 담고 있는 레지스터는 64비트(8바이트)입니다.
여러분이 원하는 것은 마지막("가장 낮은 자리") 바이트뿐이며, 레지스터에 따라 _부분 레지스터 별칭_ 으로 곧바로 접근할 수 있습니다:

| register | least significant byte |
| -------- | ---------------------- |
| `rax`    | `al`                   |
| `rbx`    | `bl`                   |
| `rcx`    | `cl`                   |
| `rdx`    | `dl`                   |
| `rsi`    | `sil`                  |
| `rdi`    | `dil`                  |
| `rbp`    | `bpl`                  |
| `rsp`    | `spl`                  |
| `r8`     | `r8b`                  |
| `r9`     | `r9b`                  |
| `r10`    | `r10b`                 |
| `r11`    | `r11b`                 |
| `r12`    | `r12b`                 |
| `r13`    | `r13b`                 |
| `r14`    | `r14b`                 |
| `r15`    | `r15b`                 |

그러니 문자가 `rax`에 있고 버퍼를 `rsi`가 가리킨다면 `mov [rsi], al`을 해야 합니다.

까다롭지만 차근차근 해내면 플래그가 보상입니다!

----

**디버깅:**
제대로 만들기가 까다로울 수 있습니다.
이 챌린지를 디버깅하려면 코드에 `_start`를 추가하기를 권합니다:

```asm
.global _start
_start:
    mov rdi, 42     # you'll pass 42 as the first argument to your function
    push 0          # this pushes eight 0 bytes to the stack, clearing what will be your output buffer
    mov rsi, rsp    # the output buffer as the second argument to itoa
    int3            # this is optional, if you want gdb to break here without having to set a breakpoint!
    call itoa       # there we go!

    mov rax, 60     # exit cleanly, like a cultured individual
    syscall
```

(`-shared` 없이) 평범한 실행 파일로 어셈블하고 링크한 뒤 `gdb`로 불러오세요. 이 버전에는 진입점이 있습니다:

```console
hacker@dojo:~$ as -o debug.o debug.s
hacker@dojo:~$ ld -o debug debug.o
hacker@dojo:~$ gdb ./debug
(gdb) run
```

실행이 `int3`에서 멈추고, 거기서부터 [소프트웨어 들여다보기](/computing-101/introspecting)에서 배운 기법으로 스택의 메모리와 레지스터 등을 살펴보며 제대로 동작할 때까지 단계별로 진행할 수 있습니다!
여러분의 `.so`를 불러오는 네이티브 하니스를 직접 디버깅할 수도 있습니다:

```console
hacker@dojo:~$ gdb --args /challenge/harness your-solve.so 42
(gdb) run
```

`/challenge/harness` 뒤의 첫 인자는 여러분의 라이브러리이고, 두 번째는 `itoa`에 넘길 대역 숫자입니다.
