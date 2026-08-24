때로는 첫 번째 열, 세 번째 열, 42번째 열처럼 특정 열의 데이터만 뽑아내고 싶을 때가 있습니다.
그럴 때 쓰는 것이 `cut` 명령어입니다.

예를 들어 다음과 같은 데이터 파일이 있다고 해봅시다:

```console
hacker@dojo:~$ cat scores.txt
hacker 78 99 67
root 92 43 89
hacker@dojo:~$
```

`cut`으로 특정 열을 뽑아낼 수 있습니다:

```console
hacker@dojo:~$ cut -d " " -f 1 scores.txt
hacker
root
hacker@dojo:~$ cut -d " " -f 2 scores.txt
78
92
hacker@dojo:~$ cut -d " " -f 3 scores.txt
99
43
hacker@dojo:~$
```

`-d` 인자는 열 _구분자(delimiter)_ 를 지정합니다(열을 무엇으로 나누는지).
여기서는 공백 문자입니다.
물론 셸이 그 공백을 다른 인자를 나누는 공백이 아니라 인자 자체로 알아보도록 따옴표로 묶어야 합니다!
`-f` 인자는 _필드(field)_ 번호, 즉 몇 번째 열을 뽑을지 지정합니다.

이 챌린지에서 `/challenge/run` 프로그램은 무작위 숫자와 (플래그의) 한 글자짜리 문자를 열로 갖는 여러 줄을 출력합니다.
`cut`으로 플래그 문자를 뽑아낸 다음, (앞 레벨처럼!) `tr -d "\n"`으로 파이프해서 한 줄로 이어 붙이세요.
풀이는 `/challenge/run | cut ??? | tr ???`에서 `???`를 채운 형태가 될 것입니다.
