텍스트 입력을 받아 수로 바꿔봤는데, 실제 프로그램은 수를 텍스트로 _출력_ 하기도 해야 합니다.
`atoi`의 역이 되는 이것을 `itoa`(integer to ASCII)라고 부릅니다.
여기서도 같은 방식으로, 먼저 한 자리부터 시작해 만들어 나가겠습니다!

`atoi`의 반대로, 어떤 숫자의 문자는 그 값에 `'0'`(`0x30`)을 더한 것입니다.
`'7'`(ASCII 문자)이 `0x30`을 빼서 `7`(값)이 되었듯, 마찬가지로 `7`(값)은 `0x30`을 더해 `'7'`(ASCII 문자)이 됩니다.

```
7  ->  7 + 0x30  =  0x37  =  '7'
```

`itoa_digit`부터 시작합시다.
여러분의 `itoa_digit`은 `rdi`로 값(한 자리 숫자 `0`-`9`)을 받아 그 ASCII 문자를 `rax`로 반환합니다.
챌린지가 찾을 수 있도록 `.global itoa_digit`을 잊지 마세요.

앞 레벨은 실행 파일 전체였습니다.
이 레벨은 앞서 `atoi` 함수들에서 쓴 공유 라이브러리 방식으로 돌아갑니다:

```console
hacker@dojo:~$ as -o your-solve.o your-solve.s
hacker@dojo:~$ ld -shared -o your-solve.so your-solve.o
hacker@dojo:~$ /challenge/check your-solve.so
```

`0x30`을 더하고 그 문자를 반환해서 플래그를 차지하세요.
