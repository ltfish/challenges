`root`가 되어야 하는 것은 해커만이 아닙니다.
자기 컴퓨터의 주인으로서 여러분도 컴퓨터를 관리하려면 `root` 권한을 써야 할 때가 많습니다.
`root`가 되는 것은 리눅스 사용자가 꽤 흔히 하는 일이며, 이를 위한 유틸리티가 둘 있습니다: `su`와 `sudo`입니다.

이 챌린지에서는 더 오래된 쪽인 `su`(**s**ubstitute **u**ser 명령어)를 다룹니다.
요즘은 `root` 권한을 얻는 데 잘 쓰이지 않지만, 좀 더 점잖던 시절의 우아한 유틸리티이므로 먼저 다뤄 보겠습니다.

`su`는 setuid 바이너리입니다:

```console
hacker@dojo:~$ ls -l /usr/bin/su
-rwsr-xr-x 1 root root 232416 Dec 1 11:45 /usr/bin/su
hacker@dojo:~$
```

SUID 비트가 설정되어 있으므로 `su`는 `root`로 실행됩니다.
`root`로 실행되니 `root` 셸을 띄울 수 있습니다!
물론 `su`는 분별이 있어서, 사용자가 `root`로 권한을 올리도록 허락하기 전에 그 사용자가 `root` 비밀번호를 아는지 확인합니다:

```console
hacker@dojo:~$ su
Password: 
su: Authentication failure
hacker@dojo:~$
```

`root` 비밀번호를 확인한다는 바로 이 점 때문에 `su`는 낡은 방식이 되었습니다.
요즘 시스템에는 `root` 비밀번호가 있는 경우가 아주 드물고, 관리자 권한을 주는 데는 (나중에 배울) 다른 메커니즘을 씁니다.

하지만 이 챌린지에는(오직 이 챌린지에만) `root` 비밀번호가 _있습니다_.
그 비밀번호는 `hack-the-planet`이며, `root`가 되려면 이것을 `su`에 넘겨야 합니다!
그렇게 해서 플래그를 읽으세요!
