셸 사용자들이 파일을 환경 변수로 읽어 들이려 할 때, 흔히 이렇게 합니다:

```console
hacker@dojo:~$ echo "test" > some_file
hacker@dojo:~$ VAR=$(cat some_file)
hacker@dojo:~$ echo $VAR
test
```

동작하기는 하지만, 까칠한 해커들이 ["쓸데없는 cat 사용"](https://porkmail.org/era/unix/award#cat)이라고 부르는 것에 해당합니다.
즉 파일을 읽으려고 별도의 프로그램을 통째로 실행하는 것은 낭비라는 뜻입니다.
알고 보면 셸의 힘만으로도 할 수 있습니다!

앞에서 사용자 입력을 변수로 `read`했습니다.
그리고 파일을 명령의 입력으로 리다이렉트해 보기도 했습니다!
이 둘을 합치면 셸만으로 파일을 읽을 수 있습니다.

```console
hacker@dojo:~$ echo "test" > some_file
hacker@dojo:~$ read VAR < some_file
hacker@dojo:~$ echo $VAR
test
```

여기서 무슨 일이 일어났을까요?
이 예시는 `some_file`을 `read`의 *표준 입력* 으로 리다이렉트했고, 그래서 `read`가 `VAR`로 읽어 들일 때 그 파일에서 읽은 것입니다!
이제 그것을 써서 `/challenge/read_me`를 `PWN` 환경 변수로 읽어 들이면 플래그를 드리겠습니다!
`/challenge/read_me`는 계속 바뀌므로, 명령 하나로 곧바로 `PWN` 변수에 읽어 들여야 합니다!
