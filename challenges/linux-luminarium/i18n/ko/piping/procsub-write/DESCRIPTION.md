프로세스 치환이 `<(command)`로 명령의 출력을 읽을 수 있는 파일처럼 보이게 한다는 것을 배웠습니다.
그런데 프로세스 치환은 명령에 _쓰는_ 데에도 쓸 수 있습니다!

`tee`로 데이터를 두 파일에 복제할 수 있습니다:

```console
hacker@dojo:~$ echo HACK | tee THE > PLANET
hacker@dojo:~$ cat THE
HACK
hacker@dojo:~$ cat PLANET
HACK
hacker@dojo:~$
```

그리고 `tee`로 데이터를 파일과 명령에 복제해 보기도 했습니다:

```console
hacker@dojo:~$ echo HACK | tee THE | cat
HACK
hacker@dojo:~$ cat THE
HACK
hacker@dojo:~$
```

그렇다면 두 개의 명령에 복제하려면 어떻게 할까요?
`tee`의 man 페이지에 나와 있듯이, `tee`는 파일과 표준 출력에 쓰도록 설계되었습니다:

```text
TEE(1)                           User Commands                          TEE(1)

NAME
       tee - read from standard input and write to standard output and files
```

그런데 잠깐! 방금 bash가 프로세스 치환으로 명령을 파일처럼 보이게 할 수 있다는 것을 배웠죠!
명령에 쓸 때(출력 프로세스 치환)는 `>(command)`를 씁니다.
`>(rev)`를 인자로 쓰면 bash가 `rev` 명령을 실행하고(이 명령은 표준 입력에서 데이터를 읽어 순서를 뒤집어 표준 출력으로 씁니다!) 그 입력을 임시 이름 있는 파이프 파일에 연결합니다.
명령이 이 파일에 쓰면 그 데이터는 해당 명령의 표준 입력으로 들어갑니다:

```console
hacker@dojo:~$ echo HACK | rev
KCAH
hacker@dojo:~$ echo HACK | tee >(rev)
HACK
KCAH
```

위에서는 다음 순서로 일이 일어났습니다:

1. `bash`가 `rev` 명령을 띄우고, 이름 있는 파이프(아마 `/dev/fd/63`)를 `rev`의 표준 입력에 연결했습니다
2. `bash`가 `tee` 명령을 띄우면서 그 표준 입력에 파이프를 연결하고, `tee`의 첫 인자를 `/dev/fd/63`으로 바꿔치기했습니다. `tee`는 `>(rev)`라는 인자를 본 적조차 없습니다. 셸이 `tee`를 띄우기 전에 그것을 _치환_ 했으니까요
3. `bash`가 `echo` 빌트인으로 `HACK`을 `tee`의 표준 입력에 찍어 넣었습니다
4. `tee`가 `HACK`을 읽어 표준 출력에 쓰고, 이어서 `/dev/fd/63`(`rev`의 stdin에 연결되어 있죠)에 썼습니다
5. `rev`가 표준 입력에서 `HACK`을 읽어 뒤집고, `KCAH`를 표준 출력에 썼습니다

이제 여러분 차례입니다!
이 챌린지에는 `/challenge/hack`, `/challenge/the`, `/challenge/planet`이 있습니다.
`/challenge/hack` 명령을 실행하고, 그 출력을 `/challenge/the`와 `/challenge/planet` 두 명령의 입력으로 복제하세요!
`tee`가 여러 출력 대상을 받을 수 있다는 점과, `>(command)`도 그런 대상 중 하나라는 점을 기억하세요.
이 방법이 가물가물하다면 앞의 "tee로 파이프 데이터 복제하기"와 "입력을 위한 프로세스 치환" 챌린지를 다시 훑어보세요.

----
**토막 상식!**

눈썰미 있는 학습자라면 다음 둘이 같다는 것을 알아챌 것입니다:

```console
hacker@dojo:~$ echo hi | rev
ih
hacker@dojo:~$ echo hi > >(rev)
ih
hacker@dojo:~$
```

데이터를 파이프하는 방법이 하나만은 아니네요!
물론 두 번째 방식이 훨씬 읽기 어렵고 확장하기도 어렵습니다.
예를 들면:

```console
hacker@dojo:~$ echo hi | rev | rev
hi
hacker@dojo:~$ echo hi > >(rev | rev)
hi
hacker@dojo:~$
```

좀 우스꽝스럽죠!
여기서 얻을 교훈은, 프로세스 치환이 도구 상자 속의 강력한 도구이긴 하지만 아주 _특수한_ 도구라는 것입니다. 모든 일에 쓰지는 마세요!
