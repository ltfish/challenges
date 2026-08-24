명령을 잇는 가장 쉬운 방법은 `;`입니다.
대부분의 맥락에서 `;`는 Enter가 줄을 나누는 것과 비슷하게 명령을 나눕니다.
그래서 이것은:

```console
hacker@dojo:~$ echo COLLEGE > pwn
hacker@dojo:~$ cat pwn
COLLEGE
hacker@dojo:~$
```

이것과 대체로 같습니다:

```console
hacker@dojo:~$ echo COLLEGE > pwn; cat pwn
COLLEGE
hacker@dojo:~$
```

기본적으로 Enter를 누르면 셸이 여러분이 입력한 명령을 실행하고, 그 명령이 끝난 뒤 다음 명령을 입력하라고 프롬프트를 줍니다.
세미콜론도 비슷하되, 프롬프트가 없고 아무것도 실행되기 전에 여러분이 두 명령을 모두 입력한다는 점이 다릅니다.

지금 해보세요! 이 레벨에서는 `/challenge/pwn`을 실행한 뒤 `/challenge/college`를 실행하되, 세미콜론으로 이어야 합니다.
