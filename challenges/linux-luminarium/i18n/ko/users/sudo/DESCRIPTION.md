옛날에는 일반적인 리눅스 시스템에 `root` 비밀번호가 있어서, 관리자들이 (자기 계정 비밀번호로 로그인한 뒤) 그것으로 `root`에 `su`하곤 했습니다.
하지만 `root` 비밀번호는 관리하기 번거롭고, 비밀번호(나 그 해시!)가 유출될 수 있으며, 서버 여러 대를 다루는 큰 환경에는 잘 맞지 않습니다.
이를 해결하려고 최근 수십 년 사이 세상은 `su`를 통한 관리에서 `sudo`를 통한 관리로 옮겨 갔습니다(*재미있는 사실*: `sudo`는 원래 **su**peruser **do**의 줄임말이었지만 이제는 "`su` 'do'"로 바뀌었고, `su`가 "substitute user"를 뜻하므로 현재 `sudo`의 의미는 "substitute user, do"입니다).

지정한 사용자로 셸을 띄우는 것이 기본인 `su`와 달리, `sudo`는 기본적으로 명령을 `root`로 실행합니다:

```console
hacker@dojo:~$ whoami
hacker
hacker@dojo:~$ sudo whoami
root
hacker@dojo:~$
```

플래그를 얻는 것과 좀 더 관련지어 보면:

```console
hacker@dojo:~$ grep hacker /etc/shadow
grep: /etc/shadow: Permission denied
hacker@dojo:~$ sudo grep hacker /etc/shadow
hacker:$6$Xro.e7qB3Q2Jl2sA$j6xffIgWn9xIxWUeFzvwPf.nOH2NTWNJCU5XVkPuONjIC7jL467SR4bXjpVJx4b/bkbl7kyhNquWtkNlulFoy.:19921:0:99999:7:::
hacker@dojo:~$
```

비밀번호 인증에 기대는 `su`와 달리, `sudo`는 정책을 확인해서 그 사용자가 `root`로 명령을 실행할 권한이 있는지 판단합니다.
이 정책은 `/etc/sudoers`에 정의되어 있으며, 여기서 깊이 다루지는 않지만 이에 대해 배울 수 있는 [자료](https://www.digitalocean.com/community/tutorials/how-to-edit-the-sudoers-file)는 많습니다!

그래서 세상은 `sudo`로 옮겨 갔고, (시스템 관리라는 목적에서는) `su`를 뒤로 남겨 두었습니다.
사실 pwn.college의 특권 모드(Privileged Mode)도 여러분에게 권한을 올릴 수 있는 `sudo` 접근을 주는 방식으로 동작합니다!

이 레벨에서는 `sudo` 접근을 드릴 테니, 그것으로 플래그를 읽으세요.
아주 쉽고 간단합니다!

----
**참고:**
이 레벨 다음부터는 특권 모드를 켤 수 있습니다!
워크스페이스에서 잠긴 자물쇠를 클릭하면 특권 모드로 챌린지를 다시 시작하고, 열린 자물쇠를 클릭하면 일반 모드로 돌아옵니다.
특권 모드가 켜져 있는 동안에는 터미널 프롬프트의 호스트명이 `~practice`로 끝납니다.
특권 모드는 들여다보고 디버깅할 수 있도록 완전한 `sudo` 접근을 주지만, 제출할 수 없는 자리표시자 플래그를 줍니다.
