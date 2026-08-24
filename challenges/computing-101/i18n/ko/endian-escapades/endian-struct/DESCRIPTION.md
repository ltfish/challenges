실제 프로그램이 버퍼를 하나의 균일한 크기로 읽는 일은 드뭅니다.
프로그램은 *구조체(struct)* 를 읽습니다. 크기가 *서로 다른* 필드 몇 개가 메모리에 차례로 놓인 것이죠(사실 _struct_ 는 _structure_ 의 줄임말입니다).

이 `/challenge/reverse-me`는 여러분의 비밀번호를 구조체로 다룹니다.
C 언어를 모를 수도 있지만, 안다면 그 구조체는 이렇게 정의되었을 것입니다:

```c
struct { uint64_t a; uint32_t b; uint16_t c; uint8_t d; uint8_t e; };
```

디스어셈블리는 각 필드를 자기 폭과 오프셋으로 불러옵니다:

```
movabs rbx, 0x................   ; a: 8-byte field at +0
mov    rax, [rdi+0]
cmp    rax, rbx
mov    eax, [rdi+8]               ; b: 4-byte field at +8
cmp    eax, 0x........
mov    ax,  [rdi+12]              ; c: 2-byte field at +12
cmp    ax,  0x....
mov    al,  [rdi+14]              ; d: 1-byte field at +14
cmp    al,  0x..
mov    al,  [rdi+15]              ; e: 1-byte field at +15
cmp    al,  0x..
```

이 챌린지 하나에 이 모듈 전체가 담겨 있습니다.
각 필드마다 그 접근에서 세 가지를 읽어내세요. *폭* (`rax`/`eax`/`ax`/`al`에서), *오프셋* (`[rdi+X]`), 그리고 *값* (필드 폭에 맞게 즉시값을 엔디언 보정)입니다.
필드들을 오프셋 순서대로 다시 맞추면 비밀번호가 됩니다.

```console
hacker@dojo:~$ objdump -d -M intel /challenge/reverse-me
hacker@dojo:~$ /challenge/reverse-me YOUR_PASSWORD_HERE
```

----
**경고**:
`/challenge/reverse-me`는 **SUID** 바이너리이므로 디버깅하면 권한이 떨어지고, 내부의 `open("/flag")`가 gdb 아래에서는 조용히 실패합니다.
읽을 때는 `objdump`를 쓰되, 플래그를 얻으려면 **직접** 실행하세요.
