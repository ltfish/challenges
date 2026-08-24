자, Zardus가 정신을 차렸습니다!
홈 디렉터리 공유는 더 이상 없습니다. 편의는 줄었지만 Zardus는 `/tmp/collab`을 공유하는 쪽으로 옮겼습니다.
그 디렉터리를 누구나 쓸 수 있게 만들고, 기억해 둘 사악한 명령 목록을 만들기 시작했습니다!

```console
zardus@dojo:~$ mkdir /tmp/collab
zardus@dojo:~$ chmod a+w /tmp/collab
zardus@dojo:~$ echo "rm -rf /" > /tmp/collab/evil-commands.txt
```

이 챌린지에서 `/challenge/victim`을 실행하면 Zardus가 그 명령 목록에 `cat /flag`를 추가합니다:

```console
hacker@dojo:~$ /challenge/victim

Username: zardus
Password: **********
zardus@dojo:~$ echo "cat /flag" >> /tmp/collab/evil-commands.txt
zardus@dojo:~$ exit
logout

hacker@dojo:~$
```

앞 레벨에서 보았듯, `/tmp/collab`에 쓰기 권한이 있는 `hacker` 사용자는 그 `evil-commands.txt` 파일을 바꿔치기할 수 있습니다.
또 [명령어 이해하기](/linux-luminarium/commands)에서 파일이 다른 파일로 _링크_ 될 수 있다는 것도 기억하세요.
`hacker`가 `evil-commands.txt`를, `zardus`가 쓸 수 있는 어떤 민감한 파일로 향하는 심볼릭 링크로 바꿔치기하면 어떻게 될까요?
혼돈과 장난이 벌어집니다!

링크할 파일이 무엇인지는 _알고 있을_ 것입니다.
공격을 성공시켜 `/flag`를 얻으세요(이 레벨에서는 Zardus가 다시 읽을 수 있습니다!).

----
**힌트:**
`/challenge/victim`을 두 번 실행해야 합니다. 한 번은 `cat /flag`가 원하는 곳에 쓰이게 하려고, 또 한 번은 그것이 실행되게 하려고요!

**`/tmp`는 쓰기 위험한가요???**
여기서 보여준 공격에도 불구하고 `/tmp`는 안전하게 쓸 수 있습니다.
이 디렉터리는 _누구나 쓸 수 있지만_ 특별한 권한 비트가 설정되어 있습니다:

```console
hacker@dojo:~$ ls -ld /tmp
drwxrwxrwt 29 root root 1056768 Jun  6 14:06 /tmp
hacker@dojo:~$
```

끝에 있는 `t` 비트가 _스티키(sticky)_ 비트입니다.
스티키 비트는 그 디렉터리 안의 파일을 파일 소유자만 이름 바꾸거나 지울 수 있게 합니다.
바로 이 공격을 막으려고 설계된 것이죠!
물론 이 챌린지의 문제는 Zardus가 `/tmp/collab`에 스티키 비트를 켜지 않았다는 점입니다.
이 경우에는 그것으로 구멍을 막을 수 있었을 것입니다:

```console
zardus@dojo:~$ chmod +t /tmp/collab
```

물론 누구나 쓸 수 있는 디렉터리 같은 공유 자원은 여전히 위험합니다.
훨씬 뒤의 그린 벨트 자료인 [경쟁 조건](/system-security/race-conditions)에서, 그런 자원이 보안 문제를 일으키는 여러 방식을 보게 될 것입니다!
