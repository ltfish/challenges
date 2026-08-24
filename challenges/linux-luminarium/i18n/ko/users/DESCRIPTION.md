`hacker`인 여러분이 이 기계 속의 유일한 유령이라고 생각했나요?
보통의 리눅스 시스템에는 사용자가 아주 많습니다!
리눅스 시스템의 전체 사용자 목록은 `/etc/passwd` 파일에 적혀 있습니다(이름은 역사적인 이유로 그렇게 붙었을 뿐, 실제로는 더 이상 비밀번호를 담고 있지 않습니다).
도장 컨테이너에서 가져온 예시입니다:

```console
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
systemd-timesync:x:101:101:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
systemd-network:x:102:103:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin
systemd-resolve:x:103:104:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
mysql:x:104:105:MySQL Server,,,:/nonexistent:/bin/false
messagebus:x:105:106::/nonexistent:/usr/sbin/nologin
sshd:x:106:65534::/run/sshd:/usr/sbin/nologin
hacker:x:1000:1000::/home/hacker:/bin/bash
```

사용자도 많고, 정보도 많습니다!
각 줄은 `:`로 구분되어 사용자명, 예전에 비밀번호가 있던 자리를 대신하는 `x`(실제 비밀번호가 어디 있는지는 나중에 다룹니다), 숫자로 된 사용자 ID, 숫자로 된 기본 그룹 ID, 사용자에 대한 긴 설명, 홈 디렉터리, 기본 셸을 담고 있습니다.

맨 아래에 `hacker` 사용자가 보입니다.
바로 여러분입니다!
나머지 사용자 대부분은 역사적인 이유로 남아 있거나, 설치된 각종 소프트웨어를 뒷받침하는 서비스 계정이거나, "유틸리티" 계정입니다(예를 들어 `nobody` 사용자는 어떤 프로그램이 아무런 특권 없이 실행되도록 보장하는 데 쓰입니다).

특히 중요한 사용자가 하나 있습니다: 시스템 관리자인 `root`입니다.
시스템 관리자는 명백한 보안적 함의를 가집니다: 리눅스의 이런저런 기능을 통해 어떻게든 `root` 사용자가 될 수 있는 `hacker` 사용자는 시스템을 마음대로 헤집을 수 있습니다.
시스템에 침투한 해커의 아주 흔한 목표가 바로 `root`로 권한을 상승시키는 것이며, 그렇기에 `root`는 무슨 수를 써서라도 지켜내야 합니다!

이 모듈에서는 사용자를 둘러싼 온갖 장난을 살펴보고, 시스템을 관리하기 위해 사용자를 전환하는 정석적인 방법들을 배우며, 그 과정에서 즐거운 시간을 보내봅시다!
