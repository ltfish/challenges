[프로세스](https://pwn.college/linux-luminarium/processes/) 모듈에서 종료 코드를 배웠습니다.
이제 그것으로 명령을 이어 붙여 봅시다!

`&&` 연산자는 첫 번째 명령이 성공했을 때에만(리눅스 관례로는 종료 코드 0으로 끝났을 때) 두 번째 명령을 실행하게 해 줍니다.
두 조건이 모두 참이어야 하므로 "AND" 연산자라고 부릅니다. 첫 번째 명령이 성공해야 하고, 그래야 두 번째 명령이 실행됩니다.
어떤 동작이 다른 동작의 성공에 달려 있는 복잡한 커맨드 라인 작업에서 아주 유용합니다.

문법은 이렇습니다:
```console
hacker@dojo:~$ command1 && command2
```

뜻은 이렇습니다: "command1을 실행하고, 성공하면 command2를 실행하라."

예시를 보면:

```console
hacker@dojo:~$ touch /home/hacker/file && echo "this will run"
success
this will run
hacker@dojo:~$ touch /file && echo "this will NOT run"
touch: cannot touch '/file': Permission denied
hacker@dojo:~$
```

두 번째 `touch`는 hacker 사용자에게 `/file`에 대한 쓰기 권한이 없어서 실패했고, 그래서 `echo`가 실행되지 않았습니다.

이 챌린지에서는 `/challenge/first-success`와 `/challenge/second` 프로그램을 `&&` 연산자로 이어야 합니다.
먼저 각 명령을 따로 실행해서 어떻게 되는지 보세요(플래그를 얻지 _못합니다_).
하지만 `&&`로 이으면 플래그가 나타납니다!
