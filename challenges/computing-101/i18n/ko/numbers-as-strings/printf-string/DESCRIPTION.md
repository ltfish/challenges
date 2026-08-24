이제 문자열을 끼워 넣는 표시인 `%s`를 추가합니다.
`%d`와 비슷하지만, 다음 `argv` 값이 이미 텍스트이므로 `atoi`나 `itoa`가 필요 없습니다.

`%s`는 다음 커맨드 라인 문자열을 가져와 길이를 구하고 그 바이트들을 `write`합니다.
`%d`는 앞 레벨들에서 하던 수 변환을 그대로 합니다.
각 표시는 다음 커맨드 라인 값을 순서대로 소비합니다.
포매터 문법이 들어 있는 문자열은 포맷 문자열뿐입니다.
`%s`의 인자에 `\`나 `%` 같은 바이트가 들어 있다면, 이스케이프나 표시로 다루지 말고 그대로 복사하세요.

```
argv[1]:  "%s has %d flags"
argv[2]:  "hacker"
argv[3]:  "3"
output:   "hacker has 3 flags"
```

```
argv[1]:  "%s"
argv[2]:  "LITERAL\WITH\SLASHES"
output:   "LITERAL\WITH\SLASHES"
```

즉 이제 프로그램은 두 개의 위치를 추적합니다. 포맷 문자열에서의 위치와, 다음에 소비할 `argv` 값이죠.

앞서처럼 빌드하고 제출하세요:

```console
hacker@dojo:~$ as -o prog.o prog.s
hacker@dojo:~$ ld -o prog prog.o
hacker@dojo:~$ ./prog '%s has %d flags' hacker 3
hacker has 3 flags
hacker@dojo:~$ /challenge/check prog
```

값을 순서대로 소비하고 필요할 때마다 각 조각을 쓰세요.
