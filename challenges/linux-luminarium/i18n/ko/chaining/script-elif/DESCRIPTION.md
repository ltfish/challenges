`if` 문 하나로 조건을 검사하는 법을 배웠습니다.
그런데 여러 조건을 검사해야 한다면 어떨까요?
`elif`(`else if`의 줄임말)를 쓰면 됩니다:

```bash
if [ "$1" == "one" ]
then
    echo "1"
elif [ "$1" == "two" ]
then
    echo "2"
elif [ "$1" == "three" ]
then
    echo "3"
else
    echo "unknown"
fi
```

`if`와 마찬가지로 elif 뒤에도 `then`이 _필요하다는_ 점에 주의하세요.
앞서와 같이 마지막의 `else`는 어디에도 걸리지 않은 나머지를 모두 받습니다.

이 챌린지에서는 `/home/hacker/solve.sh`에 다음과 같은 스크립트를 작성하세요:

- 인자 하나를 받습니다
- 인자가 "hack"이면 "the planet"을 출력합니다
- 인자가 "pwn"이면 "college"를 출력합니다  
- 인자가 "learn"이면 "linux"를 출력합니다
- 그 밖의 입력에는 "unknown"을 출력합니다

예시:

```console
hacker@dojo:~$ bash /home/hacker/solve.sh hack
the planet
hacker@dojo:~$ bash /home/hacker/solve.sh pwn
college
hacker@dojo:~$ bash /home/hacker/solve.sh learn
linux
hacker@dojo:~$ bash /home/hacker/solve.sh foo
unknown
hacker@dojo:~$
```

스크립트가 제대로 동작하면 `/challenge/run`을 실행해서 플래그를 얻으세요!

----
**참고:**
스크립트를 작성할 때 예시의 띄어쓰기를 꼼꼼히 따르세요.
다른 많은 언어와 달리 bash는 `[`와 `]`가 다른 문자와 공백으로 분리되어 있어야 하며, 그렇지 않으면 조건을 해석하지 못합니다.
