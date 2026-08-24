앞의 구조체는 필드를 위에서 아래로, 메모리 순서대로 읽었으므로 디스어셈블리를 그대로 훑기만 해도 비밀번호가 순서대로 나왔습니다.
하지만 그것이 보장되지는 않습니다.
프로그램은 구조체의 필드를 *어떤* 순서로든 검사할 수 있으며, 코드에서 비교가 나오는 순서는 그 바이트가 메모리 어디에 있는지와 아무 상관이 없습니다.

이 `/challenge/reverse-me`는 같은 다섯 필드를 검사하지만 *뒤섞어서* 합니다:

```
mov    ax,  [rdi+12]              ; the +12 word might be checked first...
cmp    ax,  0x....
mov    al,  [rdi+15]              ; ...then a byte from the very end...
cmp    al,  0x..
movabs rbx, 0x................    ; ...then the +0 qword, and so on.
mov    rax, [rdi+0]
cmp    rax, rbx
```

그래서 더는 디스어셈블리를 그대로 훑어 비밀번호를 읽을 수 없습니다.
각 필드의 *값* 은 앞서와 똑같이 복원하되, 이제는 `[rdi+X]` 불러오기에서 그 *오프셋* 도 읽어야 합니다. 그 오프셋이 바로 그 바이트들이 있어야 할 자리입니다.
각 필드를 자기 오프셋에 놓고 오프셋 순서대로 이어 붙이면 비밀번호가 됩니다.

```console
hacker@dojo:~$ objdump -d -M intel /challenge/reverse-me
hacker@dojo:~$ /challenge/reverse-me YOUR_PASSWORD_HERE
```

----
**경고**:
`/challenge/reverse-me`는 **SUID** 바이너리이므로 디버깅하면 권한이 떨어지고, 내부의 `open("/flag")`가 gdb 아래에서는 조용히 실패합니다.
읽을 때는 `objdump`를 쓰되, 플래그를 얻으려면 **직접** 실행하세요.
