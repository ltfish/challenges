지금까지는 어떤 파일을 다뤄야 하는지 저희가 알려드렸습니다.
하지만 디렉터리 안에는 파일(그리고 다른 디렉터리)이 잔뜩 들어 있을 수 있고, 그 이름을 매번 알려드릴 수는 없습니다.
`ls` 명령어로 그 내용을 **l**i**s**t 하는 법을 배워야 합니다!

`ls`는 인자로 받은 모든 디렉터리의 파일을 나열하고, 인자가 없으면 현재 디렉터리의 파일을 나열합니다.
직접 봅시다:

```console
hacker@dojo:~$ ls /challenge
run
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ ls /home/hacker
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$
```

이 챌린지에서는 `/challenge/run`에 무작위 이름을 붙여 두었습니다!
`/challenge`의 파일을 나열해서 그것을 찾아내세요.
그런 다음 찾아낸 절대 경로를 실행해서 플래그를 얻으세요.
