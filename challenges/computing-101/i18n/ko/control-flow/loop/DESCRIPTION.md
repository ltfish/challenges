지금까지 살펴본 제어 흐름 패턴은 모두 한 줄기로 실행되었습니다. 비교하고, 분기하고, 끝나죠.
그런데 같은 동작을 여러 번 반복해야 한다면 어떨까요?
그것이 바로 **반복문(loop)** 입니다. 자기 자신을 반복하려고 _뒤로_ 점프하는 명령어들의 나열이죠.

이 챌린지에서 `/challenge/reverse-me`는 반복문으로 `argv[1]`을 비밀번호와 비교합니다:

```asm
loop:
  mov    al, BYTE PTR [rsi]       ; load next password character
  cmp    al, BYTE PTR [rdi]       ; compare against next argv[1] character
  jne    fail                     ; mismatch → jump to fail
  cmp    al, 0x0                  ; reached the null terminator?
  je     success                  ; yes → all characters matched!
  inc    rdi                      ; **inc**rement rdi to advance to next argv[1] character
  inc    rsi                      ; **inc**rement rsi to advance to next password character
  jmp    loop                     ; jump back to the top — repeat!
```

핵심 명령어는 맨 아래의 `jmp loop`입니다.
(조건이 맞을 때만 점프하는) `jne`와 달리 `jmp`는 **무조건** 항상 점프합니다.
`loop` 레이블로 뒤로 점프함으로써 프로그램은 _다음_ 문자 쌍에 같은 비교 로직을 다시 실행합니다.
반복문은 불일치를 찾거나(`jne fail`), 다른 문자들이 비밀번호와 무사히 일치한 뒤 문자열 끝의 널 종료 문자에 도달하면(`je success`) 끝납니다.

이것이 컴파일된 코드에서 만나게 될 모든 `for` 반복문, `while` 반복문, 문자열 연산 뒤에 있는 기본 패턴입니다.

바이너리를 분석해서 비밀번호를 알아내고 플래그를 얻으세요!
