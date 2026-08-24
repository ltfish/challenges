셸로 작업하다 보면 어떤 명령의 출력을 변수에 저장하고 싶을 때가 많습니다.
다행히 셸은 [_명령 치환(Command Substitution)_](https://www.gnu.org/software/bash/manual/html_node/Command-Substitution.html)이라는 것으로 이를 아주 쉽게 해 줍니다!
보세요:

```console
hacker@dojo:~$ FLAG=$(cat /flag)
hacker@dojo:~$ echo "$FLAG"
pwn.college{blahblahblah}
hacker@dojo:~$
```

멋지네요!
이제 직접 해보세요.
`/challenge/run` 명령의 출력을 곧바로 `PWN`이라는 변수로 읽어 들이면, 거기에 플래그가 담깁니다!

----
**토막 상식:**
`$()` 대신 백틱을 쓸 수도 있습니다. 위 예시에서 ``FLAG=$(cat /flag)`` 대신 `` FLAG=`cat /flag` ``처럼요.
이것은 더 오래된 형식이고 몇 가지 단점이 있습니다.
예를 들어 명령 치환을 _중첩_ 하고 싶다고 해봅시다.
`$(cat $(find / -name flag))`를 백틱으로 어떻게 쓸까요?
pwn.college의 공식 입장은 `` `blah` `` 대신 `$(blah)`를 쓰라는 것입니다.
