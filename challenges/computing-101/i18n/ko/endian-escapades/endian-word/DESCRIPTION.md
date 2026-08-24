더 작게 가봅시다. 이제 `/challenge/reverse-me`는 두 바이트씩, **word** 단위로 검사합니다.

규칙은 변하지 않습니다. 뒤집히는 바이트는 정확히 그 읽기에 포함된 것들입니다.
word 읽기는 두 바이트를 맞바꾸고, word들끼리는 주소 순서를 지킵니다.
(그리고 한 바이트 읽기는 맞바꿀 것이 없으므로, 단일 바이트는 엔디언 보정이 필요 없습니다.)

`/challenge/reverse-me`를 디스어셈블해서 여덟 개의 `cmp ax, 0x....` 즉시값을 읽고, 각 쌍을 맞바꾸되 word는 주소 순서를 지켜 실행하세요:

```console
hacker@dojo:~$ objdump -d -M intel /challenge/reverse-me
hacker@dojo:~$ /challenge/reverse-me YOUR_PASSWORD_HERE
```

----
**경고**:
`/challenge/reverse-me`는 **SUID** 바이너리이므로 디버깅하면 권한이 떨어지고, 내부의 `open("/flag")`가 gdb 아래에서는 조용히 실패합니다.
읽을 때는 `objdump`를 쓰되, 플래그를 얻으려면 **직접** 실행하세요.
