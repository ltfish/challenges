먼저 stdout을 파일로 리다이렉트하는 것부터 봅시다.
`>` 문자로 다음과 같이 할 수 있습니다:

```console
hacker@dojo:~$ echo hi > asdf
```

이렇게 하면 `echo hi`의 출력(`hi`가 되겠죠)이 `asdf` 파일로 리다이렉트됩니다.
그런 다음 `cat` 같은 프로그램으로 이 파일을 출력할 수 있습니다:

```console
hacker@dojo:~$ cat asdf
hi
```

이 챌린지에서는 이 출력 리다이렉션을 써서 `PWN`이라는 단어를(전부 대문자) `COLLEGE`라는 파일 이름에(전부 대문자) 써야 합니다.
