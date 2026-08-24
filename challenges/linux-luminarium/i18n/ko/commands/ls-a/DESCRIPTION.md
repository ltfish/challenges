흥미롭게도 `ls`는 기본적으로 _모든_ 파일을 보여주지는 않습니다.
리눅스에는 `.`으로 시작하는 파일이 `ls`를 비롯한 몇몇 상황에서 기본적으로 나타나지 않는 관례가 있습니다.
`ls`로 그런 파일까지 보려면 다음처럼 `-a` 플래그를 붙여야 합니다:

```console
hacker@dojo:~$ touch pwn
hacker@dojo:~$ touch .college
hacker@dojo:~$ ls
pwn
hacker@dojo:~$ ls -a
.college	pwn
hacker@dojo:~$
```

이제 여러분 차례입니다!
`/`에 점으로 시작하는 파일로 숨겨진 플래그를 찾아내세요.
