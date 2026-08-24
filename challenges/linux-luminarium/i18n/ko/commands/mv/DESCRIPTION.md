`mv` 명령어로 파일을 _옮길_ 수도 있습니다.
사용법은 간단합니다:

```console
hacker@dojo:~$ ls
my-file
hacker@dojo:~$ cat my-file
PWN!
hacker@dojo:~$ mv my-file your-file
hacker@dojo:~$ ls
your-file
hacker@dojo:~$ cat your-file
PWN!
hacker@dojo:~$
```

이 챌린지는 `/flag` 파일을 `/tmp/hack-the-planet`으로 옮기기를 원합니다(그렇게 하세요)!
단, 다른 방법(예를 들어 VSCode에서 파일 이름 바꾸기)이 아니라 _반드시_ `mv` 명령어를 써야 합니다.
다 했으면 `/challenge/check`를 실행하세요. 확인한 뒤 플래그를 줍니다.
