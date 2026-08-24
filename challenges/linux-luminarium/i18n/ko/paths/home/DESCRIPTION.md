모든 사용자는 _홈 디렉터리(home directory)_ 를 가지며, 보통 파일 시스템의 `/home` 아래에 있습니다.
도장에서 여러분은 `hacker` 사용자이고, 홈 디렉터리는 `/home/hacker`입니다.
홈 디렉터리는 보통 사용자가 자신의 개인 파일을 대부분 보관하는 곳입니다.
pwn.college를 헤쳐 나가면서 여러분도 대부분의 풀이를 여기에 저장하게 될 것입니다.

보통 셸 세션은 홈 디렉터리를 현재 작업 디렉터리로 해서 시작합니다.
처음 프롬프트를 다시 봅시다:

```console
hacker@dojo:~$
```

이 프롬프트의 `~`가 바로 현재 작업 디렉터리이며, `~`는 `/home/hacker`의 줄임 표기입니다.
bash가 이런 줄임 표기를 제공하고 사용하는 이유는, 다시 말하지만 여러분이 대부분의 시간을 홈 디렉터리에서 보내기 때문입니다.
그래서 bash는 경로처럼 보이는 인자의 맨 앞에 `~`가 오면 그것을 홈 디렉터리로 확장합니다.
이런 식입니다:

```console
hacker@dojo:~$ echo LOOK: ~
LOOK: /home/hacker
hacker@dojo:~$ cd /
hacker@dojo:/$ cd ~
hacker@dojo:~$ cd ~/asdf
hacker@dojo:~/asdf$ cd ~/asdf
hacker@dojo:~/asdf$ cd ~
hacker@dojo:~$ cd /home/hacker/asdf
hacker@dojo:~/asdf$
```

`~`의 확장 결과는 _절대_ 경로이며, 맨 앞의 `~`만 확장된다는 점에 주의하세요.
예를 들어 `~/~`는 `/home/hacker/home/hacker`가 아니라 `/home/hacker/~`로 확장됩니다.

재미있는 사실: `cd`는 목적지를 적지 않으면 홈 디렉터리를 기본값으로 씁니다:

```console
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ cd
hacker@dojo:~$
```

이제 여러분 차례입니다!
이 챌린지에서 `/challenge/run`은 커맨드 라인에 인자로 지정한 파일에 플래그 사본을 써줍니다. 단, 다음 제약이 있습니다:

1. 인자는 반드시 절대 경로여야 합니다.
2. 그 경로는 반드시 홈 디렉터리 안에 있어야 합니다.
3. 확장되기 전의 인자는 반드시 세 글자 이하여야 합니다.

다시 말하지만, 경로는 다음처럼 `/challenge/run`의 _인자_ 로 넘겨야 합니다(`YOUR_PATH_HERE` 자리에 여러분의 경로를 적으세요):

```console
hacker@dojo:~$ /challenge/run YOUR_PATH_HERE
```
