실수를 하지 않더라도 사용자는 자기도 모르게 위험을 남겨둘 수 있습니다.
예를 들어 일반적인 사용자의 홈 디렉터리에 있는 많은 파일이 민감한 정보를 담는 데 자주 쓰이면서도 _기본적으로 누구나 읽을 수 있습니다_.
믿기지 않겠지만, 명시적으로 바꾸지 않는 한 여러분의 `.bashrc`도 누구나 읽을 수 있습니다!

```console
hacker@dojo:~$ ls -l ~/.bashrc
-rw-r--r-- 1 hacker hacker 148 Jun  7 05:56 /home/hacker/.bashrc
hacker@dojo:~$
```

"적어도 기본적으로 누구나 쓸 수 있는 건 아니잖아!"라고 생각할 수도 있습니다.
하지만 읽을 수만 있어도 피해를 줄 수 있습니다.
`.bashrc`는 셸이 시작할 때 처리하므로, 사람들은 보통 자기가 바꾸고 싶은 환경 변수의 초기화를 거기에 넣습니다.
대개는 `PATH` 같은 무해한 것이지만, 때로는 편하게 쓰려고 API 키를 넣어두기도 합니다.
예를 들어 이 챌린지에서는:

```
zardus@dojo:~$ echo "FLAG_GETTER_API_KEY=sk-XXXYYYZZZ" > ~/.bashrc
```

이렇게 해두면 Zardus는 API 키를 손쉽게 참조할 수 있습니다.
이 레벨에서 사용자는 유효한 API 키로 플래그를 얻을 수 있습니다:

```
zardus@dojo:~$ flag_getter --key $FLAG_GETTER_API_KEY
Correct API key! Do you want me to print the key (y/n)? y
pwn.college{HACKED}
zardus@dojo:~$
```

당연히 Zardus는 자기 키를 `.bashrc`에 보관합니다.
그 키를 훔쳐 플래그를 얻을 수 있을까요?

----
**참고:**
API 키를 얻으면 `hacker` 사용자로 그냥 `flag_getter`를 실행하세요.
이 챌린지의 `/challenge/victim`은 분위기를 내기 위한 것일 뿐, 쓸 필요는 없습니다.
