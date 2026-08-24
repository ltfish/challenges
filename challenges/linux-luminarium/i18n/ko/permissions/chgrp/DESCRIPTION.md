나눔은 배려이고, 나눔은 리눅스의 설계에 녹아 있습니다.
파일에는 소유 _사용자_ 와 소유 _그룹_ 이 모두 있습니다.
한 그룹에는 여러 사용자가 속할 수 있고, 한 사용자는 여러 그룹에 속할 수 있습니다.

자신이 어떤 그룹에 속해 있는지는 `id` 명령으로 확인할 수 있습니다:

```console
hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
hacker@dojo:~$
```

여기서 `hacker` 사용자는 `hacker` 그룹에만 속해 있습니다.
그룹의 가장 흔한 용도는 여러 시스템 자원에 대한 접근을 통제하는 것입니다.
예를 들어 pwn.college의 "특권 모드"는 더 편하게 디버깅하도록 root 접근을 줍니다.
이것은 특권 모드로 실행할 때 그룹을 하나 더 붙여주는 방식으로 처리됩니다:

```console
hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker),27(sudo)
hacker@dojo:~$
```

일반적인 리눅스 데스크톱의 주 사용자는 그룹이 _아주 많습니다_.
예를 들어 Zardus의 데스크톱은 이렇습니다:

```console
zardus@yourcomputer:~$ id
uid=1000(zardus) gid=1000(zardus) groups=1000(zardus),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),100(users),106(netdev),114(bluetooth),117(lpadmin),120(scanner),995(docker)
zardus@yourcomputer:~$
```

이 그룹들 덕분에 Zardus는 CD와 플로피 디스크를 읽고(요즘 누가 그러죠?), 시스템을 관리하고, 음악을 재생하고, 모니터에 그림을 그리고, 블루투스를 쓰는 등의 일을 할 수 있습니다.
이런 접근 통제는 파일 시스템의 그룹 소유권을 통해 이루어지는 경우가 많습니다!
예를 들어 그래픽 출력은 특별한 `/dev/fb0` 파일로 할 수 있습니다:

```console
zardus@yourcomputer:~$ ls -l /dev/fb0
crw-rw---- 1 root video 29, 0 Jun 30 23:42 /dev/fb0
zardus@yourcomputer:~$
```

이 파일은 특별한 _장치 파일_ 이며(타입 `c`는 "문자 장치"라는 뜻입니다), 이 파일과 주고받는 동작은 (일반 파일처럼 디스크 저장 내용을 바꾸는 대신) 화면 출력을 바꿉니다!
Zardus의 계정이 이 파일을 다룰 수 있는 이유는, 파일의 그룹 소유자가 `video`이고 Zardus가 `video` 그룹의 구성원이기 때문입니다.

하지만 도장의 `/flag` 파일은 사정이 다릅니다!
다음을 봅시다:

```console
hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
hacker@dojo:~$ ls -l /flag
-r--r----- 1 root root ... /flag
hacker@dojo:~$ cat /flag
cat: /flag: Permission denied
hacker@dojo:~$
```

여기서 플래그 파일은 `root` 사용자와 `root` 그룹이 소유하고 있는데, `hacker` 사용자는 `root` 사용자도 아니고 `root` 그룹의 구성원도 아니므로 파일에 접근할 수 없습니다.
다행히 그룹 소유권은 `chgrp`(**ch**ange **gr**ou**p**) 명령으로 바꿀 수 있습니다!
파일의 소유자이면서 _동시에_ 새 그룹의 구성원이 아니라면 보통 `root` 권한이 필요하므로, `root`가 되어 살펴봅시다:

```console
root@dojo:~# mkdir pwn_directory
root@dojo:~# touch college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root root    0 May 22 13:42 college_file
drwxr-xr-x 2 root root 4096 May 22 13:42 pwn_directory
root@dojo:~# chgrp hacker college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root hacker    0 May 22 13:42 college_file
drwxr-xr-x 2 root root   4096 May 22 13:42 pwn_directory
root@dojo:~#
```

이 레벨에서는 플래그를 소유 그룹이 읽을 수 있게 해 두었는데, 지금 그 그룹은 `root`입니다.
다행히 `hacker` 사용자로도 `chgrp`를 실행할 수 있게 해 두었습니다!
플래그 파일의 그룹 소유권을 바꾸고 플래그를 읽으세요!
