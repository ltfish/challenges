앞 레벨의 예시를 떠올려 봅시다:

```console
hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
```

여기서 보이는 것은 물론 `hacker`가 자기만의 명령을 들여와 셸을 더 쓸모 있게 만드는 모습입니다.
시간이 지나면 여러분도 우아한 도구들을 모으게 될 것입니다.
`win`부터 시작해 봅시다!

앞에서는 `/challenge/run`이 실행하는 `win` 명령이 `/challenge/more_commands`에 있었습니다.
이번에는 `win`이 존재하지 않습니다!
[명령어 이어붙이기](/linux-luminarium/chaining)의 마지막 레벨을 떠올려 `win`이라는 셸 스크립트를 만들고, 그 위치를 `PATH`에 추가해서 `/challenge/run`이 찾을 수 있게 하세요!

----
**힌트:**
`/challenge/run`은 `root`로 실행되며 `win`을 호출합니다. 따라서 `win`은 그냥 플래그 파일을 cat하면 됩니다.
다시 말하지만 `/challenge/run`에 필요한 것은 `win` _뿐_ 이므로, `PATH`를 그 디렉터리 하나로 덮어써도 됩니다.
다만 그렇게 하면 여러분의 `win` 명령이 `cat`을 찾지 못한다는 점을 기억하세요.

그것을 피하는 방법은 셋입니다:

1. 파일 시스템에서 `cat` 프로그램이 어디 있는지 알아내세요. `PATH` 변수에 들어 있는 디렉터리 어딘가에 있을 _수밖에_ 없으니, 그 변수를 출력해 보고([셸 변수](/linux-luminarium/variables)에서 방법을 떠올려 보세요!) 그 안의 디렉터리들을(각 항목은 `:`로 구분된다는 것을 기억하세요) 훑어서 `cat`이 있는 곳을 찾아, 절대 경로로 `cat`을 실행하세요.
2. 기존 디렉터리들 _더하기_ `win`을 만든 위치를 새 항목으로 넣은 `PATH`를 설정하세요.
3. (역시 [셸 변수](/linux-luminarium/variables)를 참고해서) `read`로 `/flag`를 읽으세요. `read`는 `bash`의 내장 기능이므로 `PATH` 장난에 영향을 받지 않습니다.

자, 이제 가서 `win`하세요!
