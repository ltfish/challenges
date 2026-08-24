앞 모듈에서 살펴봤듯이, `root`가 아닌 사용자에게도 특정 시스템 작업을 하려면 높은 권한이 필요한 경우가 많습니다.
`root`나 sudoers만 할 수 있는 작업을 사용자가 할 때마다 시스템 관리자가 옆에서 비밀번호를 알려줄 수는 없습니다.
대신 "Set User ID"(SUID) 권한 비트를 쓰면 사용자가 그 프로그램 파일의 소유자로서 프로그램을 실행할 수 있습니다.

이것이 바로 여러분이 실행하는 챌린지 프로그램이 플래그를 읽을 수 있게 하는, 그리고 pwn.college 바깥에서는 `su`나 `sudo` 같은 시스템 관리 도구를 가능하게 하는 바로 그 메커니즘입니다.
SUID가 붙은 파일의 권한은 이렇게 보입니다:

```console
hacker@dojo:~$ ls -l /usr/bin/sudo
-rwsr-xr-x 1 root root 232416 Dec 1 11:45 /usr/bin/sudo
hacker@dojo:~$
```

실행 비트 자리에 있는 `s`는 그 프로그램이 _SUID로_ 실행된다는 뜻입니다.
즉 (실행 권한만 있다면) 어떤 사용자가 실행하든, 그 프로그램은 소유 사용자(여기서는 `root` 사용자)로 실행된다는 의미입니다.

파일의 소유자라면 chmod로 그 파일의 SUID 비트를 설정할 수 있습니다:

```
chmod u+s [program]
```

하지만 조심하세요!
`root`가 소유한 실행 파일에 SUID 비트를 주면 공격자에게 `root`가 될 수 있는 공격 경로를 열어줄 수 있습니다.
이에 대해서는 [Program Misuse 모듈](/fundamentals/program-misuse/)에서 더 배웁니다.

이제 `/challenge/getroot` 프로그램에 SUID 비트를 붙여서 `root` 셸을 띄우고, 여러분이 직접 플래그를 `cat`할 수 있게 해 드리겠습니다!
