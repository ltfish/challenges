지금까지의 `if` 문은 특정한 경우를 처리했는데, 나머지는 어떻게 할까요?
그럴 때 `else`가 등장합니다!

`else` 절은 `if` 조건이 거짓일 때 실행됩니다:

```bash
if [ "$1" == "hello" ]
then
    echo "Hi there!"
else
    echo "I don't understand"
fi
```

`else`에는 조건이 없다는 점에 주의하세요. 앞에서 걸리지 않은 나머지를 모두 받습니다.
`then` 문도 없습니다.
마지막으로 `fi`는 `else` 블록 뒤에 와서 이 복합 문 전체의 끝을 표시합니다!
`else`는 선택 사항이기도 합니다. 앞 레벨에서는 쓰지 않았고, 원하는 로직에 필요할 때만 쓰면 됩니다.

실용적인 예시입니다:

```bash
if [ "$1" == "start" ]
then
    echo "Starting the service..."
else
    echo "Unknown command. Use 'start' to begin."
fi
```

이 챌린지에서는 `/home/hacker/solve.sh`에 다음과 같은 스크립트를 작성하세요:

- 인자 하나를 받습니다
- 인자가 "pwn"이면 "college"를 출력합니다
- 그 밖의 입력에는 "nope"을 출력합니다

예시:

```console
hacker@dojo:~$ bash /home/hacker/solve.sh pwn
college
hacker@dojo:~$ bash /home/hacker/solve.sh hack
nope
hacker@dojo:~$ bash /home/hacker/solve.sh anything
nope
hacker@dojo:~$
```

스크립트가 제대로 동작하면 `/challenge/run`을 실행해서 플래그를 얻으세요!
