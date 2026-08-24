셸 스크립트를 만드는 법을 배웠지만, 지금까지는 그저 명령의 나열이었습니다.
스크립트는 인자를 받을 수 있게 되면 훨씬 강력해집니다!
이런 모습입니다:

```console
hacker@dojo:~$ bash myscript.sh hello world
```

스크립트는 특별한 변수로 이 인자들에 접근합니다:
- `$1`은 첫 번째 인자("hello")를 담습니다
- `$2`는 두 번째 인자("world")를 담습니다
- `$3`은 (있었다면) 세 번째 인자를 담습니다
- ...그런 식으로 이어집니다

간단한 예시입니다:
```bash
hacker@dojo:~$ cat myscript.sh
#!/bin/bash
echo "First argument: $1"
echo "Second argument: $2"
hacker@dojo:~$ bash myscript.sh hello world
First argument: hello
Second argument: world
hacker@dojo:~$
```

이 챌린지에서는 `/home/hacker/solve.sh`에 다음과 같은 스크립트를 작성해야 합니다:
1. 인자 두 개를 받습니다
2. 그것들을 역순으로 출력합니다(두 번째 인자를 먼저, 그다음 첫 번째 인자)

예를 들면:
```console
hacker@dojo:~$ bash /home/hacker/solve.sh pwn college
college pwn
hacker@dojo:~$
```

스크립트가 제대로 동작하면 `/challenge/run`을 실행해서 플래그를 얻으세요!
