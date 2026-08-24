지금까지는 주로 _읽기_ 권한을 다뤘습니다.
`/flag` 파일을 읽으려고 읽을 수 있게 만들어 왔으니 당연한 일이죠.
이 레벨에서는 실행 권한을 살펴봅니다.

`/challenge/run` 같은 프로그램을 실행하면, 리눅스는 여러분에게 그 프로그램 파일에 대한 실행 권한이 있을 때에만 실제로 실행해 줍니다.
다음을 봅시다:

```console
hacker@dojo:~$ ls -l /challenge/run
-rwxr-xr-x 1 root root    0 May 22 13:42 /challenge/run
hacker@dojo:~$ /challenge/run
Successfully ran the challenge!
hacker@dojo:~$
```

이 경우 `/challenge/run`은 `hacker` 사용자가 실행할 수 있기 때문에 실행됩니다.
파일이 `root` 사용자와 `root` 그룹 소유이므로, 이것은 `other` 권한에 실행 비트가 설정되어 있어야 한다는 뜻입니다.
그 권한을 없애면 실행은 실패합니다!

```console
hacker@dojo:~$ chmod o-x /challenge/run
hacker@dojo:~$ ls -l /challenge/run
-rwxr-xr-- 1 root root    0 May 22 13:42 /challenge/run
hacker@dojo:~$ /challenge/run
bash: /challenge/run: Permission denied
hacker@dojo:~$
```

이 챌린지에서 `/challenge/run` 프로그램은 플래그를 주지만, 먼저 그것을 실행 가능하게 만들어야 합니다!
`chmod`를 떠올려서 `/challenge/run`이 플래그를 알려주게 만드세요!
