때로는 `cat`으로 읽어내려는 파일이 너무 클 수 있습니다.
다행히 필요한 내용을 찾아주는 `grep` 명령어가 있습니다!
이 챌린지에서 배워봅시다.

`grep`을 쓰는 방법은 여러 가지인데, 여기서는 한 가지를 배웁니다:

```console
hacker@dojo:~$ grep SEARCH_STRING /path/to/file
```

이렇게 실행하면 `grep`은 파일에서 `SEARCH_STRING`이 들어 있는 줄을 찾아 콘솔에 출력합니다.

이 챌린지에서는 `/challenge/data.txt` 파일에 십만 줄의 텍스트를 넣어 두었습니다.
`grep`으로 플래그를 찾아내세요!

힌트: 플래그는 항상 `pwn.college`라는 문자열로 시작합니다.
