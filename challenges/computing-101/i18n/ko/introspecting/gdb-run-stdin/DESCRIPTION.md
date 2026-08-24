앞 레벨에서는 gdb의 `run`으로 커맨드 라인 인자를 넘겼습니다.
프로그램은 stdin에서 읽을 수도 있고, gdb는 대상 프로그램을 실행할 때 stdin을 리다이렉트할 수 있게 해 줍니다.
문법은 셸에서 본 리다이렉션과 같지만, gdb 안에서 `run` 뒤에 옵니다:

```text
(gdb) run < /path/to/input
```

이 챌린지에서 `/challenge/debug-me`는 필요한 입력을 `/challenge/secret`에서 읽습니다.
`/challenge/secret`을 stdin으로 리다이렉트해서 gdb 아래에서 실행하고, 출력되는 비밀 숫자를 읽어 `/challenge/submit-number`로 제출하세요.
