글로빙은 _경로_ 단위로 일어나므로, 글로빙한 인자로 전체 경로를 펼칠 수 있습니다.
예를 들면:

```console
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: /home/hacker/file_[ab]
Look: /home/hacker/file_a /home/hacker/file_b
```

이제 여러분 차례입니다.
다시 한 번 `/challenge/files`에 파일을 여럿 놓아 두었습니다.
홈 디렉터리에서 시작해, `file_b`, `file_a`, `file_s`, `file_h` 파일의 절대 경로로 펼쳐지는 대괄호 글로브 하나를 인자로 주어 `/challenge/run`을 실행하세요!
