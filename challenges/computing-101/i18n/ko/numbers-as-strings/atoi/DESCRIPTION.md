두 자리 `atoi`는 `첫째 * 10 + 둘째`를 했습니다.
자릿수가 둘보다 많으면 어떨까요?
당연히 누적 합계를 두고, 새 숫자마다 `합계 = 합계 * 10 + 숫자`를 하면 됩니다.
그 반복이 바로 _반복문_ 이며, [반복문 작성하기](/computing-101/control-flow/loop-write)에서 연습했고 여기서 응용합니다.

숫자를 왼쪽에서 오른쪽으로 읽습니다:

```
"123":
  total = 0
  '1':  total =  0*10 + 1  =   1
  '2':  total =  1*10 + 2  =  12
  '3':  total = 12*10 + 3  = 123
```

이것을 문자열의 끝까지 합니다. C 언어의 관례(여기서도 씁니다)에서 문자열의 끝은 값이 0x00인 바이트(즉 2진수 `00000000`, 10진수 _값_ 0)로 표시됩니다.
이것은 문자 '0'과 다르다는 점에 주의하세요. 다시 말하지만 문자 '0'의 값은 `0x30`(2진수 `00110000`)입니다.

그러니 반복문은 이렇습니다. 다음 바이트를 보고, `0`이면 반복문 밖으로 점프하고([반복문 작성하기](/computing-101/control-flow/loop-write)를 참고하세요), 아니면 `atoi_digit`이 했던 대로 숫자로 바꾸고, 합계에 `10`을 곱하고, 그 숫자를 더한 뒤 반복문의 처음으로 돌아갑니다.

여러분의 `atoi`는 `rdi`로 문자열의 포인터를 받아 정수 값을 `rax`로 반환해야 합니다.
숫자들을 반복해서 훑고 그 수를 반환하세요.

----

**디버깅:**
제대로 만들기가 까다로울 수 있습니다.
이 챌린지를 디버깅하려면 호출을 흉내 내는 `_start`를 코드에 추가하기를 권합니다:

```
.global _start
_start:
    push 0x333231   # "123" on the stack -- little-endian, so 0x31 ('1') is the first byte, and the high zero bytes terminate it
    mov rdi, rsp    # a pointer to that string, as the first argument to atoi
    int3            # this is optional, if you want gdb to break here without having to set a breakpoint!
    call atoi       # there we go!

    mov rdi, rax    # atoi's result comes back in rax; exit with it so you can read it back with `echo $?`
    mov rax, 60     # exit
    syscall
```

(`-shared` 없이) 평범한 실행 파일로 어셈블하고 링크한 뒤 `gdb`로 불러오세요. 이 버전에는 진입점이 있습니다:

```console
hacker@dojo:~$ as -o debug.o debug.s
hacker@dojo:~$ ld -o debug debug.o
hacker@dojo:~$ gdb ./debug
(gdb) run
```

실행이 `int3`에서 멈추고, 거기서부터 [소프트웨어 들여다보기](/computing-101/introspecting)에서 배운 기법으로 `rdi`가 문자열을 훑고 `rax`에 누적 합계가 쌓이는 것을 지켜보며 단계별로 진행하다 보면 제대로 동작하게 될 것입니다!
