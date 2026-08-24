짝수/홀수 검사에서 `and`를 만났는데, 여기서는 원하는 비트만 남기는 데 씁니다.

비트 `and`는 두 값을 비트 단위로 비교합니다. 각 출력 비트는 두 입력 비트가 *모두* `1`일 때만 `1`이죠.
그래서 `and`는 *마스킹* 의 도구입니다. 원하는 비트는 남기고 나머지는 0으로 만드는 것이죠.

마스크가 `1`인 자리는 원래 비트가 그대로 통과하고, `0`인 자리는 결과 비트가 지워집니다:

```
  1011 0110   (your value)
& 0000 1111   (the mask: keep the low 4 bits)
---------
  0000 0110   (everything above the low 4 bits is gone)
```

x86에서 그 마스킹은 마스크를 두 번째 피연산자로 주는 `and` 하나로 *끝납니다*:

```
and rax, 0xF
```

흔한 용도는 `0xFF`로 마스킹해 값의 가장 낮은 바이트, 즉 낮은 8비트만 뽑아내는 것입니다.

`rdi`로 64비트 값을 받아 그 가장 낮은 바이트만 `rax`로 반환하는 함수를 작성하세요.
이름은 대문자로 `LOBYTE`라고 하세요. **LO**w **BYTE**를 뜻하며, 나중에 익숙해질 도구들에서 이 기능을 가리키는 약칭으로 자주 쓰입니다.
`.global LOBYTE`로 내보내세요.

공유 라이브러리로 빌드해서 채점기에 넘기세요:

```console
hacker@dojo:~$ as -o lobyte.o lobyte.s
hacker@dojo:~$ ld -shared -o lobyte.so lobyte.o
hacker@dojo:~$ /challenge/check lobyte.so
```
