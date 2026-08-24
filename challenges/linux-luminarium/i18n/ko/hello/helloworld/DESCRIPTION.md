이번에는 조금 더 복잡한 것을 해봅시다: _인자(argument)_ 가 있는 명령어입니다. 인자란 명령어에 함께 넘겨주는 추가 데이터를 말합니다.
한 줄을 입력하고 엔터를 치면, 셸은 사실 그 입력을 명령어와 _인자_ 로 나눠서 해석합니다.
첫 단어가 명령어이고, 뒤따르는 단어들이 인자입니다.
직접 봅시다:

```console
hacker@dojo:~$ echo Hello
Hello
hacker@dojo:~$
```

여기서 명령어는 `echo`, 인자는 `Hello`였습니다.
`echo`는 인자로 받은 것들을 위 세션처럼 터미널에 그대로 "메아리쳐" 돌려주는 간단한 명령어입니다.

인자가 여러 개인 `echo`도 봅시다:

```console
hacker@dojo:~$ echo Hello Hackers!
Hello Hackers!
hacker@dojo:~$
```

여기서 명령어는 `echo`였고, `Hello`와 `Hackers!`가 `echo`에 넘어간 두 개의 인자였습니다.
간단하죠!

이 챌린지에서 플래그를 얻으려면 `hello` 명령어를(`echo` 명령어가 아닙니다) `hackers`라는 인자 하나와 함께 실행해야 합니다.
지금 해보세요!
