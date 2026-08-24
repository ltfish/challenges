이제 포맷 문자열에 문법이 들어 있습니다.
백슬래시는 `\n` 같은 이스케이프 시퀀스를 시작하고, 퍼센트는 `%d` 같은 포맷 표시를 시작합니다.

여기서 현실적인 문제가 생깁니다. 때로는 출력에 진짜 백슬래시나 진짜 퍼센트 기호가 들어가야 하니까요.
포매터의 흔한 관례는 문법 바이트를 두 번 적는 것입니다.
입력 바이트 `\\` 두 개는 출력 백슬래시 한 바이트를 쓰고, 입력 바이트 `%%` 두 개는 출력 퍼센트 한 바이트를 씁니다.

```
argv[1]:  "path\\file"
output:   "path\file"

argv[1]:  "progress: 100%%"
output:   "progress: 100%"
```

훑다가 `\\`를 보면 두 입력 바이트를 건너뛰고 백슬래시 한 바이트를 `write`하세요.
`%%`를 보면 두 입력 바이트를 건너뛰고 퍼센트 한 바이트를 `write`하세요.
평범한 텍스트와 `\n` 이스케이프도 계속 지원해야 합니다.

앞서처럼 빌드하고 제출하세요:

```console
hacker@dojo:~$ as -o prog.o prog.s
hacker@dojo:~$ ld -o prog prog.o
hacker@dojo:~$ ./prog 'progress: 100%%'
progress: 100%
hacker@dojo:~$ /challenge/check prog
```

두 번 적은 문법 바이트를 리터럴 한 바이트로 바꾸세요.
