먼저 파일 소유권부터 봅시다.
리눅스의 모든 파일은 시스템의 어떤 사용자가 소유합니다.
일상에서 그 사용자는 대개 여러분이 매일 로그인하는 사용자입니다.

(전산 실습실처럼) 공유 시스템에서는 서로 다른 사용자 계정을 가진 사람이 여럿 있고, 각자 자기 홈 디렉터리에 자기 파일을 둡니다.
하지만 (개인 PC처럼) 공유하지 않는 시스템에서도 리눅스에는 여러 작업을 위한 "서비스" 사용자 계정이 많이 있습니다.

가장 중요한 두 계정은 다음과 같습니다:

1. 여러분의 사용자 계정! pwn.college에서는 사용자명이 무엇이든 `hacker` 사용자입니다.
2. `root`. 관리자 계정이며, 대부분의 보안 상황에서 최종 목표입니다. `root` 사용자를 손에 넣었다면 해킹 목표를 거의 확실히 달성한 셈입니다!

그래서 어떻다는 걸까요?
사실 여러분이 그냥 `cat /flag`를 하지 못하게 막는 방식이 바로, `/flag`를 `root` 사용자가 소유하게 하고, 다른 사용자는 읽지 못하도록 권한을 설정하고(나중에 배웁니다), 실제 챌린지는 `root` 사용자로 실행되게 설정하는 것입니다(이것도 나중에 배웁니다).
그 결과 `cat /flag`를 하면 이렇게 됩니다:

```console
hacker@dojo:~$ ls -l /flag
-r-------- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$ cat /flag
cat: /flag: Permission denied
hacker@dojo:~$
```

여기서 플래그는 `root` 사용자(그 줄의 첫 `root`)와 `root` 그룹(그 줄의 두 번째 `root`)이 소유하고 있습니다.
`hacker` 사용자로 읽으려 하면 거부당합니다.
하지만 우리가 `root`라면(해커의 꿈이죠!) 이 파일을 읽는 데 아무 문제가 없습니다:

```console
root@dojo:~# cat /flag
pwn.college{demo_flag}
root@dojo:~#
```

흥미롭게도 파일의 소유권은 바꿀 수 있습니다!
`chown`(**ch**ange **own**er) 명령으로 합니다:

```
chown [username] [file]
```

보통 `chown`은 `root` 사용자만 실행할 수 있습니다.
다시 `root`인 척해 보고(이건 아무리 해도 질리지 않네요!), `chown`의 전형적인 사용을 봅시다:

```console
root@dojo:~# mkdir pwn_directory
root@dojo:~# touch college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root root    0 May 22 13:42 college_file
drwxr-xr-x 2 root root 4096 May 22 13:42 pwn_directory
root@dojo:~# chown hacker college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 hacker root    0 May 22 13:42 college_file
drwxr-xr-x 2 root   root 4096 May 22 13:42 pwn_directory
root@dojo:~#
```

`college_file`의 소유자가 `hacker` 사용자로 바뀌었고, 이제 `hacker`는 `root`가 그 파일로 할 수 있었던 일을 무엇이든 할 수 있습니다!
이것이 `/flag` 파일이었다면, `hacker` 사용자가 그것을 읽을 수 있다는 뜻입니다!

이 레벨에서는 `/flag` 파일의 소유자를 `hacker` 사용자로 바꾼 뒤 플래그를 읽는 연습을 합니다.
이 챌린지에서만 `hacker` 사용자로도 chown을 마음껏 쓸 수 있게 해 두었습니다(다시 말하지만 보통은 `root`여야 합니다).
이 힘을 현명하게 써서 chown하세요!
