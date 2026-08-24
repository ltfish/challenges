물론 파일을 _만들_ 수도 있습니다!
방법은 여러 가지지만, 여기서는 간단한 명령어 하나를 살펴봅니다.
`touch` 명령어로 파일을 _건드리면_ 비어 있는 새 파일이 만들어집니다:

```
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ touch pwnfile
hacker@dojo:/tmp$ ls
pwnfile
hacker@dojo:/tmp$
```

이렇게 간단합니다!
이 레벨에서는 `/tmp/pwn`과 `/tmp/college` 두 개의 파일을 만들고, `/challenge/run`을 실행해서 플래그를 얻으세요!
