엔디언은 64비트 값에만 해당하는 것이 아닙니다.
메모리에서 읽는 _모든_ 정수는 리틀 엔디언으로 돌아오며, 뒤집히는 바이트는 정확히 그 읽기가 다루는 범위입니다.
예를 들어 `rdi`가 가리키는 메모리에 연달아 놓인 다음 바이트들을 봅시다:

```
rdi -> 11 22 33 44 55 66 77 88
```

이 8바이트를 전부 `mov rsi, [rdi]`로 `rsi`에 읽으면 `rsi`의 값은 `0x8877665544332211`이 됩니다.
32비트(4바이트) 값 두 개로 읽을 수도 있습니다(예를 들어 각각 `rsi`와 `rdx`의 32비트인 4바이트 _부분_ 레지스터 `esi`와 `edx`로요):

```
mov esi, [rdi]      // results in 0x44332211 in esi
mov edx, [rdi+4]    // results in 0x88776655 in edx
```

써놓고 보면 당연하지만 _헷갈리는_ 사람도 있습니다.
구체적으로 8바이트 값 전체가 뒤집히는 일은 일어나지 _않습니다_(그랬다면 위의 `esi`에 0x88이 들어갔겠죠).

이 챌린지에서 그것을 연습합니다.
`/challenge/reverse-me`는 같은 종류의 비밀번호를 4바이트씩, **32비트 값**("dword")으로 검사하므로 정수가 둘이 아니라 넷입니다.
각 dword는 여전히 자기 네 바이트를 뒤집고, dword들끼리는 qword 때와 마찬가지로 주소 순서를 지킵니다.
dword는 일반적인 즉시값 크기에 들어맞으므로 각 검사는 곧바로 `cmp eax, 0x........`이며, 복원할 값이 명령어에 그대로 드러나 있습니다:

```
mov eax, [rdi+0]
cmp eax, 0x44434241
jne fail
```

`/challenge/reverse-me`를 디스어셈블해서 네 개의 `cmp eax` 즉시값을 읽고, 각 dword를 엔디언 보정한 뒤 주소 순서대로 이어 붙여 실행하세요:

```console
hacker@dojo:~$ objdump -d -M intel /challenge/reverse-me
hacker@dojo:~$ /challenge/reverse-me YOUR_PASSWORD_HERE
```

----
**경고**:
`/challenge/reverse-me`는 **SUID** 바이너리이므로 디버깅하면 권한이 떨어지고, 내부의 `open("/flag")`가 gdb 아래에서는 조용히 실패합니다.
읽을 때는 `objdump`를 쓰되, 플래그를 얻으려면 **직접** 실행하세요.
