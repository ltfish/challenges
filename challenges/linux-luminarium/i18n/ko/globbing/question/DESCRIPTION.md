다음으로 `?`에 대해 배워봅시다.
셸은 인자 안에서 `?` 문자를 만나면 그것을 **한 글자** 와일드카드로 취급합니다.
`*`와 비슷하게 동작하지만 _한_ 글자에만 매칭됩니다.
예를 들면:

```console
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_cc
hacker@dojo:~$ ls
file_a	file_b	file_cc
hacker@dojo:~$ echo Look: file_?
Look: file_a file_b
hacker@dojo:~$ echo Look: file_??
Look: file_cc
```

이제 직접 연습해 봅시다!
홈 디렉터리에서 시작해 `/challenge`로 디렉터리를 옮기되, `cd`에 넘기는 인자에서 `c`와 `l` 대신 `?` 문자를 쓰세요!
도착했으면 `/challenge/run`을 실행해 플래그를 얻으세요!
