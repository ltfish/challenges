가장 핵심적인 리눅스 명령어 중 하나가 `cat`입니다.
`cat`은 대개 다음처럼 파일 내용을 읽어내는 데 씁니다:

```console
hacker@dojo:~$ cat /path/to/file
Hello Hackers!
```

인자를 여러 개 주면 `cat`은 여러 파일을 이어 붙여(con**cat**enate, 그래서 이런 이름입니다) 출력합니다.
예를 들면:

```console
hacker@dojo:~$ cat myfile
This is my file!
hacker@dojo:~$ cat yourfile
This is your file!
hacker@dojo:~$ cat myfile yourfile
This is my file!
This is your file!
hacker@dojo:~$ cat myfile yourfile myfile
This is my file!
This is your file!
This is my file!
```

마지막으로, 인자를 아예 주지 않으면 `cat`은 터미널 입력을 읽어서 그대로 출력합니다.
그건 뒤쪽 챌린지에서 살펴봅니다...

이 챌린지에서는 플래그를 여러분의 홈 디렉터리(셸이 시작하는 곳)의 `flag` 파일로 복사해 두었습니다.
`cat`으로 읽어보세요!
