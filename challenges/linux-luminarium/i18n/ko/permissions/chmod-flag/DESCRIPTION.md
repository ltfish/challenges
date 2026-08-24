이제 소유권에는 꽤 익숙해졌습니다.
동전의 반대편인 파일 권한을 이야기해 봅시다.
예시를 다시 떠올려 보죠:

```console
hacker@dojo:~$ mkdir pwn_directory
hacker@dojo:~$ touch college_file
hacker@dojo:~$ ls -l
total 4
-rw-r--r-- 1 hacker hacker    0 May 22 13:42 college_file
drwxr-xr-x 2 hacker hacker 4096 May 22 13:42 pwn_directory
hacker@dojo:~$
```

다시 말하지만 첫 글자는 파일 종류입니다.
그다음 아홉 글자가 파일이나 디렉터리의 실제 접근 권한이며, 소유 사용자의 권한을 나타내는 3글자(이제 이해하시죠!), 소유 그룹의 권한을 나타내는 3글자(이것도 이제 이해하시죠!), 그리고 그 밖의 모든 접근(다른 사용자나 다른 그룹 등)의 권한을 나타내는 3글자로 나뉩니다.

세 글자 각각은 서로 다른 종류의 권한을 나타냅니다:

```
r - user/group/other can read the file (or list the directory)
w - user/group/other can modify the files (or create/delete files in the directory)
x - user/group/other can execute the file as a program (or can enter the directory, e.g., using `cd`)
- - nothing 
```

위의 `college_file`에서 `rw-r--r--` 권한은 이렇게 해석됩니다:

- `r`: 파일을 소유한 사용자(`hacker` 사용자)가 읽을 수 있습니다
- `w`: 파일을 소유한 사용자(`hacker` 사용자)가 쓸 수 있습니다
- `-`: 파일을 소유한 사용자(`hacker` 사용자)가 실행할 수 _없습니다_
- `r`: 파일을 소유한 그룹(`hacker` 그룹)의 사용자가 읽을 수 있습니다
- `-`: 파일을 소유한 그룹(`hacker` 그룹)의 사용자가 쓸 수 _없습니다_
- `-`: 파일을 소유한 그룹(`hacker` 그룹)의 사용자가 실행할 수 _없습니다_
- `r`: 그 외 모든 사용자가 읽을 수 있습니다
- `-`: 그 외 모든 사용자가 쓸 수 _없습니다_
- `-`: 그 외 모든 사용자가 실행할 수 _없습니다_

이제 `/flag`의 기본 권한을 봅시다:

```console
hacker@dojo:~$ ls -l /flag
-r-------- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$
```

여기에는 비트가 딱 하나 설정되어 있습니다. 소유 사용자(여기서는 `root`)의 `r`ead 권한입니다.
소유 그룹(`root` 그룹)의 구성원과 그 외 모든 사용자는 이 파일에 접근할 수 없습니다.

그렇다면 파일에 그룹 접근 권한이 없는데 `chgrp` 레벨들은 어떻게 동작했는지 궁금할 수 있습니다.
그 레벨들에서는 권한을 다르게 설정해 두었습니다:

```console
hacker@dojo:~$ ls -l /flag
-r--r----- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$
```

그룹에 접근 권한이 있었습니다!
그래서 파일을 `chgrp`하면 읽을 수 있게 되었던 것입니다.

아무튼!
소유권과 마찬가지로 파일 권한도 바꿀 수 있습니다.
`chmod`(**ch**ange **mod**e) 명령으로 합니다.
chmod의 기본 사용법은 다음과 같습니다:

```
chmod [OPTIONS] MODE FILE
```

`MODE`는 두 가지 방식으로 지정할 수 있습니다. 기존 권한 모드를 수정하는 방식과, 기존 것을 덮어쓰는 완전히 새로운 모드를 주는 방식입니다.

이 레벨에서는 앞의 것, 즉 기존 모드를 수정하는 방식을 다룹니다.
`chmod`는 `WHO`+/-`WHAT` 형식으로 권한을 손볼 수 있게 해 주는데, `WHO`는 user/group/other이고 `WHAT`은 read/write/execute입니다.
예를 들어 소유 _사용자_ 에게 _읽기_ 권한을 더하려면 `u+r` 모드를 지정합니다.
`g`roup과 `o`ther(또는 `a`ll)에 대한 `w`rite와 e`x`ecute 권한도 같은 방식으로 지정합니다.
예시를 더 보면:

- 위에서 본 `u+r`는 사용자 권한에 읽기 접근을 더합니다
- `g+wx`는 그룹 권한에 쓰기와 실행 접근을 더합니다
- `o-w`는 그 외 사용자의 쓰기 접근을 _제거_ 합니다
- `a-rwx`는 사용자, 그룹, 그 외 모두의 모든 권한을 제거합니다

그래서:

```console
root@dojo:~# mkdir pwn_directory
root@dojo:~# touch college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root root    0 May 22 13:42 college_file
drwxr-xr-x 2 root root 4096 May 22 13:42 pwn_directory
root@dojo:~# chmod go-rwx *
root@dojo:~# ls -l
total 4
-rw------- 1 hacker root    0 May 22 13:42 college_file
drwx------ 2 root   root 4096 May 22 13:42 pwn_directory
root@dojo:~#
```

이 챌린지에서는 `/flag` 파일의 권한을 바꿔서 읽어야 합니다!
보통은 파일의 권한을 바꾸려면 그 파일의 소유자여야 하지만, 이 레벨에서는 `chmod` 명령을 전능하게 만들어 두었으므로 `hacker` 사용자이면서도 원하는 것을 무엇이든 `chmod`할 수 있습니다.
이것은 궁극의 힘입니다.
`/flag` 파일은 `root`가 소유하고 있고 그것은 바꿀 수 없지만, 읽을 수 있게 만들 수는 있습니다.
가서 풀어보세요!
