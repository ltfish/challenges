앞 레벨에서는 여러분이 프로그램을 시작한 뒤 저희가 `disassemble` 명령을 대신 실행해 주었습니다.
이제 여러분 차례입니다!

`starti`로 프로그램을 시작한 다음, `disassemble` 명령을 직접 실행해야 합니다:

```gdb
(gdb) starti
...
(gdb) disassemble
Dump of assembler code for function main:
=> 0x0000000000401000 <+0>:     mov    rdi,0x539
   0x0000000000401007 <+7>:     mov    rdi,0x0
   0x000000000040100e <+14>:    mov    rax,0x3c
   0x0000000000401015 <+21>:    syscall
End of assembler dump.
```

출력을 읽어 비밀 숫자를 찾은 뒤 `/challenge/submit-number`로 제출하세요.
