인자 없이 실행하면 `su`는 (`root`의 비밀번호로 인증한 뒤) `root` 셸을 띄웁니다.
하지만 사용자명을 인자로 주면 `root` 대신 _그_ 사용자로 전환할 수도 있습니다.
예를 들면:

```console
hacker@dojo:~$ su some-user
Password:
some-user@dojo:~$
```

멋지네요!
이 레벨에서는 `zardus` 사용자로 전환한 뒤 `/challenge/run`을 실행해야 합니다.
Zardus의 비밀번호는 `dont-hack-me`입니다.
행운을 빕니다!
