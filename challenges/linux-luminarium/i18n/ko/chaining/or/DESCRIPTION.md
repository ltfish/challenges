방금 첫 명령이 성공했을 때만 두 번째 명령을 실행하는 `&&` 연산자를 배웠습니다.
이제 그 반대를 배워봅시다. `||` 연산자는 첫 번째 명령이 실패했을 때에만(0이 아닌 코드로 끝났을 때) 두 번째 명령을 실행하게 해 줍니다.
첫 명령이 성공하거나 아니면 두 번째 명령이 실행되므로 "OR" 연산자라고 부릅니다.

문법은 이렇습니다:
```console
hacker@dojo:~$ command1 || command2
```

뜻은 이렇습니다: "command1을 실행하고, 실패하면 command2를 실행하라."

예시를 보면:
```console
hacker@dojo:~$ touch /file || echo "touch failed, so this runs"
touch: cannot touch '/file': Permission denied
touch failed, so this runs
hacker@dojo:~$ touch /home/hacker/file || echo "this will NOT run"
hacker@dojo:~$
```

`||` 연산자는 대체 명령이나 오류 처리를 제공할 때 아주 유용합니다!

이 챌린지에서는 `/challenge/first-failure`와 `/challenge/second`를 `||` 연산자로 이어야 합니다.
해보세요!
