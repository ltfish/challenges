`grep` 명령어에는 아주 유용한 옵션이 있습니다: `-v`(매칭 반전)입니다.
보통의 `grep`은 패턴에 매칭되는 줄을 보여주지만, `grep -v`는 패턴에 매칭되지 _않는_ 줄을 보여줍니다:

```console
hacker@dojo:~$ cat data.txt
hello hackers!
hello world!
hacker@dojo:~$ cat data.txt | grep -v world
hello hackers!
hacker@dojo:~$
```

때로는 원하는 데이터만 남기는 유일한 방법이, 원하지 _않는_ 데이터를 걸러 _내는_ 것일 때가 있습니다.
이 챌린지에서 `/challenge/run`은 플래그를 stdout으로 내보내지만, 진짜 플래그에 섞어서 1000개가 넘는 가짜 플래그(플래그 어딘가에 `DECOY`라는 단어가 들어 있습니다)도 함께 내보냅니다.
가짜들을 걸러 _내고_ 진짜 플래그를 남겨야 합니다!

`grep -v`로 "DECOY"가 들어간 줄을 모두 걸러내고 진짜 플래그를 찾아내세요!
