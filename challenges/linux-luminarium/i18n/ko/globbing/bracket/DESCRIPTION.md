다음으로 `[]`를 다룹니다.
대괄호는 본질적으로 `?`의 제한된 형태입니다. 아무 문자에나 매칭되는 대신, 대괄호 안에 적어둔 특정 문자 집합에 대한 와일드카드로 동작합니다.
예를 들어 `[pwn]`은 `p`, `w`, `n` 중 한 문자에 매칭됩니다.
예를 들면:

```console
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```

여기서 해보세요!
`/challenge/files`에 파일을 여럿 놓아 두었습니다.
작업 디렉터리를 `/challenge/files`로 옮기고, `file_b`, `file_a`, `file_s`, `file_h`로 펼쳐지는 대괄호 글로브 하나를 인자로 주어 `/challenge/run`을 실행하세요!
