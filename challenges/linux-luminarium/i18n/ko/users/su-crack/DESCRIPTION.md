`su`에 비밀번호를 입력하면, 그 사용자에 대해 저장된 비밀번호와 비교합니다.
이 비밀번호는 _예전에는_ `/etc/passwd`에 저장되었지만, `/etc/passwd`는 누구나 읽을 수 있는 파일이라 비밀번호를 두기에 좋지 않아서 `/etc/shadow`로 옮겨졌습니다.
앞 레벨에 나온 `/etc/shadow` 예시입니다:

```console
root:$6$s74oZg/4.RnUvwo2$hRmCHZ9rxX56BbjnXcxa0MdOsW2moiW8qcAl/Aoc7NEuXl2DmJXPi3gLp7hmyloQvRhjXJ.wjqJ7PprVKLDtg/:19921:0:99999:7:::
daemon:*:19873:0:99999:7:::
bin:*:19873:0:99999:7:::
sys:*:19873:0:99999:7:::
sync:*:19873:0:99999:7:::
games:*:19873:0:99999:7:::
man:*:19873:0:99999:7:::
lp:*:19873:0:99999:7:::
mail:*:19873:0:99999:7:::
news:*:19873:0:99999:7:::
uucp:*:19873:0:99999:7:::
proxy:*:19873:0:99999:7:::
www-data:*:19873:0:99999:7:::
backup:*:19873:0:99999:7:::
list:*:19873:0:99999:7:::
irc:*:19873:0:99999:7:::
gnats:*:19873:0:99999:7:::
nobody:*:19873:0:99999:7:::
_apt:*:19873:0:99999:7:::
systemd-timesync:*:19901:0:99999:7:::
systemd-network:*:19901:0:99999:7:::
systemd-resolve:*:19901:0:99999:7:::
mysql:!:19901:0:99999:7:::
messagebus:*:19901:0:99999:7:::
sshd:*:19901:0:99999:7:::
hacker::19916:0:99999:7:::
zardus:$6$bEFkpM0w/6J0n979$47ksu/JE5QK6hSeB7mmuvJyY05wVypMhMMnEPTIddNUb5R9KXgNTYRTm75VOu1oRLGLbAql3ylkVa5ExuPov1.:19921:0:99999:7:::
```

`:`로 구분된 각 줄에서 첫 번째 필드는 사용자명이고 두 번째는 비밀번호입니다.
값이 `*`나 `!`이면 사실상 그 계정의 비밀번호 로그인이 비활성화되어 있다는 뜻이고, 빈 필드는 비밀번호가 없다는 뜻이며(어떤 설정에서는 비밀번호 없이 `su`할 수 있게 되는, 드물지 않은 설정 실수입니다), Zardus의 `$6$bEFkpM0w/6J0n979$47ksu/JE5QK6hSeB7mmuvJyY05wVypMhMMnEPTIddNUb5R9KXgNTYRTm75VOu1oRLGLbAql3ylkVa5ExuPov1.` 같은 긴 문자열은 앞 레벨에 나온 Zardus의 비밀번호(여기서는 `dont-hack-me`)를 단방향 암호화(해싱)한 결과입니다.
이 파일의 다른 필드에도 각각 의미가 있으며, [여기](https://www.cyberciti.biz/faq/understanding-etcshadow-file/)에서 더 읽어볼 수 있습니다.

`su`에 비밀번호를 입력하면, `su`는 그것을 단방향 암호화(해싱)해서 저장된 값과 비교합니다.
결과가 일치하면 `su`는 그 사용자로 전환할 수 있게 해 줍니다!

그런데 비밀번호를 모른다면 어떨까요?
비밀번호의 해시 값을 가지고 있다면 _크래킹_ 할 수 있습니다!
`/etc/shadow`는 기본적으로 `root`만 읽을 수 있지만, 유출은 일어나기 마련입니다!
예를 들어 백업은 암호화되지 않고 충분히 보호되지 않은 채 파일 서버에 보관되는 경우가 많고, 이 때문에 셀 수 없이 많은 데이터 유출이 일어났습니다.

해커가 유출된 `/etc/shadow`를 손에 넣으면 비밀번호를 크래킹하며 온갖 난동을 부릴 수 있습니다.
크래킹은 유명한 [John the Ripper](https://www.openwall.com/john/)로 할 수 있습니다:

```console
hacker@dojo:~$ john ./my-leaked-shadow-file
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Will run 32 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
password1337      (zardus)
1g 0:00:00:22 3/3 0.04528g/s 10509p/s 10509c/s 10509C/s lykys..lank
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker@dojo:~$
```

여기서 John the Ripper는 유출된 Zardus의 비밀번호 해시를 크래킹해서 실제 값이 `password1337`임을 알아냈습니다.
가엾은 Zardus!

이 레벨은 그 이야기를 재현해서 `/etc/shadow` 유출본(`/challenge/shadow-leak`)을 줍니다.
그것을 크래킹하고(몇 분 걸릴 수 있습니다) `zardus`로 `su`한 뒤 `/challenge/run`을 실행해 플래그를 얻으세요!
