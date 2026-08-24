이번에는 한 바이트씩, 8비트 레지스터 `al`로 검사합니다:

```
mov al, [rdi+0]
cmp al, 0x41
jne fail
```

그리고 여기서 보상이 옵니다. 한 바이트에는 뒤집을 순서가 없으므로 즉시값이 *곧* 문자이며, 이미 순서대로 놓여 있습니다. `0x41`은 그냥 `'A'`죠. 바이트 비교 열여섯 번이면 끝이고, 엔디언 보정은 전혀 필요 없습니다.

이것이 지금까지 적용해 온 규칙의 맨 끝입니다. 뒤집는 단위가 읽기 크기이므로, 한 바이트 읽기는 아무것도 뒤집지 않습니다.
디스어셈블리를 위에서 아래로 훑으며 즉시값을 그대로 읽고 실행하세요.

```console
hacker@dojo:~$ objdump -d -M intel /challenge/reverse-me
hacker@dojo:~$ /challenge/reverse-me YOUR_PASSWORD_HERE
```

----
**경고**:
`/challenge/reverse-me`는 **SUID** 바이너리이므로 디버깅하면 권한이 떨어지고, 내부의 `open("/flag")`가 gdb 아래에서는 조용히 실패합니다.
읽을 때는 `objdump`를 쓰되, 플래그를 얻으려면 **직접** 실행하세요.
