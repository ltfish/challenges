파일은 여러분 주위에 넘쳐납니다.
사탕 껍질처럼, 언젠가는 너무 많아지죠.
이 레벨에서는 치우는 법을 배웁니다!

리눅스에서는 `rm` 명령어로 파일을 **r**e**m**ove 합니다:

```console
hacker@dojo:~$ touch PWN
hacker@dojo:~$ touch COLLEGE
hacker@dojo:~$ ls
COLLEGE     PWN
hacker@dojo:~$ rm PWN
hacker@dojo:~$ ls
COLLEGE
hacker@dojo:~$
```

연습해 봅시다.
이 챌린지는 여러분의 홈 디렉터리에 `delete_me` 파일을 만듭니다!
그것을 삭제한 뒤 `/challenge/check`를 실행하면, 제대로 지웠는지 확인하고 플래그를 줍니다!
