가장 먼저 배울 글로브는 `*`입니다.
셸은 인자 안에서 `*` 문자를 만나면 그것을 "와일드카드"로 취급해서, 그 패턴에 맞는 파일들로 인자를 바꾸려 합니다.
설명보다 보여주는 것이 빠릅니다:

```console
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_*
Look: file_a file_b file_c
```

물론 이 경우에는 글로브가 여러 개의 인자로 펼쳐졌지만, 하나만 매칭될 수도 있습니다.
예를 들면:

```console
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: file_*
Look: file_a
```

매칭되는 파일이 하나도 없으면, 기본적으로 셸은 글로브를 그대로 둡니다:

```console
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: nope_*
Look: nope_*
```

`*`는 `/`와 맨 앞의 `.` 문자를 제외한 파일 이름의 어떤 부분에도 매칭됩니다.
예를 들면:

```console
hacker@dojo:~$ echo ONE: /ho*/*ck*
ONE: /home/hacker
hacker@dojo:~$ echo TWO: /*/hacker
TWO: /home/hacker
hacker@dojo:~$ echo THREE: ../*
THREE: ../hacker
```

이제 직접 연습해 봅시다!
홈 디렉터리에서 시작해 `/challenge`로 디렉터리를 옮기되, 글로빙을 써서 `cd`에 넘기는 인자를 네 글자 이하로 만드세요!
도착했으면 `/challenge/run`을 실행해 플래그를 얻으세요!
