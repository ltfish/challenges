`%d` 표시 하나면 포맷 문자열에 바뀌는 수 하나를 넣을 수 있습니다.
실제 메시지에는 값이 하나보다 많이 필요한 경우가 흔합니다.

이제 같은 포맷 문자열 안에서 여러 개의 `%d` 표시를 지원하세요.
각 `%d`가 다음 커맨드 라인 값을 소비하므로, 프로그램은 다음에 쓸 `argv` 항목이 무엇인지 기억해야 합니다.

```
argv[1]:  "opened %d files and skipped %d"
argv[2]:  "7"
argv[3]:  "3"
output:   "opened 7 files and skipped 3"
```

첫 번째 `%d`는 `argv[2]`를, 두 번째는 `argv[3]`을 쓰는 식입니다.
수 하나를 출력한 뒤에는 그 표시 다음부터 포맷 문자열 훑기를 이어가세요.

앞서처럼 빌드하고 제출하세요:

```console
hacker@dojo:~$ as -o prog.o prog.s
hacker@dojo:~$ ld -o prog prog.o
hacker@dojo:~$ ./prog 'opened %d files and skipped %d' 7 3
opened 7 files and skipped 3
hacker@dojo:~$ /challenge/check prog
```

10진수 인자를 순서대로 소비하세요.
