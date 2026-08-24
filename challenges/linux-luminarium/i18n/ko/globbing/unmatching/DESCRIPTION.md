때로는 글로브에서 특정 파일을 걸러내고 싶을 때가 있습니다!
다행히 `[]`가 바로 그 일을 도와줍니다.
대괄호 안의 첫 문자가 `!`이거나(최신 bash에서는) `^`이면 글로브가 뒤집혀서, 그 대괄호는 나열된 문자가 _아닌_ 문자에 매칭됩니다.
예를 들면:

```console
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[!ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[^ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```

이 지식으로 무장하고 `/challenge/files`로 가서, `p`, `w`, `n`으로 시작하지 않는 모든 파일을 인자로 주어 `/challenge/run`을 실행하세요!

**참고:** `!` 문자는 `[]` 글로브의 첫 문자가 아닐 때 bash에서 다른 특별한 의미를 가지므로, 뭔가 이상해지면 그 점을 떠올리세요! `^`에는 이 문제가 없지만, 오래된 셸과는 호환되지 않습니다.
