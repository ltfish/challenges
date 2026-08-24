x86이 여러 바이트 값을 *리틀 엔디언* 으로, 즉 낮은 바이트를 먼저 저장한다는 것을 방금 읽었습니다.
이제 써먹을 시간입니다. `/challenge/reverse-me`는 8글자 비밀번호를 자기 코드 깊숙한 곳의 qword 하나에 숨기고 있습니다.

이 프로그램은 여러분의 입력을 불러와 8바이트 전부를 하드코딩된 값과 한 번에 비교합니다:

```
movabs rbx, 0x4847464544434241
mov    rax, [rdi]
cmp    rax, rbx
jne    fail
```

(`movabs`는 처음 보겠지만 그냥 `mov`입니다. 보통 `mov`의 즉시값은 최대 32비트라, 상수가 64비트를 다 채우면 어셈블러가 이 더 넓은 형태("move absolute")를 씁니다. `mov`로 읽으면 됩니다.)

그 즉시값은 *CPU가 메모리에서 읽은 그대로의* 비밀번호이며, 리틀 엔디언이므로 바이트가 뒤집혀 있습니다:

```
0x4847464544434241  ->  bytes 48 47 46 45 44 43 42 41  (high to low, as printed)
                    ->  low byte first: 41 42 43 44 45 46 47 48  ->  "ABCDEFGH"
```

디스어셈블해서 그 `movabs` 즉시값 하나를 읽고, 여덟 바이트를 뒤집어 비밀번호를 만든 뒤 실행하세요:

```console
hacker@dojo:~$ objdump -d -M intel /challenge/reverse-me
hacker@dojo:~$ /challenge/reverse-me YOUR_PASSWORD_HERE
```

----
**경고**:
`/challenge/reverse-me`는 **SUID** 바이너리이므로 디버깅하면 권한이 떨어지고, 내부의 `open("/flag")`가 gdb 아래에서는 조용히 실패합니다.
읽을 때는 `objdump`를 쓰되, 플래그를 얻으려면 **직접** 실행하세요.
