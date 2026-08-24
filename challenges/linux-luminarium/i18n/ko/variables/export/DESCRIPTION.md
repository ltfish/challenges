기본적으로 셸 세션에서 설정한 변수는 그 셸 프로세스에만 유효합니다.
즉, 실행하는 다른 명령들은 그 변수를 물려받지 않습니다.
자기 셸 안에서 또 다른 셸 프로세스를 띄워 보면 이를 직접 확인할 수 있습니다:

```console
hacker@dojo:~$ VAR=1337
hacker@dojo:~$ echo "VAR is: $VAR"
VAR is: 1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 
```

위 출력에서 `$` 프롬프트는 메인 셸 프로세스의 *자식* 으로 실행된 최소 기능 셸 `sh`의 프롬프트입니다.
그리고 `VAR` 변수를 받지 못했습니다!

당연한 일입니다.
셸 변수에는 민감하거나 이상한 데이터가 있을 수 있는데, 명시적으로 원하지 않는 한 실행하는 다른 프로그램으로 새어 나가면 곤란하니까요.
그렇다면 새어 나가도 된다고 어떻게 표시할까요?
변수를 *export* 하면 됩니다.
변수를 export하면 그 변수는 자식 프로세스의 *환경 변수* 로 전달됩니다.
환경 변수 개념은 다른 챌린지에서도 만나겠지만, 그 효과는 여기서 확인할 수 있습니다.
예시입니다:

```console
hacker@dojo:~$ VAR=1337
hacker@dojo:~$ export VAR
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
```

이번에는 자식 셸이 VAR의 값을 받아서 출력했습니다!
앞의 두 줄을 합칠 수도 있습니다.

```console
hacker@dojo:~$ export VAR=1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
```

이 챌린지에서는 `PWN` 변수를 `COLLEGE` 값으로 설정해 export하고, `COLLEGE` 변수는 `PWN` 값으로 설정하되 export하지 *않은* 채로(즉 `/challenge/run`이 물려받지 않게) `/challenge/run`을 실행해야 합니다.
행운을 빕니다!
